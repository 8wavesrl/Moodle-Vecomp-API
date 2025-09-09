# core_course_delete_categories

**Funzione:** `core_course_delete_categories`  
**Rotta:** `POST /webservice/restful/server.php/core_course_delete_categories`  
**Permessi:** `moodle/category:delete` e/o `moodle/category:manage` (sulla/e categoria/e).

## Descrizione
Elimina una o più categorie. È possibile scegliere come trattare i contenuti (spostare i corsi o eliminarli).

## Request
**Body JSON**
```json
{
  "categories": [
    {
      "id": 7,
      "recursive": 1,
      "newparent": 0,
      "deletecourses": 0
    }
  ]
}
```
- `recursive`: elimina anche le sottocategorie (1/0).  
- `newparent`: se >0 sposta la/e categoria/e sotto un nuovo parent.  
- `deletecourses`: se 1 elimina i corsi contenuti, altrimenti tenta lo spostamento.

## Response
```json
{
  "status": "ok",
  "deleted": [7],
  "movedcourses": [12, 13]
}
```

## Note
- Verificare che `newparent` sia valido quando `deletecourses=0` e la categoria contiene corsi.
- L’operazione è distruttiva: valutare un backup preventivo.
