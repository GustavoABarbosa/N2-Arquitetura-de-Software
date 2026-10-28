# N2 — Questão 1: Arquitetura DDD (SGP Católica)

**Disciplina:** Projeto e Arquitetura de Software  
**Curso:** Engenharia de Software  
**Professor:** Luiz C. Camargo, PhD  
**Aluno:** Gustavo Ariel Barbosa  
**Sistema-base:** SGP Católica (projeto de Programação Web)  
**Data:** 29/10/2026  

---

## O que é este repositório?

Este repositório corresponde **apenas à Questão 1** da Avaliação N2:

> Utilize a arquitetura/domínio do projeto de programação Web e a transforme em uma arquitetura voltada para DDD. Espera-se que a organização desta arquitetura (não precisa ter código-fonte do projeto web) esteja acessível em um repositório do GitHub **(3,0)**.

Aqui está a **organização DDD / hexagonal** do domínio do **SGP Católica**: bounded contexts, camadas (`domain`, `application`, `ports`, `adapters`) e documentação textual.

**Não** faz parte deste repositório: código Vue do `sgp-web`, Questão 2, Questão 3 nem os diagramas visuais da entrega (estes foram feitos em **draw.io** e constam apenas no **PDF** enviado no Teams).

---
## Domínio (ponto de partida)

O **SGP Católica** é uma plataforma web para professores e alunos: o professor gerencia questões, turmas, provas e aplicações com geração de PDF em múltiplas versões, publica gabaritos e lança notas; o aluno consulta provas atribuídas e o histórico de notas. Detalhes em [`00-dominio.md`](00-dominio.md).

---
## Como navegar

| Item | Conteúdo |
|------|----------|
| [`00-dominio.md`](00-dominio.md) | Parágrafo de domínio, personas, linguagem ubíqua, mapa de contexts |
| [`01-arquitetura-ddd.md`](01-arquitetura-ddd.md) | Princípios DDD/hexagonal, portas, regras de domínio, relação com o frontend |
| [`contexts/`](contexts/) | Um diretório por bounded context (com README explicando o contexto) |
| [`shared/kernel/`](shared/kernel/) | Kernel compartilhado |

### Bounded contexts

```
contexts/
  identity/       # Identidade e Acesso
  questions/      # Banco de Questões
  classes/        # Turmas e Matrículas
  exams/          # Montagem de Provas
  applications/   # Aplicação e Versões
  grading/        # Correção e Notas
  reports/        # Relatórios
```

Cada contexto contém `domain/`, `application/`, `ports/` e `adapters/` (entrada HTTP e saída de persistência; alguns têm messaging/PDF). Arquivos `.gitkeep` marcam pastas ainda sem implementação de código — a Q1 exige a **organização**, não o código-fonte.

---

## Observações

- Não há implementação completa do backend neste repositório; a entrega da Q1 é a **estrutura arquitetural**.
- Questões 2 e 3 e figuras draw.io estão no PDF do Teams.
