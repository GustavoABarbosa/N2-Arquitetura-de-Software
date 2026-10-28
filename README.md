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

Aqui está a **organização da arquitetura** do domínio do **SGP Católica** (Sistema de Geração de Provas) em perspectiva **Domain-Driven Design / hexagonal** (ports & adapters).

**Não** faz parte deste repositório:

- o código-fonte Vue do projeto web (`sgp-web`);
- a Questão 2 (mensageria + C4);
- a Questão 3 (inspeção SOLID).

Esses demais itens da N2 ficam no documento entregue no Teams.

---

## Domínio (ponto de partida)

O **SGP Católica** é uma plataforma web para professores e alunos: o professor gerencia questões (objetivas e discursivas), turmas, provas e aplicações com geração de PDF em múltiplas versões, publica gabaritos e lança notas; o aluno consulta provas atribuídas e o histórico de notas. A organização neste repositório traduz esse domínio em bounded contexts e camadas hexagonais.

---
## Observações

- Este repositório documenta a **organização arquitetural**; não inclui nenhuma implementação.
