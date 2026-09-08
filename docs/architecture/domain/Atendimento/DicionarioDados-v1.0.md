# Dicionário de Dados — Atendimento

**Versão:** 1.0  
**Status:** Aprovado para MVP  
**Data:** 2026-08-08

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---:|---|
| id | UUID | Sim | Identificador único. |
| agendamentoId | UUID | Sim | Agendamento que originou o atendimento. |
| dataHoraAtendimento | TIMESTAMPTZ | Sim | Momento efetivo da interação. |
| informacoes | TEXT | Não | Informações registradas pelo profissional no MVP. |
| criadoPorUsuarioId | UUID | Sim | Usuário responsável pelo registro. |
| criadoEm | TIMESTAMPTZ | Sim | Data/hora de criação. |
| atualizadoEm | TIMESTAMPTZ | Sim | Data/hora da última alteração. |

### Regras

- `pacienteId` e `profissionalId` não são duplicados em Atendimento no MVP; são obtidos através do Agendamento.
- Atendimento não representa agendamento.
- Atendimento somente pode existir associado a um agendamento.
- Um agendamento pode não resultar em atendimento.
- Uma falta não gera atendimento.
- Um paciente pode possuir vários atendimentos no mesmo dia.
- Atendimentos de profissionais diferentes são registros independentes.
- O profissional pode editar seu próprio atendimento.
- A Coordenação poderá editar conforme as permissões definidas.
