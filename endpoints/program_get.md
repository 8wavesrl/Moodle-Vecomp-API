# local_wsvecomp_program_get

**Descrizione**: Restituisce il dettaglio di un programma (metadati + struttura).

## Strutture disponibili
- `items`: albero annidato (se supportata `external_recursive_structure`)
- `itemsjson`: stringa JSON fallback
- `tree`: struttura compatta non ricorsiva (sempre disponibile)
- `courses`: lista piatta corsi

## Node shape (items/tree.nodes)
```json
{
  "id": 123,
  "type": "top|set|course",
  "fullname": "Titolo",
  "minprerequisites": 1,
  "previtemid": null,
  "course": { "id": 45, "fullname": "Course A", "shortname": "CA", "idnumber": "C-A" },
  "children": [ ... ]
}
```
