# SIGCAPS — Modelo Geral de Domínio

**Versão:** 1.0  
**Status:** Aprovado — Consolidação da Fase 1  
**Data:** 2026-08-29

## 1. Objetivo

Este documento consolida o modelo geral de domínio do SIGCAPS ao final da Fase 1 — Análise, Modelagem e Documentação.

Seu objetivo é apresentar uma visão única dos principais conceitos do domínio, suas responsabilidades, relacionamentos e regras de negócio, servindo como referência para a implementação técnica.

Este documento deve ser analisado em conjunto com o MER v1.0 e com o Dicionário de Dados Consolidado v1.0.

---

## 2. Escopo do domínio

O SIGCAPS tem como objetivo apoiar o gerenciamento das principais atividades administrativas e assistenciais de uma unidade CAPS, reduzindo a dependência de registros manuais em cadernos, prontuários e folhas de produção.

O MVP contempla:

- cadastro e gerenciamento de pacientes;
- controle de usuários, perfis e permissões;
- agendamento de atendimentos;
- registro de atendimentos realizados;
- registro de triagens;
- registro de atividades em grupo;
- registro dos participantes das atividades;
- preservação do histórico dos pacientes;
- apoio à apuração da produção dos profissionais.

---

## 3. Entidades do MVP

O domínio consolidado é composto pelas seguintes entidades:

1. Paciente
2. Usuário
3. Perfil
4. Permissão
5. Agendamento
6. Atendimento
7. Triagem
8. AtividadeGrupo
9. AtividadeGrupoParticipante

`AtividadeGrupoParticipante` é uma entidade associativa utilizada para materializar o relacionamento entre `AtividadeGrupo` e `Paciente`. Ela não representa um conceito de negócio independente.

---

## 4. Visão geral do domínio

```text
                         ┌──────────────┐
                         │   USUÁRIO    │
                         └──────┬───────┘
                                │
                                │ N:1
                                ▼
                         ┌──────────────┐
                         │    PERFIL    │
                         └──────┬───────┘
                                │
                                │ N:N
                                ▼
                         ┌──────────────┐
                         │  PERMISSÃO   │
                         └──────────────┘


┌──────────────┐
│   PACIENTE   │
└──────┬───────┘
       │
       ├───────────────┐
       │               │
       │ 1:N           │ 1:N
       ▼               ▼
┌─────────────┐  ┌─────────────┐
│ AGENDAMENTO │  │   TRIAGEM   │
└──────┬──────┘  └─────────────┘
       │
       │ 0..1
       ▼
┌─────────────┐
│ ATENDIMENTO │
└─────────────┘


┌──────────────────┐
│  ATIVIDADEGRUPO  │
└────────┬─────────┘
         │
         │ 1:N
         ▼
┌────────────────────────────┐
│ ATIVIDADEGRUPOPARTICIPANTE │
└──────────────┬─────────────┘
               │
               │ N:1
               ▼
          ┌──────────┐
          │ PACIENTE │
          └──────────┘
```

---

## 5. Paciente

O **Paciente** representa a pessoa atendida ou acompanhada pela unidade CAPS.

### Responsabilidades

- armazenar os dados cadastrais;
- manter informações de identificação e contato;
- armazenar informações básicas do paciente;
- identificar se o paciente é ambulatorial ou intensivo;
- manter o status de acompanhamento;
- preservar o histórico mesmo após a inativação;
- armazenar informações relacionadas ao encaminhamento quando necessário;
- servir como referência para agendamentos;
- servir como referência para atendimentos;
- servir como referência para triagens;
- participar de atividades em grupo.

### Status

No MVP:

```text
ATIVO
INATIVO
```

A inativação não implica exclusão dos dados históricos.

Quando o status for `INATIVO`, o motivo da inativação deve ser informado.

### Tipo de paciente

No MVP:

```text
AMBULATORIAL
INTENSIVO
```

O tipo identifica o contexto de acompanhamento do paciente e influencia o fluxo de triagem e acompanhamento da unidade.

---

## 6. Usuário, Perfil e Permissão

O controle de acesso é dividido em três conceitos:

```text
Usuário
   │
   └── Perfil
          │
          └── Permissões
```

### Usuário

Representa a conta utilizada para acesso ao sistema.

Cada usuário possui um único perfil no MVP.

O usuário pode atuar como profissional de saúde, recepção, técnico de enfermagem, coordenação ou outro perfil definido pela unidade.

### Perfil

Representa o conjunto de responsabilidades e permissões associado ao usuário.

Exemplos identificados no domínio:

- Recepção;
- Coordenação;
- Técnico(a) de Enfermagem;
- Enfermeiro;
- Psicóloga;
- Assistente Social;
- Psiquiatra.

### Permissão

Representa uma ação que pode ser executada no sistema.

A separação permite que as regras de autorização sejam mantidas independentemente dos dados cadastrais do usuário.

---

## 7. Agendamento

O **Agendamento** representa o compromisso planejado entre um paciente e um profissional.

### Responsabilidades

- registrar o paciente;
- registrar o profissional responsável pelo futuro atendimento;
- registrar a data prevista;
- registrar o período;
- identificar o tipo de agendamento;
- controlar o status do agendamento;
- registrar encaixes e seus respectivos motivos;
- identificar o usuário responsável pelo lançamento.

### Tipos

No MVP:

```text
NORMAL
ENCAIXE
```

Quando o tipo for `ENCAIXE`, o motivo deve ser registrado.

### Período

No MVP:

```text
MANHA
TARDE
```

Não será definido horário específico para o agendamento.

O horário efetivo será registrado no Atendimento.

### Status

No MVP:

```text
AGENDADO
REALIZADO
CANCELADO
FALTOU
```

### Regra fundamental

O Agendamento não representa o atendimento realizado.

Ele representa a previsão de atendimento.

---

## 8. Atendimento

O **Atendimento** representa a interação efetivamente realizada entre um profissional e um paciente.

O atendimento somente existe quando o paciente comparece e a interação ocorre.

```text
Agendamento
     │
     ├── paciente faltou
     │       └── nenhum Atendimento
     │
     └── paciente compareceu
             └── Atendimento
```

### Responsabilidades

- registrar a interação realizada;
- registrar data e hora efetivas;
- identificar o profissional responsável;
- registrar informações do atendimento;
- permitir a apuração da produção profissional.

### Regras

- Todo Atendimento deve estar relacionado a um Agendamento.
- Um Agendamento pode não resultar em Atendimento.
- Uma falta não gera Atendimento.
- Um paciente pode possuir vários Atendimentos no mesmo dia.
- Cada interação profissional representa um Atendimento independente.

Exemplo:

```text
Paciente
   │
   ├── Atendimento → Psicóloga
   ├── Atendimento → Enfermeiro
   ├── Atendimento → Assistente Social
   └── Atendimento → Psiquiatra
```

Cada atendimento é contabilizado individualmente na produção do respectivo profissional.

### Edição

Após o registro, o Atendimento pode ser editado pelo próprio profissional responsável ou pela Coordenação, conforme as permissões definidas.

---

## 9. Triagem

A **Triagem** representa as aferições realizadas no paciente.

Ela possui data e hora próprias, independentes do momento do Atendimento.

### Informações

- temperatura;
- peso;
- pressão sistólica;
- pressão diastólica;
- glicemia;
- situação da glicemia.

Nenhuma aferição individual é obrigatória.

Entretanto, uma Triagem completamente sem qualquer informação de aferição não deve ser registrada.

### Contexto ambulatorial

Para pacientes ambulatoriais, a Triagem é realizada quando o paciente chega à unidade para o atendimento agendado.

### Contexto intensivo

Para pacientes intensivos, a Triagem funciona como acompanhamento e pode ser realizada em diferentes dias, não sendo obrigatória diariamente.

### Auditoria

Deve ser possível identificar:

- quem criou a Triagem;
- quem realizou a última alteração.

Técnicos(as) de enfermagem e Coordenação podem editar os registros conforme as permissões definidas.

---

## 10. AtividadeGrupo

A **AtividadeGrupo** representa uma atividade realizada coletivamente por um profissional.

Exemplos:

```text
ACOLHIMENTO
DINAMICA_GRUPO
ALONGAMENTO
```

### Responsabilidades

- registrar o tipo da atividade;
- registrar a data e hora;
- registrar uma descrição;
- identificar o profissional responsável;
- permitir o registro dos participantes.

### Regras

- A atividade é registrada pelo profissional autenticado.
- Um profissional somente pode registrar atividade para si próprio.
- Uma atividade possui participantes.
- A quantidade de participantes não altera a produção do profissional.
- `ACOLHIMENTO` é um tipo de atividade e não uma entidade independente.
- O modelo permite que outros profissionais realizem atividades em grupo no futuro.

---

## 11. AtividadeGrupoParticipante

`AtividadeGrupoParticipante` é uma entidade associativa que materializa o relacionamento entre `AtividadeGrupo` e `Paciente`.

```text
AtividadeGrupo
      │
      │ 1:N
      ▼
AtividadeGrupoParticipante
      ▲
      │ N:1
      │
   Paciente
```

### Responsabilidades

- registrar que determinado paciente participou de determinada atividade;
- impedir a duplicação da mesma participação na mesma atividade.

### Regras

- Uma AtividadeGrupo possui vários participantes.
- Um Paciente pode participar de várias atividades.
- A combinação `atividadeGrupoId + pacienteId` deve ser única.
- A entidade não representa um conceito de negócio independente.

---

## 12. Relacionamentos consolidados

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
| AtividadeGrupoParticipante | N:1 | Paciente |

---

## 13. Fluxo conceitual principal

```text
Cadastro do paciente
        │
        ▼
    Agendamento
        │
        ▼
Paciente comparece?
      /         NÃO      SIM
     │        │
     ▼        ▼
Sem        Triagem
Atendimento   │
              ▼
         Atendimento
              │
              ▼
      Produção profissional
```

Para atividades coletivas:

```text
Profissional autenticado
          │
          ▼
Atividade em grupo
          │
          ▼
Seleciona participantes
          │
          ▼
Registro da atividade
          │
          ▼
Produção do profissional
```

---

## 14. Regras de negócio consolidadas

1. Um paciente pode possuir múltiplos agendamentos.
2. Um paciente pode possuir múltiplos atendimentos.
3. Um paciente pode possuir múltiplas triagens.
4. Um paciente pode participar de múltiplas atividades em grupo.
5. Um Atendimento deve estar relacionado a um Agendamento.
6. Um Agendamento pode existir sem Atendimento.
7. A falta do paciente não gera Atendimento.
8. Um paciente pode ser atendido por vários profissionais no mesmo dia.
9. Cada Atendimento profissional é contabilizado individualmente na produção.
10. O horário efetivo pertence ao Atendimento, não ao Agendamento.
11. O Agendamento utiliza os períodos `MANHA` e `TARDE`.
12. Encaixes devem possuir motivo registrado.
13. Remarcação permanece no backlog.
14. `origemAgendamento` permanece no backlog.
15. A Triagem possui data e hora próprias.
16. Nenhuma aferição individual da Triagem é obrigatória.
17. Uma Triagem sem nenhuma aferição não deve ser registrada.
18. Técnicos(as) de enfermagem e Coordenação podem editar Triagens.
19. Deve ser possível identificar quem criou e quem alterou uma Triagem.
20. Atividades em grupo são registradas pelo profissional autenticado.
21. Um profissional não pode registrar atividade em nome de outro profissional.
22. A quantidade de participantes não altera a produção da atividade.
23. Pacientes inativados permanecem no sistema para preservação histórica.
24. Usuários possuem um único Perfil no MVP.
25. O Perfil determina as permissões do usuário.
26. A mesma participação de um paciente não pode ser registrada duas vezes na mesma atividade.

---

## 15. Decisões mantidas fora do MVP

Os seguintes itens foram identificados durante a modelagem, mas permanecem no backlog para futuras versões:

- remarcação de agendamentos;
- registro da origem do agendamento;
- evolução estruturada do paciente;
- ampliação dos dados de endereço;
- evolução do prontuário digital;
- transformação do status do paciente em entidade de domínio;
- acompanhamento diário dos pacientes intensivos como funcionalidade própria;
- dashboards avançados de produção e acompanhamento.

A existência desses itens no backlog não altera o modelo consolidado do MVP.

---

## 16. Relação com a documentação da Fase 1

Este documento deve ser utilizado em conjunto com:

- **MER v1.0** — representação estrutural das entidades e relacionamentos;
- **Dicionário de Dados Consolidado v1.0** — detalhamento dos atributos e regras dos dados;
- **Dicionários de Dados individuais** — detalhamento específico de cada entidade;
- **ADRs** — registro das decisões arquiteturais tomadas durante a evolução do projeto.

A cadeia documental da Fase 1 é:

```text
Levantamento do domínio
        ↓
Regras de negócio
        ↓
Modelo de Domínio
        ↓
MER v1.0
        ↓
Dicionários de Dados
        ↓
ADRs
        ↓
Modelo Geral de Domínio Consolidado
        ↓
Implementação Técnica
```

---

## 17. Critério de encerramento da modelagem

Com a aprovação deste documento, considera-se consolidada a modelagem conceitual do MVP da Fase 1.

A partir deste ponto, alterações estruturais no domínio deverão ser tratadas como novas decisões e devidamente documentadas, evitando alterações informais que comprometam o histórico do projeto.

---

## 18. Status

**Modelo Geral de Domínio v1.0**

**Status:** Aprovado.


