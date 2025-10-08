# local_wsvecomp_get_user_progress

**Descrizione**: Restituisce i progressi di un utente partendo dall'id.

## Request
```json
{
    "userid": 2
}
```

## Response
```json
{
    "courses": [
        {
            "courseid": "282",
            "totalSectionsNumber": 1,
            "completedSections": 0,
            "totalPercentage": 0,
            "sectionsCompletionPercentage": [
                {
                    "sectionid": 1401,
                    "percentage": 0
                }
            ],
            "nextActivityIds": [
                4055,
                4056
            ]
        }
    ],
    "linked": null,
    "completed_courses_number": 0,
    "completed_courses_percentage": 0
}
```
