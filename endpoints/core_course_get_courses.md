# core_course_get_courses

**Funzione:** `core_course_get_courses`  
**Rotta:** `POST /webservice/restful/server.php/core_course_get_courses`  
**Permessi:** Nessuno per corsi visibili; `moodle/course:viewhiddencourses` per corsi nascosti.

## Descrizione
Restituisce informazioni sintetiche sui corsi specificati o su tutti i corsi.

## Request
**Body JSON**
```json
{
  "options": {
    "ids": [42, 84]
  }
}
```
> Se `options.ids` è omesso, vengono restituiti tutti i corsi visibili per l’utente.

## Response
```json
[
  {
    "id": 42,
    "shortname": "PM101",
    "fullname": "Project Management 101",
    "categoryid": 3,
    "visible": 1,
    "startdate": 1733097600,
    "enddate": 1738296000,
    "summary": "Corso introduttivo"
  }
]
```

## Note
- I campi restituiti possono includere ulteriori metadati (idnumber, lang, format, ecc.).
