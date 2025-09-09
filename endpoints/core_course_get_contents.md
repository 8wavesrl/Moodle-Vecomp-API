# core_course_get_contents

**Funzione:** `core_course_get_contents`  
**Rotta:** `POST /webservice/restful/server.php/core_course_get_contents`  
**Permessi:** Accesso al corso (iscrizione o `moodle/course:view`).

## Descrizione
Restituisce la struttura dei contenuti del corso (sezioni, moduli/attività, file).

## Request
**Body JSON**
```json
{
  "courseid": 42,
  "options": [
    { "name": "excludemodules", "value": 0 },
    { "name": "excludecontents", "value": 1 },
    { "name": "sectionnumber", "value": 0 }
  ]
}
```
- Imposta `excludecontents=0` per includere anche i file/URL delle attività.

## Response
```json
[
  {
    "id": 1,
    "name": "Introduzione",
    "summary": "",
    "modules": [
      {
        "id": 456,
        "url": "https://.../mod/page/view.php?id=456",
        "name": "Benvenuto",
        "modname": "page",
        "visible": 1,
        "uservisible": true
      }
    ]
  }
]
```

## Note
- I campi restituiti possono variare a seconda del formato corso e dei plugin attività.
