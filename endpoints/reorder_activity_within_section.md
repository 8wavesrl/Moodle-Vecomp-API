
# local_wsvecomp_reorder_activity_within_section

**Funzione:** `local_wsvecomp_reorder_activity_within_section`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_reorder_activity_within_section`  
**Permessi:** `moodle/course:manageactivities`

## Descrizione
Riordina le attività all'interno di una sezione di un corso. In automatico le availability tra attività vengono resettate secondo la convenzione **tutte nell'ordine**

## Request
**Body JSON**
```json
{
    "sectionid": 456,
    "cmids": [
        123,
        456,
        789
    ],
}
```

## Response
```json
{
    "courseid": 111,
    "sectionid": 456,
    "sequence": [
        123,
        456,
        789
    ],
    "changed": false,
    "availabilityupdated": true
}
```

## TODO
- Gestione notifiche utente.