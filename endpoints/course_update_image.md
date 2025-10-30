# local_wsvecomp_course_update_image

**Funzione:** `local_wsvecomp_course_update_image`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_course_update_image`  
**Permessi:** `moodle/course:update`

## Descrizione
Permette di impostare l'immagine in evidenza di un corso. Va caricata la stringa base64 dell'immagine.
Al termine del caricamente svuota automaticamente la cache del corso per rendere l'immagine visibile fin da subito.

---

## Parametri

Il body deve contenere l’oggetto `data` che conterrà i parametri `courseid` e `courseimage`

- **courseid** (int)
- **courseimage** (string, base64 image)

---

## Request

```json
{
    "data": {
        {
            "couseid": 1,
            "couseimage": "data:image/jpeg;base64,/9j/7AARRHVja3kAAQAEAAAABgAA/+4ADkFkb2J.....",
        }
    }
}
```
---

## Response

In caso di successo:

```json
[
    {
        "status": true,
        "filename": "courseimage_35_1761830756.jpg",
        "mimetype": "image/jpeg",
        "filesize": 201458
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
