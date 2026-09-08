# Modelo de Domínio — Atividade em Grupo

**Projeto:** SIGCAPS  
**Versão:** 1.0  
**Status:** Aprovado para o MVP  
**Data:** 2026-08-18

## Objetivo

Representar uma atividade coletiva realizada por um profissional do CAPS, registrando o tipo, data/hora, descrição e pacientes participantes.

A atividade é contabilizada na produção do profissional responsável como **uma única atividade**, independentemente da quantidade de participantes.

## Estrutura conceitual

```text
┌─────────────────────────────┐
│      ATIVIDADE_GRUPO        │
├─────────────────────────────┤
│ id                          │
│ tipoAtividade               │
│ dataHora                    │
│ descricao                   │
│ criadoPorUsuarioId          │
│ criadoEm                    │
│ atualizadoEm                │
└──────────────┬──────────────┘
               │
               │ N:N
               ▼
        ┌─────────────┐
        │   PACIENTE  │
        └─────────────┘

USUÁRIO 1 ─────────── N ATIVIDADE_GRUPO
```

## Responsabilidades

- Registrar a atividade coletiva.
- Identificar seu tipo.
- Registrar data e hora.
- Registrar uma breve descrição.
- Identificar o usuário responsável.
- Relacionar os pacientes participantes.
- Fornecer a informação necessária para a produção profissional.

## Relacionamentos

### Usuário → AtividadeGrupo
Um usuário pode registrar várias atividades; cada atividade possui um único usuário responsável.

**Cardinalidade:** `Usuário 1:N AtividadeGrupo`

### AtividadeGrupo ↔ Paciente
Uma atividade pode possuir vários participantes e um paciente pode participar de várias atividades.

**Cardinalidade:** `AtividadeGrupo N:N Paciente`

A relação N:N será implementada tecnicamente por uma estrutura associativa, sem criar uma nova entidade de domínio no MVP.

## Tipos de atividade

- `ACOLHIMENTO`
- `DINAMICA_GRUPO`
- `ALONGAMENTO`
- `OUTRA`

`ACOLHIMENTO` é um tipo de atividade e não uma entidade independente.

## Regras de negócio

- **RN-055:** Uma Atividade em Grupo deve possuir um usuário responsável pelo registro.
- **RN-056:** O usuário somente poderá registrar uma atividade para si próprio.
- **RN-057:** Uma Atividade em Grupo deve possuir data e hora.
- **RN-058:** Uma Atividade em Grupo deve possuir um tipo.
- **RN-059:** Uma Atividade em Grupo deve possuir pelo menos um paciente participante.
- **RN-060:** Um paciente pode participar de várias Atividades em Grupo.
- **RN-061:** Uma Atividade em Grupo pode possuir vários pacientes participantes.
- **RN-062:** A quantidade de participantes não altera a quantidade contabilizada na produção.
- **RN-063:** Uma Atividade em Grupo contabiliza uma única atividade na produção do profissional responsável.
- **RN-064:** `ACOLHIMENTO` será representado como tipo de Atividade em Grupo.

## Exemplo de produção

```text
Atividade: Acolhimento
Profissional: Psicóloga
Participantes: 8 pacientes

Produção:
1 atividade em grupo
```

## Escopo do MVP

Incluído: registro da atividade, tipo, data/hora, descrição, profissional responsável, participantes e contabilização como atividade única.

Fora do MVP: histórico avançado de alterações, aprovação, relatórios específicos e catálogo administrativo configurável de tipos.

## Histórico

| Versão | Data | Alteração |
|---|---|---|
| 1.0 | 2026-08-18 | Criação e consolidação da entidade AtividadeGrupo para o MVP. |
