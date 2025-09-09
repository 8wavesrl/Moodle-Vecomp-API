
# move_activity_between_courses

**Funzione:** `local_wsvecomp_move_activity_between_courses`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_move_activity_between_courses`  
**Permessi:** corso A `moodle/backup:backupactivity`, `moodle/course:manageactivities` – corso B `moodle/restore:restoreactivity`, `moodle/course:manageactivities`

## Descrizione
Sposta o copia una singola attività tra corsi tramite backup/restore; copia i completion dell’attività; può riposizionare nella sezione/indice; opzionalmente azzera le availability e ricalcola i completion di corso.

## Request
**Headers**: vedi [_partials/auth.md](../auth.md)

**Body JSON**
```json
{
  "sourcecmid": 123,
  "targetcourseid": 20,
  "targetsection": 1,
  "targetindex": 0,
  "resetavailability": true,
  "recompute": true,
  "domove": true
}
```

## Response
```json
{
  "oldcmid": 123,
  "newcmid": 456,
  "sourcecourseid": 10,
  "targetcourseid": 20,
  "moved": true,
  "migratedusers": 87,
  "recomputed": true,
  "availabilityreset": true
}
```

## Note
- `resetavailability=true`: la disponibilità viene azzerata, quindi il modulo copiato/spostato in B è subito accessibile e completabile da tutti gli utenti.
- `resetavailability=false`: la disponibilità viene ricostruita in base all’ordine dei moduli nella sezione; ogni attività è bloccata finché la precedente non viene completata (catena di completamento).
- `recompute=true` aggiorna i completion e può **revocare** quelli di corso in B se manca il nuovo CM.
- Cache: invalidazione `coursemodinfo` e rebuild del corso A/B.

## Spostamento vs Copia (`domove`)

Il parametro `domove` controlla il comportamento dell’endpoint **move_activity_between_courses**:

- **`domove = true` (SPOSTA)**  
  - Backup/restore in B **e** cancellazione dell’attività in A.  
  - **Pro:** niente duplicati, struttura dei corsi pulita, progress/completion allineati alla nuova realtà.  
  - **Contro:** gli utenti di A perdono l’accesso a quel CM; eventuali riferimenti/log al vecchio `cmid` restano orfani.

- **`domove = false` (COPIA)**  
  - Backup/restore in B, l’attività **rimane** anche in A.  
  - **Pro:** più sicuro; non tocchi A; utile per riuso del materiale.  
  - **Contro:** possibili duplicati; nessuna sincronizzazione “live” dei completion tra le due copie.

> Suggerimento: per test non distruttivi usa `domove=false`; quando sei sicuro, rilancia con `domove=true`.

---
## TODO
- Gestione automatica dei completion nei `enrol_programs` quando le attività dei corsi inclusi in un Program vengono spostate/copiate/eliminate.
- Gestione notifiche utente.