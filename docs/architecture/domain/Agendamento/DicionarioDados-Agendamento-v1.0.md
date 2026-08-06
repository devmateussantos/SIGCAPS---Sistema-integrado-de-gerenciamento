# Dicionário de Dados — Agendamento

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Chave primária|
| pacienteId | UUID | Sim | FK Paciente |
| profissionalId | UUID | Sim | FK Usuário |
| usuarioAgendouId | UUID | Sim | FK Usuário |
| dataAgendamento | DATE | Sim | Data prevista do atendimento |
| periodo | ENUM | Sim | MANHÃ / TARDE |
| tipoAgendamento | ENUM | Sim | NORMAL / ENCAIXE |
| motivoEncaixe | TEXT | Condicional | Obrigatório quando tipoAgendamento = ENCAIXE |
| status | ENUM | Sim | AGENDADO / REALIZADO / CANCELADO / FALTOU |
| observacoes | TEXT | Não | Informações complementares |
| criadoEm | TIMESTAMPTZ | Sim | Auditoria |
| atualizadoEm | TIMESTAMPTZ | Sim | Auditoria |
