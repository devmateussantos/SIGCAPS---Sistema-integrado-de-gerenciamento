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

### Decisões Arquiteturais
- ADR-006 — Representação do encaixe como tipo de agendamento.

---------------------------------------------------

## [0.5.0] - 2026-08-08

### Adicionado
- Modelagem de Atendimento.
- Dicionário de Atendimento.
- Modelagem de Triagem.
- Dicionário de Triagem.
- ADR-007 e ADR-008.
- Regras de negócio RN-034 a RN-054.

### Alterado
- Relação Agendamento → Atendimento consolidada como 1:0..1.
- Triagem definida como entidade independente do Atendimento no MVP.
- Campos de autoria padronizados para criação e alteração.

------------------------------------------------------

## [1.0.0] - 2026-08-29

### Adicionado

- Consolidação do Modelo de Domínio do MVP.
- Modelo de Domínio da Atividade em Grupo.
- MER v1.0 consolidado.
- Dicionários de Dados consolidados.
- Modelo Geral de Domínio Consolidado v1.0.
- Entidade AtividadeGrupoParticipante.
- Consolidação das regras de negócio da Fase 1.

### Alterado

- Padronização e consolidação das entidades e relacionamentos do MVP.
- Atualização do Dicionário de Dados Consolidado.
- Atualização do Modelo Geral de Domínio.
- Padronização das nomenclaturas das entidades e atributos.

### Documentação

- Consolidação das decisões arquiteturais da Fase 1.
- Revisão cruzada entre Modelo de Domínio, MER e Dicionários de Dados.
- Registro das funcionalidades futuras no Product Backlog.

### Status

- Fase 1 — Análise, Modelagem e Documentação: **CONCLUÍDA**.