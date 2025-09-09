# local_wsvecomp_program_set_structure

Imposta la struttura semplice del Program come **lista ordinata di corsi** sotto il nodo TOP.

## Parametri
- `programid` *(int)*
- `courses[]` *(int)* — lista di ID corso
- `completiontype` *(string)* — allinanyorder | allinorder | atleast (default allinanyorder)
- `minprerequisites` *(int)* — usato solo con completiontype=atleast

## Esempio
```json
{
  "programid": 42,
  "courses": [123,124,125],
  "completiontype": "allinorder"
}
```

## Response
```json
{
  "programid": 42,
  "tree": { "rootid": 987, "nodes": [...], "edges": [...] },
  "courses": [
    { "id": 123, "fullname": "Corso 1" },
    { "id": 124, "fullname": "Corso 2" }
  ]
}
```

## Note
- `allinanyorder`: corsi indipendenti, previtemid null, min = numero figli
- `allinorder`: catena lineare previtemid, min = numero figli
- `atleast`: min impostato a X (clampato a 1..numero figli)

## TODO
- Gestione automatica dei completion nei `enrol_programs` quando le attività dei corsi inclusi in un Program vengono spostate/copiate/eliminate.
- Gestione notifiche utente.