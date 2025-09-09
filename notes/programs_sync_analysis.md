
# Analisi sincronizzacione programs dopo la modifica di un corso
Dopo la modifica o eliminazione di un corso da API, va gestito il ricalcolo dei progress e dei completamenti di tutti gli enrol_programs che contengono quel corso specifico, preferibilmente utilzzando le classi core del plugin Programs.

## Descrizione
Cosa succede quando cambia un corso

Eventi da ascoltare (core):
- \core\event\course_module_created
- \core\event\course_module_deleted
- \core\event\course_module_updated (copre move, change availability, ecc.)
- \core\event\course_deleted

Strategia robusta (senza bloccare la UI)
	
 	1.	Observer intercetta l’evento, ricava il courseid e trova tutti i programmi che includono quel corso:
	    SELECT DISTINCT programid FROM {enrol_programs_items} WHERE courseid = :courseid
	
 	2.	Queue di un adhoc task con i programids trovati (così lavori offline e in transazione separata).
	
 	3.	Nell’adhoc task, per ogni programid:
        - program::load_content($programid) → $top.
		- $top->autorepair() per riallineare sequenze/prev/Prerrequisiti del plugin (lo stiamo già usando: è il pezzo chiave “sicuro”).
  		- Invalidazione cache sul/i corsi coinvolti (coursemodinfo) e, volendo, invalidazione custom per il Program (se ne introduci una).
        - (Opzionale – “fase 2”): ricomputo esplicito dei progress/completion per gli utenti allocati al Program.

Perché è “medio” e non “hard”

	- La parte critica (consistenza struttura) la fa già il plugin con autorepair();
 	- il resto è plumbing: legare eventi → task → loop sui programmi;
  	- La parte potenzialmente più “profonda” è il ricomputo dei completion a livello di Program per utente, che dipende dall’API interna del plugin. Se c’è un metodo ufficiale (tipo program::update_* / allocation::*), lo usiamo. Se non c’è, si può calcolare “on the fly” dai course completion (completion_info / is_course_complete()) e scrivere dove richiesto — ma qui serve vedere le tabelle/metodi del plugin per non “bucare” la logica ufficiale;


## Skeleton di implementazione

local/wsvecomp/db/events.php

```php
<?php
defined('MOODLE_INTERNAL') || die();

$observers = [
    [
        'eventname'   => '\core\event\course_module_created',
        'callback'    => '\local_wsvecomp\observers::course_module_changed',
        'internal'    => false,
        'priority'    => 9999,
    ],
    [
        'eventname'   => '\core\event\course_module_updated',
        'callback'    => '\local_wsvecomp\observers::course_module_changed',
        'internal'    => false,
        'priority'    => 9999,
    ],
    [
        'eventname'   => '\core\event\course_module_deleted',
        'callback'    => '\local_wsvecomp\observers::course_module_changed',
        'internal'    => false,
        'priority'    => 9999,
    ],
    [
        'eventname'   => '\core\event\course_deleted',
        'callback'    => '\local_wsvecomp\observers::course_deleted',
        'internal'    => false,
        'priority'    => 9999,
    ],
];
?>
```

local/wsvecomp/classes/observers.php

```php
<?php
namespace local_wsvecomp;

defined('MOODLE_INTERNAL') || die();

class observers {
    public static function course_module_changed(\core\event\base $event): void {
        global $DB;
        $courseid = (int)($event->courseid ?? 0);
        if (!$courseid) { return; }

        $programids = $DB->get_fieldset_select('enrol_programs_items', 'DISTINCT programid', 'courseid = ?', [$courseid]);
        if (empty($programids)) { return; }

        $task = new \local_wsvecomp\task\recompute_programs_task();
        $task->set_component('local_wsvecomp');
        $task->set_custom_data((object)[
            'programids' => array_values(array_unique(array_map('intval', $programids))),
            'courseid'   => $courseid,
        ]);
        \core\task\manager::queue_adhoc_task($task, true);
    }

    public static function course_deleted(\core\event\course_deleted $event): void {
        global $DB;
        $courseid = (int)$event->objectid;
        // Stessa logica: trova Program che lo contenevano.
        $programids = $DB->get_fieldset_select('enrol_programs_items', 'DISTINCT programid', 'courseid = ?', [$courseid]);
        if (empty($programids)) { return; }

        $task = new \local_wsvecomp\task\recompute_programs_task();
        $task->set_component('local_wsvecomp');
        $task->set_custom_data((object)[
            'programids' => array_values(array_unique(array_map('intval', $programids))),
            'courseid'   => $courseid,
            'coursedeleted' => true,
        ]);
        \core\task\manager::queue_adhoc_task($task, true);
    }
}
?>
```

local/wsvecomp/classes/task/recompute_programs_task.

```php
<?php
namespace local_wsvecomp\task;

defined('MOODLE_INTERNAL') || die();

use core\task\adhoc_task;

class recompute_programs_task extends adhoc_task {
    public function get_component() { return 'local_wsvecomp'; }

    public function execute() {
        global $DB;

        $data = $this->get_custom_data();
        $programids = isset($data->programids) ? (array)$data->programids : [];
        if (empty($programids)) { return; }

        foreach ($programids as $pid) {
            try {
                // 1) Riallinea struttura/consistenza del Program (plugin API).
                $top = \enrol_programs\local\program::load_content((int)$pid);
                $top->autorepair();

                // 2) Invalidazione cache corso/i (il corso cambiato è in $data->courseid).
                if (!empty($data->courseid)) {
                    rebuild_course_cache((int)$data->courseid, true);
                }

                // 3) (Facoltativo) Recompute progress/completion degli utenti allocati.
                //    Se il plugin espone API ufficiali per il ricalcolo, usale qui.
                //    Esempio (pseudo):
                // $userids = $DB->get_fieldset_select('enrol_programs_allocations','userid','programid=?',[$pid]);
                // foreach ($userids as $uid) {
                //     self::recompute_program_progress_for_user($pid, $uid);
                // }

            } catch (\Throwable $e) {
                mtrace('[local_wsvecomp] recompute_programs_task pid='.$pid.' error: '.$e->getMessage());
            }
        }
    }

    // Esempio di stub: valuta completion dei corsi foglia e aggiorna stato Program.
    // COMPLETARE SOLO se definisci dove scrivere i risultati (API/tabelle plugin).
    protected static function recompute_program_progress_for_user(int $programid, int $userid): void {
        // 1) Carica top e tree, ricava foglie corso + regole set (allinorder, atleast, ...).
        // 2) Per ogni corso foglia: usa completion_info($course)->is_course_complete($user).
        // 3) Applica la regola del set per derivare stato Program e progress%.
        // 4) Aggiorna tabelle/ API del plugin, se disponibili.
    }
}?>
```

Nota: il punto (3) è quello “variabile”: se il plugin enrol_programs ha un metodo ufficiale per aggiornare il completion/progress (es. su allocation o program), lo chiami qui. In mancanza, puoi:

	- calcolare dinamicamente il progress% dai completion di corso (foglie) e non salvare, ma solo invalidare cache → la UI lo ricalcola al volo;
 	- oppure introdurre una tua tabella cache (es. local_wsvecomp_progprogress) e popolarla, senza toccare le tabelle del plugin.


# Integrazione con la convenzione “sblocco in ordine”

Se nel corso cambiano i moduli e applichi la regola “ogni modulo dipende dal precedente”, a valle dell’evento:

	- ricostruendo l’albero del Program via autorepair() ottieni coerenza delle prerequisiti lato Program;
 	- i progress del Program si riallineano quando (a) il completion del corso cambia e (b) la UI ricalcola (oppure lo forzi nel task).

