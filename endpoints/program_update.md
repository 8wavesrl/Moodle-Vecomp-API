# local_wsvecomp_program_create

Aggionra un Program (simple)

## Parametri
- `programid` *(int, richiesto)* — es. system o coursecat
- `fullname` *(string, richiesto)* — nome del programma
- `idnumber` *(string, opzionale)* — identificativo univoco
- `public` *(bool, opzionale)* — default false

## Esempio
```json
{
    "programid": 220,
    "fullname": "Academy 2025",
    "idnumber": "PRG-2025",
    "public": true
}
```

## Response
```json
{
    "programid": 220,
    "fullname": "Academy 2025",
    "idnumber": "PRG-2025",
    "public": true
}
```

## Note
Valutare se serve estendere ad altri campi di modifica.