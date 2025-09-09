# local_wsvecomp_program_list

**Descrizione**: Elenco programmi con filtri, ordinamento e paginazione. Con parametro opzionale `with_tree`.

## Request
```json
{
  "search": "lorem",
  "page": 0,
  "perpage": 25,
  "sort": "timecreated",
  "dir": "DESC",
  "with_tree": true
}
```

## Response
```json
{
  "total": 3,
  "items": [
    {
      "id": 42,
      "fullname": "Programma Demo",
      "tree": { "rootid": 987, "nodes": [...], "edges": [...] },
      "courses": [ { "id": 12, "fullname": "Course A" } ]
    }
  ]
}
```
