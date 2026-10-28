# Contexto: Montagem de Provas

**Aggregate:** `Exam` (+ `ExamQuestion`)  
**Casos de uso:** Create, Update, Archive, List, Get  

| Camada | Papel |
|--------|--------|
| `domain/` | Limite de 20 questões, ordem, pontuação, status draft/ready/closed |
| `application/` | Casos de uso do builder de prova |
| `ports/` | `ExamRepository` (consulta questões via porta do contexto Questions) |
| `adapters/in/http/` | ExamsController |
| `adapters/out/persistence/` | Persistência de provas |
