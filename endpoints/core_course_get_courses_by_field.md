# core_course_get_courses_by_field

**Funzione:** `core_course_get_courses_by_field`  
**Rotta:** `POST /webservice/restful/server.php/core_course_get_courses_by_field`  
**Permessi:** Nessuno per corsi visibili; `moodle/course:viewhiddencourses` per corsi nascosti.

## Descrizione
Recupera i corsi filtrando per un campo specifico (`id`, `shortname`, `idnumber`, `category`, ecc.).

## Request
**Body JSON**
```json
{
  "field": "shortname",
  "value": "PM101"
}
```

```json
{
  "field": "category",
  "value": 1
}
```

## Response
```json
{
  "courses": [
    {
      "id": 42,
      "shortname": "PM101",
      "fullname": "Project Management 101",
      "categoryid": 3
    }
  ]
}
```

## Note
- Se `field` è vuoto, restituisce tutti i corsi.
- Restituisce anche metadati di categoria.
