# core_courseformat_new_module

**Funzione:** `core_courseformat_new_module`  
**Rotta:** `POST /webservice/restful/server.php/core_courseformat_new_module`  
**Permessi:** `moodle/course:manageactivities` nel corso.

## Descrizione
Aggiunge un nuovo modulo (attività/risorsa) ad un corso in una sezione specifica.

## Request
**Body JSON**
```json
{
  "courseid": 42,
  "sectionnum": 1,
  "modulename": "assign",
  "name": "Compito 1",
  "visible": 1
}
```

## Response
```json
{
  "id": 789,
  "cmid": 789,
  "modulename": "assign",
  "sectionnum": 1
}
```

## Note
- `modulename` deve essere il nome interno del modulo (es. `assign`, `quiz`, `page`).
- Alcuni moduli richiedono parametri extra (impostazioni specifiche).
