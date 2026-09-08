# SIGCAPS — Dicionário de Dados Consolidado
## Versão: 1.0
## Status: Em revisão — Fechamento da Fase 1
## Data: 2026-08-23


### 🔎 Dois pontos que quero que você observe com atenção

Há duas decisões aqui que considero especialmente importantes.

**1. `AtividadeGrupoParticipante` permanece como estrutura associativa**, exatamente como concluímos no MER. Não estamos reabrindo a modelagem criando uma nova entidade de negócio.

**2. Triagem permanece `1:N` com Paciente.** Isso é importante porque agora o dicionário deixa explícito que a data/hora pertence à **aferição**, não ao atendimento. Isso representa corretamente tanto o cenário ambulatorial quanto o acompanhamento dos pacientes intensivos.

Também mantive **nenhuma aferição individual como obrigatória**, mas estabeleci a regra de que uma triagem completamente vazia não deve existir. Isso resolve a aparente contradição que surgiu durante nossa discussão.

Por enquanto eu deixaria este documento **como “Em revisão”**, exatamente como fizemos com os anteriores. Se você encontrar qualquer campo, tipo, obrigatoriedade ou regra que não corresponda ao que definimos, corrigimos antes de transformá-lo no **Dicionário de Dados Consolidado v1.0 oficial**.