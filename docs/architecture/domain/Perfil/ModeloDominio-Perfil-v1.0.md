# Modelo de Domínio — Perfil

**Versão:** 1.0

**Status:** Aprovado

**Data:** 05/08/2026

**Autor:** Mateus dos Santos

**Mentoria Técnica:** ChatGPT

## Objetivo

Definir as funções dos usuários e servir como referência para a determinação de suas permissões dentro do sistema SIGCAPS.

---

## Responsabilidades

A entidade Perfil é responsável por:

- Representar uma função dentro do sistema.
- Servir como referência para as permissões associadas aos usuários.
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

├── 1:N Usuário