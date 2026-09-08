# Dicionário de Dados — Agendamento

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Chave primária|
| pacienteId | UUID | Sim | FK Paciente |
| profissionalId | UUID | Sim | FK Usuário |
| criadoPorUsuarioId | UUID | Sim | FK Usuário |
| dataAgendamento | DATE | Sim | Data prevista do atendimento |
| periodo | ENUM | Sim | MANHA / TARDE |
| tipoAgendamento | ENUM | Sim | NORMAL / ENCAIXE |
| motivoEncaixe | TEXT | Condicional | Obrigatório quando tipoAgendamento = ENCAIXE |
| status | ENUM | Sim | AGENDADO / REALIZADO / CANCELADO / FALTOU |
| observacoes | TEXT | Não | Informações complementares |
| criadoEm | TIMESTAMPTZ | Sim | Auditoria |
| atualizadoEm | TIMESTAMPTZ | Sim | Auditoria |

### Regras

- Não será definido horário específico no agendamento do MVP.
- O horário efetivo será registrado no Atendimento.
- O profissional que atender pode ser diferente de quem criou o agendamento.
- `motivoEncaixe` deve ser informado quando aplicável.
- Remarcação permanece no backlog.
- `origemAgendamento` permanece no backlog.