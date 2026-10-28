# Contexto: Relatórios

**Conceitos:** `ApplicationReport`, `ConsolidatedReport`, `ProfessorSummary`  
**Casos de uso:** ApplicationReport, ConsolidatedReport, DashboardSummary  

| Camada | Papel |
|--------|--------|
| `domain/` | Estatísticas (média, mediana, desvio, distribuição) |
| `application/` | Consultas de relatório (somente leitura) |
| `ports/` | `ReportQuery` (pode ler dados dos contextos Applications/Grading) |
| `adapters/in/http/` | ReportsController |
| `adapters/out/persistence/` | Queries / projeções de relatório |
