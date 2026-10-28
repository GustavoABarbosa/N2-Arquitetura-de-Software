# Contexto: Identidade e Acesso

**Aggregates:** `User`, `RefreshToken`  
**Casos de uso:** Register, Login, Refresh, Logout, LogoutAll, Anonymize (LGPD), Me  

| Camada | Papel |
|--------|--------|
| `domain/` | Regras de senha, anonimização, validade de token |
| `application/` | Casos de uso de autenticação |
| `ports/` | `UserRepository`, `TokenStore`, `PasswordHasher` |
| `adapters/in/http/` | AuthController |
| `adapters/out/persistence/` | Persistência de usuários e refresh tokens |
