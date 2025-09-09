# core_course_update_courses

**Funzione:** `core_course_update_courses`  
**Rotta:** `POST /webservice/restful/server.php/core_course_update_courses`  
**Permessi:** `moodle/course:update`.

## Descrizione
Aggiorna i dati di uno o più corsi.

## Request
**Body JSON**
```json
{
  "courses": [
    {
      "id": 42,
      "fullname": "Project Management Avanzato",
      "shortname": "PM102",
      "categoryid": 4,
      "visible": 1
    }
  ]
}
```

## Response
```json
{
  "status": "ok",
  "updated": [42]
}
```

## Note
- Attenzione a collisioni di `shortname` o `idnumber`.
