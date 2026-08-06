# Modelo de Domínio — Perfil

**Versão:** 1.0

**Status:** Aprovado

**Data:** 05/08/2026

**Autor:** Mateus dos Santos

**Mentoria Técnica:** ChatGPT

## Objetivo

Definir as permissões dos usuários dentro do sistema SIGCAPS.

---

## Responsabilidades

A entidade Usuário é responsável por:

- Identificar a responsabilidade de cada usuário.
- Distribuir as permissões dos usuários
---

## Regras de Negócio

RN-017

Perfis representam funções dentro do sistema.

RN-018

Permissões são definidas pelo perfil.

RN-019

Um perfil pode estar associado a vários usuários.

---

## Relacionamentos

├── N:1 Perfil