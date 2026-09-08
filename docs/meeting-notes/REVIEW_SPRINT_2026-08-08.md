# Revisão da Sprint — Atendimento e Triagem

**Data:** 2026-08-08

## Atendimento
- Todo atendimento nasce de um Agendamento.
- Um Agendamento gera no máximo um Atendimento.
- O horário efetivo é registrado em `dataHoraAtendimento`.
- Falta pertence ao Agendamento.
- Cada profissional gera seu próprio Atendimento.
- Edição: profissional responsável ou Coordenação.
- Paciente e profissional não são duplicados em Atendimento no MVP.

## Triagem
- Pertence diretamente ao Paciente.
- Possui data/hora própria.
- Nenhum campo de aferição é individualmente obrigatório.
- Deve possuir ao menos uma aferição para não ser um registro vazio.
- Pressão: sistólica/diastólica em INT separados.
- Peso: uma casa decimal.
- Temperatura: °C.
- Glicemia: INT em mg/dL.
- Situação da glicemia é condicional.
- Técnicos(as) de Enfermagem e Coordenação podem editar.
- Criação e alteração são auditadas.

## Ponto de atenção
A resposta “nenhum campo obrigatório” foi reconciliada com “não existe Triagem sem informação”: os campos individuais são opcionais, mas o registro como um todo exige ao menos uma aferição.
