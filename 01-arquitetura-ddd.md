# Questão 1 — Arquitetura DDD / Hexagonal (SGP)

**Pontuação da rubrica:** 3,0  
**Diagramas visuais:** elaborados no **draw.io** (padrão da disciplina) e incluídos apenas no **PDF** da atividade Teams — este repositório não contém diagramas gerados automaticamente.

---

## Objetivo

Transformar a arquitetura/domínio do projeto Web SGP em uma **organização orientada a Domain-Driven Design** com estilo **hexagonal (ports & adapters)**. Este repositório documenta e materializa essa organização em pastas; **não** inclui o código-fonte Vue do `sgp-web`.

## Princípios adotados

1. **Modelo rico no domínio** — regras de negócio (limites de 20 questões, 1–10 versões, ownership do professor, turma arquivada imutável) ficam em entidades/aggregates e serviços de domínio, não em controllers ou UI.
2. **Um bounded context por capacidade de negócio** — evita o “backend monolítico de funções” do mock atual (`backend.ts`).
3. **Dependências apontam para dentro** — Application e Adapters dependem de **portas** (interfaces); o Domain não conhece HTTP, localStorage, filas nem Vue.
4. **Eventos de domínio** — mudanças relevantes (`PdfGenerated`, `AnswerKeyPublished`, `CorrectionConfirmed`, `GradeAssigned`) são fatos do domínio, publicáveis por adaptador de saída.

## Mapa de bounded contexts

| Contexto | Pasta | Aggregate roots / conceitos | Responsabilidade |
|----------|-------|----------------------------|------------------|
| Identidade e Acesso | [`contexts/identity`](contexts/identity) | `User`, `RefreshToken` | Cadastro, login, refresh, logout, anonimização LGPD |
| Banco de Questões | [`contexts/questions`](contexts/questions) | `Question` | CRUD, tags, soft-delete, regras objetiva/discursiva |
| Turmas e Matrículas | [`contexts/classes`](contexts/classes) | `Class`, `ClassEnrollment` | Turma ativa/arquivada, convite, matrícula/remoção |
| Montagem de Provas | [`contexts/exams`](contexts/exams) | `Exam` | Builder até 20 questões, status draft/ready/closed |
| Aplicação e Versões | [`contexts/applications`](contexts/applications) | `Application`, `ExamVersion` | Aplicar prova à turma, PDF, versões, gabarito público |
| Correção e Notas | [`contexts/grading`](contexts/grading) | `Correction`, `ExamAssignment` | Persistência de correção, atribuição a aluno, sync |
| Relatórios | [`contexts/reports`](contexts/reports) | `ApplicationReport` | Estatísticas e consolidação (leitura do domínio de notas) |

Kernel compartilhado: [`shared/kernel`](shared/kernel) (`Result`, `DomainError`, `DomainEvent`).

## Organização de pastas (este repositório)

Cada contexto segue o mesmo hexágono:

```
n2-arquitetura/
  contexts/
    <contexto>/
      domain/                 # entidades, VOs, regras, eventos de domínio
      application/            # casos de uso
      ports/                  # contratos (in/out)
      adapters/
        in/http/              # controllers REST
        in/messaging/         # consumers (quando aplicável)
        out/persistence/      # repositórios concretos
        out/messaging/        # publisher (quando aplicável)
        out/pdf/              # gerador de PDF (applications)
  shared/
    kernel/
  00-dominio.md
  01-arquitetura-ddd.md
```

As pastas existem neste repositório (marcadas com `.gitkeep` onde ainda não há código — a Q1 pede **organização**, não implementação).

## Hexágono — exemplo: contexto Aplicação e Versões

Fluxo (descrição alinhada ao diagrama draw.io do PDF):

1. **Adapters de entrada** — REST Controllers e, quando aplicável, Message Consumers.
2. **Application** — casos de uso (`CreateApplication`, `RequestPdfGeneration`, `PublishAnswerKey`) orquestram o domínio via portas.
3. **Domain** — aggregate `Application` e eventos de domínio (`PdfGenerated`, `AnswerKeyPublished`, …).
4. **Ports de saída** — `ApplicationRepository`, `PdfGenerator`, `EventPublisher`.
5. **Adapters de saída** — PostgreSQL, serviço de PDF, message broker.

Dependências: entrada → application → domain; application → ports de saída → adapters concretos. O domain **não** depende de infraestrutura.

### Portas (contratos) — exemplo

| Porta | Direção | Exemplos de métodos |
|-------|---------|---------------------|
| `CreateApplicationPort` | in | `execute({ examId, classId, teacherId })` |
| `ApplicationRepository` | out | `save`, `findByIdOwnedBy`, `listByTeacher` |
| `PdfGenerator` | out | `generate(application, versionConfigs)` |
| `EventPublisher` | out | `publish(PdfGenerated ou AnswerKeyPublished)` |

### Regras que permanecem no Domain

- Aplicação só sobre prova não arquivada e turma ativa do mesmo professor.
- Entre 1 e 10 versões por geração de PDF.
- Regeneração bloqueada se já existem correções sincronizadas.
- Gabarito público só após `answerKeyPublished = true`.

## Relação com o frontend atual

O `sgp-web` continua como **adaptador de UI** (Vue + Pinia + `src/api/*`). Na arquitetura alvo, esses módulos HTTP (`questionsApi`, `applicationsApi`, …) falam com controllers dos contextos; o mock MSW (`mock/backend.ts`) é substituído, no longo prazo, pela API hexagonal — sem misturar regras de PDF, auth e relatórios no mesmo arquivo.

## Por que esta organização atende a Q1

- Decompõe o domínio Web em **bounded contexts** nomeados na linguagem do produto.
- Expõe **hexágono** (`domain` / `application` / `ports` / `adapters`) por contexto, **visível neste repositório**.
- Documenta princípios DDD; o diagrama hexagonal oficial está no PDF (draw.io).
- **Não** exige o código-fonte do projeto web Vue.
