# Domínio de aplicação — SGP Católica

## Parágrafo de domínio

O **SGP Católica** (Sistema de Geração de Provas) é o domínio de uma plataforma acadêmica web voltada a professores e alunos da instituição: o professor autentica-se, mantém um banco de questões (objetivas com alternativas e discursivas com pontuação máxima), organiza turmas com matrícula direta ou por código de convite, monta provas limitadas a vinte questões com pontuação por item, aplica essas provas gerando PDFs com uma ou mais versões (embaralhamento de questões/alternativas e opcional identificação do aluno), publica gabaritos públicos e consolida notas — inclusive com correção assistida por aplicativo móvel (QR Code/câmera) prevista no produto — enquanto o aluno consulta provas atribuídas e o histórico de desempenho. O frontend em desenvolvimento na disciplina de Programação Web (`sgp-web`) materializa esse domínio com Vue 3 e uma API simulada; esta Questão 1 toma esse domínio como ponto de partida para uma arquitetura DDD/hexagonal.

## Personas e objetivos

| Persona                       | Objetivos principais                                                                                                                   |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Professor                     | Autenticar-se; CRUD de questões; turmas e matrículas; montar provas; gerar PDFs/versões; publicar gabarito; atribuir notas; relatórios |
| Aluno                         | Autenticar-se ou entrar por código; ver provas atribuídas; consultar notas e gabarito quando publicado                                 |
| Sistema / App mobile (futuro) | Enviar correções confirmadas de forma confiável para o backend                                                                         |

## Linguagem ubíqua (trecho)

| Termo     | Significado                                                                  |
| --------- | ---------------------------------------------------------------------------- |
| Questão   | Item objetiva ou discursiva do banco do professor                            |
| Prova     | Agregado de questões ordenadas com pontuação, ainda não aplicada a uma turma |
| Aplicação | Instância de uma prova aplicada a uma turma; gera versões e PDF              |
| Versão    | Variante embaralhada da aplicação, com código público de gabarito            |
| Correção  | Resultado da leitura/gabarito, com nota total e vínculo opcional ao aluno    |
| Matrícula | Vínculo ativo entre aluno e turma                                            |

## Bounded contexts (visão inicial)

| Contexto | Conceitos principais | Relação |
|----------|----------------------|---------|
| Identidade e Acesso | `User`, `RefreshToken` | Autoriza os demais contexts |
| Banco de Questões | `Question` | Alimenta Montagem de Provas |
| Turmas e Matrículas | `Class`, `ClassEnrollment` | Alimenta Aplicação e Versões |
| Montagem de Provas | `Exam` | Alimenta Aplicação e Versões |
| Aplicação e Versões | `Application`, `ExamVersion`, `AnswerKey` | Alimenta Correção e Relatórios |
| Correção e Notas | `Correction`, `ExamAssignment` | Alimenta Relatórios |
| Relatórios | `ApplicationReport` | Leitura consolidada |

Cada contexto está materializado como pasta em [`contexts/`](contexts/). Detalhamento hexagonal: [01-arquitetura-ddd.md](01-arquitetura-ddd.md). Diagramas oficiais (draw.io): PDF da atividade no Teams.
