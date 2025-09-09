# enrol_programs_source_manual_allocate_users

**Componente:** `enrol_programs`  
**File:** `classes/external/source_manual_allocate_users.php`  
**Descrizione:** alloca (in massa) utenti ad un Program tramite la **sorgente manuale**.

## Endpoint

Con protocollo **RESTful** (plugin `webservice_restful`):

```http
POST /webservice/restful/server.php/enrol_programs_source_manual_allocate_users
```

**Headers**
- `Authorization: Bearer <TOKEN>`
- `Content-Type: application/json`
- `Accept: application/json`

---

## Permessi richiesti

- Capability di gestione dei Program **(es. `enrol/programs:allocate` / ruolo con privilegi di Program manager)**.
- L’utente del token deve avere accesso in scrittura al Program target.

---

## Request

**Body JSON (tipico)**

```json
{
  "programid": 123,
  "userids": [11, 12, 13]
}
```

**Campi**
- `programid` *(int, richiesto)* – ID del Program.
- `userids` *(int[], richiesto)* – elenco degli utenti da allocare.
---

## Response

**Success (tipico)**

```json
{
  "programid": 123,
  "allocated": [11, 12, 13],
  "skipped": [],
  "warnings": []
}
```

**Errori (tipici)**
- `invalid_parameter_exception` – parametri mancanti o non validi.
- `required_capability_exception` / `webservice_access_exception` – permessi insufficienti.
- `not_found` – Program inesistente o utenti non trovati.
- `conflict` – utente già allocato.

---

## Note operative

- Se un utente è già allocato al Program, la chiamata lo riporterà in `skipped` o come warning.
- In ambienti multi-tenant o con sorgenti miste (cohort/dynamic/approval), questo metodo registra la **sorgente “manual”**.

---

## Troubleshooting

- **403 / access denied** – token senza capability di allocazione.
- **400 / invalid parameters** – `programid` non valido o `userids` vuoto.
