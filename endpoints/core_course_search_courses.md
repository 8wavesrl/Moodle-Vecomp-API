# core_course_search_courses

**Funzione:** `core_course_search_courses`  
**Rotta:** `POST /webservice/restful/server.php/core_course_search_courses`  
**Permessi:** Nessuno per corsi visibili; `moodle/course:viewhiddencourses` per corsi nascosti.

## Descrizione
Effettua una ricerca testuale nei corsi del sito.

## Request
**Body JSON**
```json
{
  "criterianame": "search",
  "criteriavalue": "Project Management",
  "page": 0,
  "perpage": 10
}
```

## Response
```json
{
  "total": 1,
  "courses": [
    {
      "id": 42,
      "shortname": "PM101",
      "fullname": "Project Management 101",
      "summary": "Corso introduttivo",
      "categoryid": 3
    }
  ]
}
```

## Note
- Supporta anche criteri come `blocklist`, `modulelist`, `tagid` a seconda della versione.
