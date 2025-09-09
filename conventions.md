
# Convenzioni

- **Formato**: JSON per request/response; RESTful con Bearer token.
- **Intestazioni**: `Content-Type: application/json`, `Accept: application/json`.
- **Nomenclatura**: parametri in lowerCamelCase.
- **Risposte**: preferire chiavi stabili (`status`, `message`, `data`, `errors[]` ove sensato).
- **Cache**: gli endpoint invalidano `coursemodinfo` e ricostruiscono cache corso se necessario.
