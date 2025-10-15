# local_wsvecomp_program_create

Crea un Program (metadati) ed eventualmente abilita le sorgenti di allocation.

## Parametri
- `contextid` *(int)* — es. system o coursecat
- `fullname` *(string)* — nome del programma
- `idnumber` *(string)* — identificativo univoco
- `description` *(string, opzionale)*
- `descriptionformat` *(int, opzionale)* — default HTML
- `public` *(bool, opzionale)* — default false
- `archived` *(bool, opzionale)*
- `creategroups` *(bool, opzionale)*
- `timeallocationstart`, `timeallocationend` *(timestamp, opzionali)*
- Scheduling “friendly”:
  - `programstart_type`: allocation|date|delay
  - `programstart_date` (se type=date)
  - `programstart_delay` (se type=delay, es. P1M, P10D)
  - `programdue_type`: notset|date|delay
  - `programdue_date`, `programdue_delay`
  - `programend_type`: notset|date|delay
  - `programend_date`, `programend_delay`
- `sources[]` *(array di stringhe, opzionale)* — elenco delle sorgenti di allocation da abilitare al volo. Valori supportati:
  - `manual`
  - `selfallocation`
  - `approval`
  - `cohort`
  - `udplans` (se presente)
- `imagebase64` (immagine codificata in base64)

## Esempio
```json
{
  "contextid": 1,
  "fullname": "Academy 2025",
  "idnumber": "PRG-2025",
  "public": true,
  "programstart_type": "date",
  "programstart_date": 1767225600,
  "sources": ["manual", "selfallocation"],
  "imagebase64": "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQ....."
}
```

## Response
```json
{
  "id": 42,
  "contextid": 1,
  "fullname": "Academy 2025",
  "idnumber": "PRG-2025",
  "public": true,
  "timecreated": 1765000000,
  "sources": ["manual","selfallocation"]
}
```

## Note
- Se non specifichi `sources`, nessuna sorgente viene abilitata in automatico.
- Una volta attivate, potrai usare direttamente i WS dedicati, es. `enrol_programs_source_manual_allocate_users` per allocare utenti via sorgente *manual*.
