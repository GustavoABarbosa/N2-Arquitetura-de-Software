# Contexto: Turmas e Matrículas

**Aggregates:** `Class`, `ClassEnrollment`  
**Casos de uso:** Create, Update, Archive, Enroll, RemoveStudent, RegenerateInviteCode, JoinByCode  

| Camada | Papel |
|--------|--------|
| `domain/` | Status ativa/arquivada, código de convite, matrícula |
| `application/` | Casos de uso de turma e matrícula |
| `ports/` | `ClassRepository`, `EnrollmentRepository` |
| `adapters/in/http/` | ClassesController, JoinController |
| `adapters/out/persistence/` | Persistência de turmas e matrículas |
