# Modelo de Domínio — Triagem

**Versão:** 1.0  
**Status:** Aprovado para MVP  
**Data:** 2026-08-08  
**Projeto:** SIGCAPS

## Objetivo
Registrar as aferições realizadas durante a triagem do paciente, preservando o momento da coleta e os responsáveis pelo registro.

No MVP, a Triagem será utilizada no fluxo ambulatorial associado à chegada do paciente para atendimento agendado. O acompanhamento não obrigatório de pacientes intensivos será evolução futura.

## Dados aferidos
- Temperatura em °C.
- Peso em kg, com uma casa decimal.
- Pressão arterial sistólica e diastólica.
- Glicemia em mg/dL.
- Situação da coleta da glicemia.

## Regras de Negócio
- **RN-043:** Uma Triagem pertence a exatamente um Paciente.
- **RN-044:** `dataHoraAfericao` representa o momento das aferições e é independente de `dataHoraAtendimento`.
- **RN-045:** Nenhuma aferição individual é obrigatória.
- **RN-046:** Uma Triagem deve possuir pelo menos uma aferição registrada; não deve existir uma Triagem vazia.
- **RN-047:** Pressão sistólica e diastólica são INT separados e devem ser informados em conjunto.
- **RN-048:** Glicemia é opcional; quando informada, sua situação/momento de coleta deve ser registrada.
- **RN-049:** Temperatura é registrada em °C.
- **RN-050:** Peso é registrado em kg com uma casa decimal.
- **RN-051:** Glicemia é registrada em mg/dL como INT.
- **RN-052:** Triagens podem ser editadas.
- **RN-053:** A edição é permitida a Técnicos(as) de Enfermagem ou Coordenação.
- **RN-054:** Devem ser registrados `criadoPorUsuarioId` e `alteradoPorUsuarioId`.

## Relacionamentos
- Paciente 1:N Triagem.
- Usuário 1:N Triagem como criador.
- Usuário 1:N Triagem como responsável pela última alteração.
- Não há relação direta Triagem → Atendimento no MVP.

## Decisões
- Não haverá tipo AMBULATORIAL/INTENSIVO em Triagem.
- O acompanhamento diário de intensivos fica no backlog.
- Os campos de aferição são opcionais individualmente.
- Uma Triagem vazia não é válida.
