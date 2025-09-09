# core_course_get_course_module

**Funzione:** `core_course_get_course_module`  
**Rotta:** `POST /webservice/restful/server.php/core_course_get_course_module`  
**Permessi:** Accesso al corso (iscrizione o `moodle/course:view`).

## Descrizione
Restituisce informazioni dettagliate su un singolo course module (`cmid`).

## Request
**Body JSON**
```json
{
  "cmid": 789
}
```

## Response
```json
{
  "id": 789,
  "course": 42,
  "modulename": "assign",
  "instance": 123,
  "sectionnum": 1,
  "visible": 1,
  "uservisible": true,
  "name": "Compito 1",
  "url": "https://.../mod/assign/view.php?id=789"
}
```

## Note
- I campi restituiti dipendono dal modulo e dalle capability utente.
