# core_user_create_users

**Funzione:** `core_user_create_users`  
**Rotta:** `POST /webservice/restful/server.php/core_user_create_users`  
**Permessi:** `moodle/course:create`

## Descrizione
Questa API consente di creare uno o più utenti in Moodle.  
È una funzione core (`core_user_create_users`) esposta tramite i Web Services.

---

## Parametri

Il body deve contenere l’oggetto `users`, un array di utenti.  
Ogni utente può avere i seguenti campi (i **grassetti** sono obbligatori):

- **username** (string)  
- **firstname** (string)  
- **lastname** (string)  
- **email** (string)  
- password (string, opzionale – se omessa usare `createpassword`)  
- createpassword (int 0/1, opzionale)  
- auth (string, es. `manual`)  
- idnumber (string)  
- lang (string, es. `it`)  
- calendartype (string)  
- theme (string)  
- timezone (string)  
- mailformat (int)  
- description (string)  
- city (string)  
- country (string, es. `IT`)  
- firstnamephonetic, lastnamephonetic, middlename, alternatename (string)  
- preferences (array di `{ "type": "...", "value": "..." }`)  
- customfields (array di `{ "type": "...", "value": "..." }`)  

---

## Request

```json
{
  "users": [
    {
      "username": "m.rossi",
      "firstname": "Mario",
      "lastname": "Rossi",
      "email": "mario.rossi@example.com",
      "auth": "manual",
      "createpassword": 1,
      "city": "Roma",
      "country": "IT",
      "customfields": [
        { "type": "codicefiscale", "value": "RSSMRA80A01H501Z" }
      ],
      "preferences": [
        { "type": "mailformat", "value": "1" }
      ]
    }
  ]
}
```
---

## Response

In caso di successo:

```json
[
  { "id": 123, "username": "m.rossi" }
]
```

---

## Errori comuni

- **401/403** – token assente o non valido, funzione non inclusa nel servizio.  
- **400** – body non valido, `Content-Type` errato.  
- **404** – endpoint errato (controllare il path).  
- **invalid_parameter_exception** – struttura o parametri mancanti/errati.  

---

## Note

- La policy di username, e-mail e password dipende dalle impostazioni di sicurezza del sito.  
- Per vedere i parametri esatti supportati dalla tua installazione: *Amministrazione sito → Server → Web services → API documentation*.
