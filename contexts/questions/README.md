# Contexto: Banco de Questões

**Aggregate:** `Question` (objetiva | discursiva)  
**Casos de uso:** Create, Update, SoftDelete, List (filtros/paginação), Get, ListTags  

| Camada | Papel |
|--------|--------|
| `domain/` | Alternativas, pontuação mínima discursiva, ownership do professor |
| `application/` | Casos de uso de CRUD |
| `ports/` | `QuestionRepository` |
| `adapters/in/http/` | QuestionsController |
| `adapters/out/persistence/` | Persistência de questões |
