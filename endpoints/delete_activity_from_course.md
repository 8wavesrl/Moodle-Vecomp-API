
# delete_activity_from_course

**Funzione:** `local_wsvecomp_delete_activity_from_course`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_delete_activity_from_course`  
**Permessi:** `moodle/course:manageactivities`

## Descrizione
Elimina un `course module` e (opzionalmente) ricalcola i completion per gli iscritti al corso.

## Request
**Body JSON**
```json
{
  "cmid": 456,
  "recompute": true
}
```

## Response
```json
{
  "courseid": 20,
  "deletedcmid": 456,
  "recomputed": true,
  "touched": 57
}
```

## Note
- Dopo la cancellazione, invalida `coursemodinfo` e ricostruisce la cache del corso.
- Con `recompute=true` invoca l’API core per aggiornare lo stato di completamento di corso.

## TODO
- Gestione automatica dei completion nei `enrol_programs` quando le attività dei corsi inclusi in un Program vengono spostate/copiate/eliminate.
- Gestione notifiche utente.