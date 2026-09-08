# Dicionário de Dados — Atividade em Grupo

**Projeto:** SIGCAPS  
**Versão:** 1.0  
**Status:** Aprovado para o MVP  
**Data:** 2026-08-18

## Entidade: AtividadeGrupo

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | UUID | Sim | Identificador único da atividade. |
| `tipoAtividade` | ENUM | Sim | Tipo da atividade coletiva. |
| `dataHora` | TIMESTAMPTZ | Sim | Data e hora em que ocorreu. |
| `descricao` | TEXT | Não | Breve descrição ou assunto abordado. |
| `criadoPorUsuarioId` | UUID | Sim | Usuário que registrou a atividade. |
| `criadoEm` | TIMESTAMPTZ | Sim | Data/hora de criação. |
| `atualizadoEm` | TIMESTAMPTZ | Sim | Data/hora da última atualização. |

## Domínio de tipoAtividade

| Valor | Descrição |
|---|---|
| `ACOLHIMENTO` | Acolhimento realizado em grupo. |
| `DINAMICA_GRUPO` | Dinâmica realizada com participantes. |
| `ALONGAMENTO` | Atividade coletiva de alongamento. |
| `OUTRA` | Atividade não contemplada pelos tipos anteriores. |

## Relacionamentos

`AtividadeGrupo N:N Paciente`

Um paciente pode participar de várias atividades e uma atividade pode possuir vários participantes. A estrutura associativa necessária à implementação não constitui uma entidade de domínio independente no MVP.

`Usuário 1:N AtividadeGrupo`

`criadoPorUsuarioId` identifica o profissional responsável pelo lançamento. O usuário autenticado somente poderá criar atividades para si próprio.

### Regras

- A atividade é registrada pelo profissional autenticado.
- O profissional somente pode registrar atividade para si próprio.
- Uma atividade pode possuir vários participantes.
- A quantidade de participantes não altera a produção do profissional.
- `ACOLHIMENTO` é um tipo de atividade e não uma entidade separada.

### Regras de integridade

- `tipoAtividade` é obrigatório.
- `dataHora` é obrigatório.
- `criadoPorUsuarioId` é obrigatório.
- Uma atividade deve possuir pelo menos um participante.
- `descricao` é opcional.
- A quantidade de participantes não altera a produção contabilizada.
