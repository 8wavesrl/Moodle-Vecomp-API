# local_wsvecomp_program_fix_user_completion

Cerca di fixare eventuali disallineamenti tra i completamenti di attività, corsi e set all'interno di un dato programma per uno specifico utente. Ritorna un oggetto complesso con i dettagli di completamento, enrol e altre informazioni legate ai corsi presenti nel programma stesso.

## Parametri
- `programid` *(int)*
- `userid` *(int)*

## Esempio Body
```json
{
  "programid": 10,
  "userid": 1
}
```

## Response
```json
{
    "programid": 1,
    "userid": 1,
    "allocationid": 2,
    "allocationtimecompleted": 1761640535,
    "programcompleted": true,
    "programcompletionchanged": false,
    "coursechecks": [
        {
            "courseid": 1519,
            "exists": true,
            "trackedactivities": 5,
            "updatedactivities": 0,
            "coursecompletionid": 205,
            "coursecompleted": true,
            "coursecompletiontime": 1761640417,
            "userenrolled": true,
            "enrolstatus": "active",
            "enrolid": 9510,
            "userenrolmentid": 4116,
            "enroltimestart": 0,
            "enroltimeend": 0,
            "programitemid": 3542,
            "previtemid": 0,
            "programitemcompleted": true,
            "programitemcompletiontime": 1761640417,
            "previtemcompleted": true,
            "previtemcompletiontime": 0
        }
    ],
    "messages": []
}
```

