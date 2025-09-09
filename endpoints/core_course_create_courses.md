# core_course_create_courses

**Funzione:** `core_course_create_courses`  
**Rotta:** `POST /webservice/restful/server.php/core_course_create_courses`  
**Permessi:** `moodle/course:create` (nella categoria di destinazione), eventuali capability sui campi avanzati.

## Descrizione
Crea uno o più corsi nelle categorie specificate.

## Request
**Body JSON**
```json
{
  "courses": [
    {
      "fullname": "Project Management 101",
      "shortname": "PM101",
      "categoryid": 3,
      "visible": 1,
      "startdate": 1733097600,
      "enddate": 1738296000,
      "summary": "Corso introduttivo",
      "format": "topics",
      "numsections": 5,
      "idnumber": "PM-101",
      "lang": "it",
      "courseformatoptions": [
        { "name": "hiddensections", "value": 0 },
        { "name": "coursedisplay", "value": 0 }
      ]
    }
  ]
}
```

## Response
```json
[
  { "id": 42, "shortname": "PM101" }
]
```

## Note
- `shortname` deve essere **unico** nel sito.
- `categoryid` deve esistere e l’utente deve poter creare corsi in quella categoria.
- Le opzioni disponibili in `courseformatoptions` dipendono dal formato corso attivo.

## TODO
- Validazioni lato servizio per collisioni su `shortname`/`idnumber`.
