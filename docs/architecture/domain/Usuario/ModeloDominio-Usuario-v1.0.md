# Modelo de Domínio — Usuário

**Versão:** 1.0

**Status:** Aprovado

**Data:** 05/08/2026

**Autor:** Mateus dos Santos

**Mentoria Técnica:** ChatGPT

## Objetivo

Representar o usuário dentro do domínio do SIGCAPS, armazenando suas informações cadastrais administrativas importantes para a diferenciação de perfis e controle de acesso.

---


## Responsabilidades

A entidade Usuário é responsável por:

- Identificar unicamente cada usuário.
- Registrar informações cadastrais.
- Controlar o status do usuário.

---

## Regras de Negócio

RN-011

Todo usuário deve possuir login único.

RN-012

Todo usuário deve possuir e-mail único.

RN-013

A senha nunca será armazenada em texto puro.

RN-014

Usuários podem ser apenas inativados.

RN-015

Todo usuário deve possuir exatamente um perfil.

RN-016

O sistema registra automaticamente o último acesso.

---

## Relacionamentos

├── N:1 Perfil
├── 1:N Agendamento
├── 1:N Atendimento
└── 1:N AtividadeGrupo