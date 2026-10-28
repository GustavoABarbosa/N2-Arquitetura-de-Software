# Shared kernel

Tipos e primitivos compartilhados entre bounded contexts, sem regras de um contexto específico:

- `Result` / erros de domínio (`DomainError`)
- base de `DomainEvent` (`type`, `occurredAt`, `payload`)
- identificadores comuns, se necessário

Os contexts **não** devem colocar aqui regras de Questão, Prova ou Correção.
