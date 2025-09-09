# core_user_delete_users

**Funzione:** `core_user_delete_users`  
**Rotta:** `POST /webservice/restful/server.php/core_user_delete_users`  
**Permessi:** `moodle/user:delete`.

## Descrizione
Elimina definitivamente uno o più utenti dal sito.

## Request
**Body JSON**
```json
{
  "userids": [11, 12]
}
```

## Response
```json
{
  "status": "ok",
  "deleted": [11, 12]
}
```

## Note
- L’eliminazione rimuove iscrizioni, preferenze, completion e dati collegati.
- Azione irreversibile.
