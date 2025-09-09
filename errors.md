
# Gestione errori

Gli errori sono restituiti in JSON (campi tipici: `exception`, `errorcode`, `message`).

Esempio:
```json
{
  "exception": "moodle_exception",
  "errorcode": "restore_precheck_failed",
  "message": "Plugin mancante: mod_hvp; [WARN] ..."
}
```

Errori comuni per gli endpoint di spostamento:
- `backup_unsupported_module` — modulo sorgente senza supporto backup/restore.
- `restore_precheck_failed` — dipendenze/permessi mancanti.
- `restore_mapping_failed` — impossibile dedurre il nuovo `cmid`.
- `setting_locked_by_permission` — alcune setting di backup/restore sono bloccate: il WS usa fallback.
