# Modelo de Domínio — Atendimento

**Versão:** 1.0  
**Status:** Aprovado para MVP  
**Data:** 2026-08-08  
**Projeto:** SIGCAPS

## Objetivo
Representar a interação efetivamente realizada entre um profissional e um paciente, originada a partir de um agendamento.

## Responsabilidades
- Registrar a realização efetiva do atendimento.
- Associar o atendimento ao agendamento que o originou.
- Registrar data e hora efetivas da interação.
- Registrar informações do atendimento no MVP.
- Preservar a autoria do registro.
- Integrar o atendimento à linha do tempo do paciente.
- Servir de base para a produção profissional.

## Regras de Negócio
- **RN-034:** Todo Atendimento deve estar vinculado a um Agendamento.
- **RN-035:** Um Agendamento pode resultar em no máximo um Atendimento.
- **RN-036:** Agendamento com status FALTOU ou CANCELADO não gera Atendimento.
- **RN-037:** Um paciente pode possuir múltiplos Atendimentos ao longo do tempo.
- **RN-038:** Um paciente pode possuir múltiplos Atendimentos na mesma data, inclusive com profissionais diferentes.
- **RN-039:** Cada Atendimento representa uma interação individual e conta para a produção do profissional responsável.
- **RN-040:** `dataHoraAtendimento` representa o momento efetivo da interação.
- **RN-041:** Após o registro, o Atendimento somente poderá ser alterado pelo profissional responsável ou pela Coordenação.
- **RN-042:** O Atendimento utiliza `agendamentoId` para obter paciente e profissional, evitando duplicação.

## Relacionamentos
- Paciente 1:N Atendimento.
- Usuário (profissional) 1:N Atendimento.
- Agendamento 1:0..1 Atendimento.
- Atendimento integra a linha do tempo do paciente.

## Histórico
| Versão | Data | Alteração |
|---|---|---|
| 1.0 | 2026-08-08 | Criação e consolidação da entidade Atendimento. |

## Decisões relacionadas
- ADR-006 — Representação do encaixe como tipo de Agendamento.
- ADR-007 — Atendimento como evento efetivo originado de Agendamento.
