
# add_vimeoactivity_to_course

**Funzione:** `local_wsvecomp_add_vimeoactivity_to_course`  
**Rotta:** `POST /webservice/restful/server.php/local_wsvecomp_add_vimeoactivity_to_course`  
**Permessi:** `moodle/course:manageactivities`

## Descrizione
Crea una **nuova** attività `vimeoactivity` nel corso, la posiziona nella sezione/indice, opzionalmente azzera le availability e ricalcola i completion.
Il campo video fa riferimento all'id Vimeo del Video.

## Request
**Body JSON**
```json
{
  "courseid": 20,
  "targetsection": 0,
  "targetindex": null,
  "name": "Titolo video",
  "video": "123456",
  "color": "",
  "intro": "",
  "introformat": 1,
  "autoplay": 0,
  "autoloop": 0,
  "popupopen": 0,
  "popupwidth": 640,
  "popupheight": 360,
  "completionenable": 1,
  "completionprogress": 100,
  "visible": 1,
  "resetavailability": true,
  "recompute": true
}
```

## Response
```json
{
  "courseid": 20,
  "newcmid": 678,
  "section": 0,
  "availabilityreset": true,
  "recomputed": true
}
```

## Note
- Mappato ai campi `mdl_vimeoactivity` (video, color, intro, introformat, autoplay, autoloop, popupopen, popupwidth, popupheight, completionenable, completionprogress, visible).
- Se `completionenable=1` e `completionprogress>0`, imposta **core completion** del CM a “on view” (`completion=2`).
- Cache: rebuild e invalidazione `coursemodinfo` del corso.

## TODO
- Gestione automatica dei completion nei `enrol_programs` quando le attività dei corsi inclusi in un Program vengono spostate/copiate/eliminate.
- Gestione notifiche utente.