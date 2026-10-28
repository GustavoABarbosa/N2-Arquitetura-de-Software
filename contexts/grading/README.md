# Contexto: Correção e Notas

**Aggregates:** `Correction`, `ExamAssignment`  
**Casos de uso:** ListCorrections, AssignCorrection, IngestCorrection (idempotente por `clientCorrectionId`)  

| Camada | Papel |
|--------|--------|
| `domain/` | Resultados objetivos/discursivos, syncStatus, atribuição aluno |
| `application/` | Casos de uso de correção e lançamento de nota |
| `ports/` | `CorrectionRepository`, `EventPublisher` |
| `adapters/in/http/` | CorrectionsController |
| `adapters/in/messaging/` | `CorrectionConfirmedConsumer` |
| `adapters/out/persistence/` | Persistência de correções e atribuições |
