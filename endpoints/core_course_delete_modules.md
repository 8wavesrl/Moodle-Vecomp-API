# core_course_delete_modules

**Funzione:** `core_course_delete_modules`  
**Rotta:** `POST /webservice/restful/server.php/core_course_delete_modules`  
**Permessi:** `moodle/course:manageactivities` (nel corso).

## Descrizione
Elimina uno o più *course module* (attività/risorse) identificati dai rispettivi `cmid`.

## Request
**Body JSON**
```json
{
  "cmids": [456, 789],
  "recyclebin": 0
}
```
- `recyclebin` (0/1): se attivo e supportato, sposta nel cestino corso.

## Response
```json
{
  "status": "ok",
  "deletedcmids": [456, 789]
}
```

## Note
- Dopo la cancellazione è consigliato invalidare `coursemodinfo` e ricostruire la cache del corso.
- Se l’istanza appartiene a un Program (plugin `enrol_programs`), valutare impatti su completion/allocazioni.
