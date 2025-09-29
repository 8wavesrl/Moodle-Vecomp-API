# local_wsvecomp_program_set_structure_tree

Imposta la struttura **ad albero** del Program (set + corsi), passando l’intera definizione in JSON.

## Parametri
- `programid` *(int)*
- `rootjson` *(string JSON)* — radice con `sequencetype`, opzionale `minprerequisites`, `children[]`,
- `replace` *(bool)*

## Esempio Body
```json
{
  "programid": 42,
  "rootjson": "{\"sequencetype\":\"allinanyorder\",\"children\":[{\"type\":\"set\",\"fullname\":\"Set A\",\"sequencetype\":\"allinorder\",\"children\":[{\"type\":\"course\",\"courseid\":123},{\"type\":\"course\",\"courseid\":124}]}]}",
  "replace": true
}
```

## Esempio rootjson
```json
{
  "sequencetype": "allinorder",
  "children":[
        {
            "type": "set",
            "fullname": "Set A",
            "sequencetype": "allinorder",
            "children": [
                {
                    "type": "course",
                    "courseid": 123
                },
                {
                    "type": "course",
                    "courseid": 124
                }
            ]
        }
    ]
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
- `sequencetype`: allinanyorder | allinorder | atleast
- `minprerequisites` incluso solo se type=atleast
- `children[].type`: set | course
- `course` node richiede `courseid`
- `replace` è un booleano (default = false) che forza la sovrascrittura dell'attuale alberatura
- ID figli in `sequencejson` sono stringhe, come da UI nativa

## TODO
- Gestione automatica dei completion nei `enrol_programs` quando le attività dei corsi inclusi in un Program vengono spostate/copiate/eliminate.
- Gestione notifiche utente.