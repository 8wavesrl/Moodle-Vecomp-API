# local_wsvecomp_trigger_welcome

Forza l'invio della notifica di benvenuto (email) agli utenti selezionati.

## Parametri
- `userids` *(array)* un array di id utente

## Esempio Body
```json
{
    "userids": [12,13,14]
}
```

## Response
```json
{
    "count": 3
}
```


## TODO
- Response un pò più strutturata