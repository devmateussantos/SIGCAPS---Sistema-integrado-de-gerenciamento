# SIGCAPS — Dicionário de Dados Consolidado

**Versão:** 1.0  
**Status:** Aprovado — Fechamento da Fase 1  
**Data:** 2026-08-29

## 1. Objetivo

Este documento descreve os atributos das entidades que compõem o modelo de dados do SIGCAPS, consolidado ao final da Fase 1.

O documento complementa o Modelo Geral de Domínio e o MER v1.0, servindo como referência para a futura implementação técnica.

Os tipos apresentados são **conceituais**, não representando necessariamente os tipos definitivos do SGBD que será adotado na implementação.


## 2. Convenções

| Convenção | Significado |
|---|---|
| Sim | Campo obrigatório |
| Não | Campo opcional |
| Condicional | Obrigatório somente quando determinada regra de negócio for atendida |
| Identificador | Identificador único da entidade |
| Texto | Informação textual |
| Inteiro | Número inteiro |
| Decimal | Número com casas decimais |
| Booleano | Verdadeiro/Falso |
| Data | Data sem horário |
| Data/Hora | Data acompanhada do horário |
| Enum | Conjunto limitado de valores definidos pelo domínio |


## 3. PACIENTE

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único do paciente. |
| `nome` | Texto | Sim | Nome completo do paciente. |
| `nomeSocial` | Texto | Não | Nome pelo qual o paciente quer ser chamado. |
| `sexo` | ENUM | Sim | Sexo ao qual o paciente se identifica. |
| `cpf` | Texto | Sim | CPF do paciente. |
| `cartaoSus` | Texto | Sim | Número do Cartão Nacional de Saúde (CNS). |
| `dataNascimento` | DATE | Sim | Utilizada para cálculo automático da idade. |
| `telefonePrincipal` | Texto | Sim | Principal número de contato do paciente. |
| `telefoneSecundario` | Texto | Não | Número alternativo utilizado para recados. |
| `logradouro` | Texto | Sim | Nome da rua onde o paciente reside. |
| `numero` | Texto | Sim | Número da casa do paciente. |
| `bairro` | Texto | Sim | Bairro onde o paciente reside. |
| `cidade` | Texto | Sim | Cidade onde o paciente reside. |
| `estado` | CHAR(2) | Sim | Estado onde o paciente reside. |
| `cep` | Texto | Sim | Código de endereço postal do paciente. |
| `nomeMae` | Texto | Não | Nome da mãe do paciente. |
| `nomePai` | Texto | Não | Nome do pai do paciente. |
| `responsavelLegal` | Texto | Não | O paciente pode ser menor de idade ou não responder por si mesmo. |
| `queixaPrincipal` | Texto | Sim | Relato apresentado em encaminhamento ou descrito pelo paciente ou pelo responsável. |
| `status` | Enum | Sim | `ATIVO` ou `INATIVO`. |
| `motivoInativacao` | Texto | Condicional | Motivo pelo qual o paciente foi inativado. |
| `tipoPaciente` | ENUM | Sim | AMBULATORIAL/INTENSIVO define qual o tipo de atendimento ou atividades o paciente pode participar. |
| `informacoesEncaminhamento` | Texto | Não | Informações referentes à requisição de encaminhamento apresentada no primeiro cadastro. |
| `criadoEm` | TIMESTAMPTZ | Sim | Data e hora da criação da ficha cadastral do paciente. |
| `atualizadoEm` | TIMESTAMPTZ | Sim | Atualizado automaticamente sempre que uma alteração ocorrer no cadastro do paciente. |

### Regras

- Pacientes não são excluídos.
- A inativação não remove o histórico do paciente.
- `motivoInativacao` é obrigatório quando `status` for `INATIVO`.
- A idade não é armazenada; é calculada a partir de `dataNascimento`.
- O endereço permanece simplificado no MVP.
- As informações do encaminhamento podem ser preservadas.


## 4. USUARIO

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único do usuário. |
| `nome` | Texto | Sim | Nome do usuário. |
| `cpf` | Texto | Sim | CPF do usuário. |
| `login` | Texto | Sim | Identificador utilizado para autenticação. |
| `senhaHash` | Texto | Sim | Credencial armazenada de forma segura na implementação. |
| `matricula` | Texto | Não | Matrícula funcional/administrativa, caso exista. |
| `ativo` | Booleano | Sim | Indica se o usuário pode acessar o sistema. |
| `perfilId` | Identificador | Sim | Referência ao perfil do usuário. |
| `ultimoLogin` | TIMESTAMPTZ | Não | Atualizado automaticamente. |
| `criadoEm` | TIMESTAMPTZ | Sim | Auditoria |
| `atualizadoEm` | TIMESTAMPTZ | Sim | Auditoria |

### Regras

- Cada usuário possui um único perfil no MVP.
- O perfil determina suas permissões.
- A matrícula não é obrigatória.
- Usuários inativos não devem acessar o sistema.


## 5. PERFIL

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único do perfil. |
| `nome` | Texto | Sim | Nome do perfil deve ser único. |
| `descricao` | Texto | Não | Descrição das responsabilidades do perfil. |
| `criadoEm` | TIMESTAMPTZ | Sim | Auditoria |


## 6. PERMISSAO

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único da permissão. |
| `nome` | Texto | Sim | Nome da permissão. |
| `descricao` | Texto | Não | Descrição da ação autorizada. |


## 7. AGENDAMENTO

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único do agendamento. |
| `pacienteId` | Identificador | Sim | Referência ao paciente agendado. |
| `profissionalId` | Identificador | Sim | Referência ao profissional que realizará o atendimento. |
| `dataAgendamento` | Data | Sim | Data prevista para o atendimento. |
| `periodo` | Enum | Sim | `MANHA` ou `TARDE`. |
| `tipoAgendamento` | Enum | Sim | NORMAL / ENCAIXE |
| `status` | Enum | Sim |  `AGENDADO`, `REALIZADO`, `CANCELADO` ou `FALTOU`. |
| `motivoEncaixe` | Texto | Condicional | Motivo do encaixe quando aplicável. |
| `criadoPorUsuarioId` | Identificador | Sim | Usuário responsável pelo registro. |
| `observacoes` | TEXT | Não | Informações complementares |
| `criadoEm` | TIMESTAMPTZ | Sim | Auditoria |
| `atualizadoEm` | TIMESTAMPTZ | Sim | Auditoria |

### Regras

- Não será definido horário específico no agendamento do MVP.
- O horário efetivo será registrado no Atendimento.
- O profissional que atender pode ser diferente de quem criou o agendamento.
- `motivoEncaixe` deve ser informado quando aplicável.
- Remarcação permanece no backlog.
- `origemAgendamento` permanece no backlog.


## 8. ATENDIMENTO

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único do atendimento. |
| `agendamentoId` | Identificador | Sim | Agendamento que originou o atendimento. |
| `dataHoraAtendimento` | Data/Hora | Sim | Momento efetivo da interação. |
| `informacoes` | Texto | Não | Informações registradas pelo profissional. |
| `criadoPorUsuarioId` | Identificador | Sim | Usuário responsável pelo registro. |
| `criadoEm` | Data/Hora | Sim | Momento de criação. |
| `atualizadoEm` | Data/Hora | Sim | Momento da última atualização. |

### Regras

- `pacienteId` e `profissionalId` não são duplicados em Atendimento no MVP; são obtidos através do Agendamento.
- Atendimento não representa agendamento.
- Atendimento somente pode existir associado a um agendamento.
- Um agendamento pode não resultar em atendimento.
- Uma falta não gera atendimento.
- Um paciente pode possuir vários atendimentos no mesmo dia.
- Atendimentos de profissionais diferentes são registros independentes.
- O profissional pode editar seu próprio atendimento.
- A Coordenação poderá editar conforme as permissões definidas.


## 9. TRIAGEM

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único da triagem. |
| `pacienteId` | Identificador | Sim | Referência ao paciente. |
| `dataHoraAfericao` | Data/Hora | Sim | Momento das aferições. |
| `temperatura` | Decimal | Não | Temperatura em graus Celsius. |
| `peso` | Decimal | Não | Peso em quilogramas, com uma casa decimal. |
| `pressaoSistolica` | Inteiro | Não | Pressão sistólica. |
| `pressaoDiastolica` | Inteiro | Não | Pressão diastólica. |
| `glicemia` | Inteiro | Não | Glicemia em mg/dL. |
| `situacaoGlicemia` | Texto/Enum | Condicional | Jejum, pré-refeição, pós-refeição etc. |
| `criadoPorUsuarioId` | Identificador | Sim | Usuário que criou o registro. |
| `alteradoPorUsuarioId` | Identificador | Não | Usuário da última alteração. |
| `criadoEm` | Data/Hora | Sim | Momento da criação. |
| `atualizadoEm` | Data/Hora | Sim | Momento da última alteração. |

### Regras

- Nenhuma aferição individual é obrigatória.
- Uma triagem sem qualquer informação de aferição não deve ser registrada.
- A pressão é armazenada separadamente em sistólica e diastólica.
- O peso possui uma casa decimal.
- A temperatura utiliza graus Celsius.
- A glicemia utiliza mg/dL.
- `situacaoGlicemia` somente possui significado quando `glicemia` for informada.
- A data/hora da triagem é independente da data/hora do atendimento.
- Técnicos de enfermagem e Coordenação podem editar.
- Deve ser possível identificar quem criou e quem alterou o registro.
- Pelo menos uma aferição deve existir.
- Sistólica e diastólica devem ser preenchidas juntas.


## 10. ATIVIDADEGRUPO

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `id` | Identificador | Sim | Identificador único da atividade. |
| `tipoAtividade` | Enum/Texto | Sim | Tipo da atividade realizada. |
| `dataHora` | Data/Hora | Sim | Momento da atividade. |
| `descricao` | Texto | Não | Breve descrição da atividade ou assunto abordado. |
| `criadoPorUsuarioId` | Identificador | Sim | Profissional responsável pelo registro. |
| `criadoEm` | Data/Hora | Sim | Momento da criação. |
| `atualizadoEm` | Data/Hora | Sim | Momento da última alteração. |

### Exemplos de tipo

- `ACOLHIMENTO`
- `DINAMICA_GRUPO`
- `ALONGAMENTO`
- Outros tipos definidos posteriormente.

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


## 11. ATIVIDADEGRUPOPARTICIPANTE

Entidade associativa que materializa o relacionamento N:N entre AtividadeGrupo e Paciente.

| Campo | Tipo conceitual | Obrigatório | Descrição |
|---|---|---:|---|
| `atividadeGrupoId` | Identificador | Sim | Referência à atividade em grupo. |
| `pacienteId` | Identificador | Sim | Referência ao paciente participante. |

### Regras

- Um paciente pode participar de várias atividades.
- Uma atividade pode possuir vários pacientes.
- A combinação `atividadeGrupoId + pacienteId` deve ser única.
- Não representa um conceito de negócio independente.


## 12. Resumo dos relacionamentos

| Origem | Cardinalidade | Destino |
|---|---:|---|
| Paciente | 1:N | Agendamento |
| Paciente | 1:N | Atendimento |
| Paciente | 1:N | Triagem |
| Paciente | 1:N | AtividadeGrupoParticipante |
| Agendamento | 1:0..1 | Atendimento |
| Usuário | 1:N | Agendamento |
| Usuário | 1:N | Atendimento |
| Usuário | 1:N | Triagem |
| Usuário | 1:N | AtividadeGrupo |
| Usuário | N:1 | Perfil |
| Perfil | N:N | Permissão |
| AtividadeGrupo | 1:N | AtividadeGrupoParticipante |


## 13. Regras gerais de integridade

1. O histórico do paciente não deve ser excluído em razão de sua inativação.
2. Um Atendimento não deve existir sem Agendamento.
3. Um Agendamento pode existir sem Atendimento.
4. Uma falta não gera Atendimento.
5. O profissional responsável pelo Atendimento é independente do usuário que criou o Agendamento.
6. Cada Atendimento representa uma interação profissional independente.
7. A Triagem possui data/hora própria.
8. Uma Triagem completamente sem aferições não deve ser registrada.
9. Uma AtividadeGrupo deve possuir participantes.
10. Um profissional não pode registrar AtividadeGrupo em nome de outro profissional.
11. A combinação de uma atividade e um paciente participante não deve ser duplicada.
12. Usuários possuem um único Perfil no MVP.
13. Permissões são atribuídas através do Perfil.
14. Informações históricas devem ser preservadas.


## 14. Observações para a implementação

Este documento não determina ainda:

- SGBD;
- framework;
- ORM;
- estratégia de migrations;
- índices físicos;
- nomes definitivos das tabelas;
- estratégia de autenticação;
- criptografia utilizada para credenciais.

Essas decisões pertencem à etapa de implementação técnica.

O documento deve ser utilizado como referência funcional para essas decisões.

