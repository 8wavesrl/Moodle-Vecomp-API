# core_course_duplicate_course

**Funzione:** `core_course_duplicate_course`  
**Rotta:** `POST /webservice/restful/server.php/core_course_duplicate_course`  
**Permessi:** tipicamente `moodle/backup:backupcourse`, `moodle/restore:restorecourse` e `moodle/course:create` nella categoria di destinazione.

## Descrizione
Duplica un corso esistente in una categoria (stessa o diversa), con possibilità di rinominare `fullname`/`shortname` e impostare visibilità.

## Request
**Body JSON**
```json
{
  "courseid": 42,
  "fullname": "Project Management 101 - Copia",
  "shortname": "PM101_COPY",
  "categoryid": 5,
  "visible": 0,
  "options": [
    { "name": "activities", "value": 1 },
    { "name": "blocks", "value": 1 },
    { "name": "filters", "value": 1 },
    { "name": "users", "value": 0 }
  ]
}
```
- `options`: insieme di flag di backup/restore. I nomi supportati dipendono dalla versione.

## Response
```json
{
  "id": 84,
  "shortname": "PM101_COPY",
  "categoryid": 5
}
```

## Note
- Assicurarsi che `shortname` della copia sia unico.
- La duplicazione segue le regole del sottosistema backup/restore.
