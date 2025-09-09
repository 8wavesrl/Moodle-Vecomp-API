# core_user_update_users

**Funzione:** `core_user_update_users`  
**Rotta:** `POST /webservice/restful/server.php/core_user_update_users`  
**Permessi:** `moodle/user:update`.

## Descrizione
Aggiorna i dati di uno o più utenti.

## Request
**Body JSON**
```json
{
  "users": [
    {
      "id": 11,
      "firstname": "Luca",
      "lastname": "Verdi",
      "email": "luca.verdi@example.com",
      "city": "Milano",
      "country": "IT"
    }
  ]
}
```

## Response
```json
{
  "status": "ok",
  "updated": [11]
}
```

## Note
- Può aggiornare anche customfields e preferences.
