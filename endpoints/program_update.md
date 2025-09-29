# local_wsvecomp_program_create

Aggionra un Program (simple)

## Parametri
- `programid` *(int, richiesto)* — es. system o coursecat
- `fullname` *(string, richiesto)* — nome del programma
- `descriptio ` *(string, opzionale)* — descrizione del programma
- `idnumber` *(string, opzionale, univoco)* — identificativo univoco
- `public` *(bool, opzionale)* — default false

## Esempio
```json
{
    "programid": 220,
    "fullname": "Academy 2025",
    "idnumber": "PRG-2025",
    "public": true,
    "description": "Lorem ipsum.."
}
```

## Response
```json
{
    "programid": 220,
    "fullname": "Academy 2025",
    "idnumber": "PRG-2025",
    "public": true,
    "description": "Lorem ipsum.."
}
```

## Note
Valutare se serve estendere ad altri campi di modifica.