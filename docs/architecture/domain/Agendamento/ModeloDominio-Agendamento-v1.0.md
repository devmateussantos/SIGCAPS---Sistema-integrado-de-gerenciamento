# Agendamento

## Versão: 1.0

Status: Aprovado

Autor: Mateus dos Santos

Revisor Técnico: ChatGPT (Mentoria)

## Objetivo

Representar o planejamento dos atendimentos futuros da unidade CAPS, registrando a intenção de atendimento entre um paciente e um profissional, independentemente da realização do atendimento.

---

## Responsabilidades

- Registrar o planejamento dos atendimento.
- Associar pacientes aos profissionais.
- Registrar quem realizou o agendamento.
- Registrar a data prevista.
- Registrar o período do atendimento.
- Controlar o status do agendamento.
- Identificar agendamentos do tipo encaixe.
- Preservar o histórico do agendamento.

---

## Regras de Negócio

RN-021
Todo agendamento pertence exatamente a um paciente.

RN-022
Todo agendamento possui exatamente um profissional responsável.

RN-023
Todo agendamento registra o usuário que realizou o agendamento.

RN-024
O período permitido é:

- MANHÃ
- TARDE

RN-025
O horário específico não será armazenado no MVP.

RN-026
Um paciente pode possuir múltiplos agendamentos na mesma data, desde que destinados a profissionais diferentes. Não é permitido mais de um agendamento para o mesmo paciente com o mesmo profissional na mesma data.

RN-027
Um atendimento somente poderá ser iniciado a partir de um agendamento com status AGENDADO.

RN-028
Após a conclusão do atendimento, o status do agendamento deverá ser atualizado para REALIZADO.

RN-029
Agendamentos com status CANCELADO ou FALTOU permanecem registrados para fins de auditoria e não geram Atendimento.

RN-030
Agendamentos do tipo ENCAIXE podem ser criados independentemente da abertura oficial da agenda mensal.

RN-031
Pacientes atendidos em situação de urgência poderão ser registrados por meio de um agendamento do tipo ENCAIXE.

RN-032
O motivo do encaixe será obrigatório quando o tipo do agendamento for ENCAIXE.

Essa última regra (RN-032) é uma pequena evolução da nossa conversa. Ela garante que o sistema registre por que aquele paciente foi encaixado, preservando o contexto para futuras consultas e indicadores.

---

## Relacionamentos

Paciente
1 → N Agendamentos

Usuário (Profissional)
1 → N Agendamentos

Usuário (Quem Agendou)
1 → N Agendamentos

Agendamento
1 → 0..1 Atendimento