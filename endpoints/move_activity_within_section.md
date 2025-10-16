
# local_wsvecomp_move_activity_within_section

**Funzione:** `local_wsvecomp_move_activity_within_section`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_move_activity_within_section`  
**Permessi:** `moodle/course:manageactivities`

## Descrizione
Sposta/riordina un’attività nello stesso corso (o in un’altra sezione dello stesso corso) **senza** backup/restore. In automatico le availability tra attività vengono resettate secondo la convenzione **tutte nell'ordine**

## Request
**Body JSON**
```json
{
  "cmid": 456,
  "targetsection": 1,
  "targetindex": 2
}
```

## Response
```json
{
  "status": "success",
  "message": "Module repositioned",
  "courseid": 20,
  "sectionid": 345,
  "sectionnumber": 1,
  "index": 2
}
```

## TODO
- Gestione notifiche utente.