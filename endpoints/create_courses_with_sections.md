# local_wsvecomp_create_courses_with_sections

**Funzione:** `local_wsvecomp_create_courses_with_sections`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_create_courses_with_sections`  
**Permessi:** `moodle/course:create`

## Descrizione
Questa API estende la core di creazione corsi di Moodle.
Oltre a creare il corso, rinomina la prima sezione creata in automatico con lo shortname del corso appena creato.
Inoltre nel corpo della risposta ci saranno anche i dettagli della sezione stessa.

---

## Parametri

Il body deve contenere l’oggetto `courses`, un array di corsi.

- **fullname** (string)
- **shortname** (string)
- **categoryid** (int)
- **summaryformat** (int, 1)
- **format** (string, 'topics')

---

## Request

```json
{
    "courese": [
        {
            "fullname": "CORSO CENTORDICI",
            "shortname": "SHORT-REST-NAME",
            "categoryid": 1,
            "summaryformat": 1,
            "format": "topics"
        }
    ]
}
```
---

## Response

In caso di successo:

```json
[
    {
        "id": 291,
        "shortname": "SHORT-REST-NAME",
        "sections": [
            {
                "sectionid": 1413,
                "sectionnumber": 0,
                "name": "SHORT-REST-NAME"
            }
        ]
    }
]
```

---

## Errori comuni

- **401/403** – token assente o non valido, funzione non inclusa nel servizio.  
- **400** – body non valido, `Content-Type` errato.  
- **404** – endpoint errato (controllare il path).  
- **invalid_parameter_exception** – struttura o parametri mancanti/errati.  

---