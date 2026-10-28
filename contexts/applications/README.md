# Contexto: Aplicação e Versões

**Aggregates:** `Application`, `ExamVersion`  
**Casos de uso:** CreateApplication, RequestPdfGeneration, PublishAnswerKey, ListVersions, GetPublicAnswerKey  

| Camada | Papel |
|--------|--------|
| `domain/` | Versões 1–10, regras de regeneração, gabarito público, eventos |
| `application/` | Casos de uso de aplicação/PDF/gabarito |
| `ports/` | `ApplicationRepository`, `PdfGenerator`, `EventPublisher` |
| `adapters/in/http/` | ApplicationsController |
| `adapters/in/messaging/` | Consumers de resultados assíncronos (ex.: `PdfGenerated`) |
| `adapters/out/persistence/` | Persistência de aplicações e versões |
| `adapters/out/messaging/` | Publisher de eventos/comandos |
| `adapters/out/pdf/` | Adaptador do gerador de PDF |
