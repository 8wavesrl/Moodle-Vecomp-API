# core_course_get_categories

**Funzione:** `core_course_get_categories`  
**Rotta:** `POST /webservice/restful/server.php/core_course_get_categories`  
**Permessi:** Nessuno per categorie visibili; `moodle/category:manage` per vedere categorie nascoste.

## Descrizione
Restituisce l’elenco delle categorie che soddisfano filtri opzionali.

## Request
**Body JSON**
```json
{
  "criteria": [
    { "key": "name", "value": "Formazione" },
    { "key": "parent", "value": "0" }
  ],
  "addsubcategories": 1
}
```

## Response
```json
[
  {
    "id": 3,
    "name": "Formazione",
    "idnumber": "CAT-FRM",
    "description": "",
    "parent": 0,
    "visible": 1,
    "depth": 1,
    "timemodified": 1720000000
  }
]
```

## Note
- Chiavi comuni nei filtri: `id`, `name`, `idnumber`, `parent`, `visible`.
