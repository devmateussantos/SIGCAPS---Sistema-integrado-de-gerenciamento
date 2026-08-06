# Changelog

Todas as alterações relevantes deste projeto serão documentadas aqui.

---

## [0.1.0] - Fundação

### Adicionado

- Estrutura inicial do Monorepo
- Organização da documentação
- Definição da arquitetura documental
- Roadmap inicial
- Modelo de Domínio iniciado

-------------------------------------------

## [0.2.0]

### Adicionado

- Modelo de Domínio da entidade Paciente.

- Dicionário de Dados da entidade Paciente.

- ADR-004.

### Alterado

- Padronização da documentação da arquitetura.

- Definição oficial dos tipos de dados.

-------------------------------------------

## [0.3.0] - Modelagem de Usuários e Perfil

### Adicionado

- Modelo de Domínio da entidade Usuário.
- Modelo de Domínio da entidade Perfil.
- Dicionário de Dados das entidades Usuário e Perfil.
- Documento Matriz de Permissões v1.0.
- Campo opcional "matricula" para futura integração com sistemas administrativos.

### Alterado

- Separação entre os conceitos de Usuário, Perfil e Permissões.
- Definição da estratégia inicial de controle de acesso (RBAC).

### Decisões Arquiteturais

- ADR-005 — Separação entre Perfil e Permissões.

---------------------------------------------------

## [0.4.0] - 2026-08-06

### Adicionado

- Modelagem da entidade Agendamento.
- Definição dos tipos de agendamento (NORMAL e ENCAIXE).
- Definição dos status do agendamento.
- Regras de negócio RN-021 a RN-032.
- Dicionário de Dados da entidade Agendamento.
- Relacionamentos da entidade Agendamento.
- Registro de novas evoluções no Product Backlog.

### Alterado

- Padronização da nomenclatura para `criadoPorUsuarioId`.