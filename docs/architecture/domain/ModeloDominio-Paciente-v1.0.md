# Modelo de Domínio — Paciente

Versão: 1.0

Status: Aprovado

Autor: Mateus dos Santos

Revisor Técnico: ChatGPT (Mentoria)

## Objetivo

Representar o paciente dentro do domínio do SIGCAPS, armazenando suas informações cadastrais, clínicas e administrativas, preservando seu histórico durante todo o ciclo de atendimento.

---

## Responsabilidades

A entidade Paciente é responsável por:

- Identificar unicamente cada paciente.
- Registrar informações cadastrais.
- Armazenar informações de contato.
- Controlar o status do paciente.
- Relacionar o paciente com atendimentos, triagens, agendamentos e atividades em grupo.
- Preservar o histórico do paciente mesmo após sua inativação.

---

## Regras de Negócio

RN-001
Todo paciente deve possuir CPF válido e único.

RN-002
Todo paciente deve possuir Cartão Nacional do SUS único.

RN-003
Pacientes nunca são excluídos.

RN-004
Pacientes podem apenas ser inativados.

RN-005
O motivo da inativação é obrigatório quando o status for INATIVO.

RN-006
A idade nunca será armazenada.

RN-007
A idade será calculada automaticamente a partir da data de nascimento.

RN-008
O paciente pode possuir um telefone principal e um telefone secundário.

RN-009
Todo paciente pertence a apenas um tipo de acompanhamento.

- Ambulatorial
- Intensivo

RN-010
Todo paciente possui um prontuário composto pela linha do tempo dos seus registros.