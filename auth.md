
# Autenticazione (RESTful)

Tutte le chiamate usano **Bearer Token** e **JSON**.

**Headers obbligatori**
- `Authorization: Bearer <TOKEN>`
- `Content-Type: application/json`
- `Accept: application/json`

**Endpoint base**
```
/webservice/restful/server.php
```

**Esempio cURL**
```bash
curl -X POST 'https://moodle.example/webservice/restful/server.php/<wsfunction>'   -H 'Authorization: Bearer <TOKEN>'   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{ ... }'
```
