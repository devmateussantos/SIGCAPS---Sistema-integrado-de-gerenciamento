# SIGCAPS — Modelo Entidade-Relacionamento (MER)

**Versão:** 1.0  
**Status:** Consolidado — Fechamento da Fase 1  
**Data:** 2026-08-21

---

## 1. Objetivo

Este documento apresenta o Modelo Entidade-Relacionamento (MER) consolidado do SIGCAPS ao final da Fase 1.

O modelo representa a estrutura conceitual dos dados necessários para suportar as principais regras de negócio definidas para o MVP.

O MER serve como referência para a futura implementação do banco de dados, sem definir neste momento detalhes específicos de um SGBD.

---

# 2. Entidades

O MER do MVP é composto pelas seguintes entidades:

- Paciente
- Usuário
- Perfil
- Permissão
- Agendamento
- Atendimento
- Triagem
- AtividadeGrupo
- AtividadeGrupoParticipante

> `AtividadeGrupoParticipante` é uma entidade associativa necessária para representar o relacionamento N:N entre AtividadeGrupo e Paciente. Ela não representa um novo conceito de negócio independente.

---

# 3. Entidade PACIENTE

Representa a pessoa atendida ou acompanhada pelo CAPS.

### Principais atributos

```text

Paciente
├── id
├── nome
├── cpf
├── cartaoSus
├── telefonePrincipal
├── telefoneRecado
├── endereco
├── status
├── motivoInativacao
└── informacoesEncaminhamento