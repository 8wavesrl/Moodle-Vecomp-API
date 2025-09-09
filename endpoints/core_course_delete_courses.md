# core_course_delete_courses

**Funzione:** `core_course_delete_courses`  
**Rotta:** `POST /webservice/restful/server.php/core_course_delete_courses`  
**Permessi:** `moodle/course:delete` (sui corsi indicati).

## Descrizione
Elimina definitivamente uno o più corsi dal sito.

## Request
**Body JSON**
```json
{
  "courseids": [21, 22, 23]
}
```

## Response
```json
{
  "status": "ok",
  "deleted": [21, 22, 23]
}
```

## Note
- L’eliminazione rimuove anche attività, iscrizioni, completion e dati collegati.
- Azione irreversibile (a meno di backup/restore).
