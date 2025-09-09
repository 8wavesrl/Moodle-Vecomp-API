# core_course_update_categories

**Funzione:** `core_course_update_categories`  
**Rotta:** `POST /webservice/restful/server.php/core_course_update_categories`  
**Permessi:** `moodle/category:manage`.

## Descrizione
Aggiorna nome, descrizione o parent di una o più categorie.

## Request
**Body JSON**
```json
{
  "categories": [
    {
      "id": 7,
      "name": "Nuovo nome categoria",
      "parent": 0,
      "idnumber": "CAT-NEW"
    }
  ]
}
```

## Response
```json
{
  "status": "ok",
  "updated": [7]
}
```

## Note
- È possibile aggiornare anche il campo `visible`.
