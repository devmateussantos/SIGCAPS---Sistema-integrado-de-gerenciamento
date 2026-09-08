# Dicionário de Dados — Triagem

**Versão:** 1.0  
**Status:** Aprovado para MVP  
**Data:** 2026-08-08

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---:|---|
| id | UUID | Sim | Identificador único. |
| pacienteId | UUID | Sim | Referência ao paciente. |
| dataHoraAfericao | TIMESTAMPTZ | Sim | Momento das aferições. |
| temperatura | DECIMAL(4,1) | Não | Temperatura em °C. |
| peso | DECIMAL(5,1) | Não | Peso em kg. |
| pressaoSistolica | INT | Não | Pressão sistólica. |
| pressaoDiastolica | INT | Não | Pressão diastólica. |
| glicemia | INT | Não | Glicemia em mg/dL. |
| situacaoGlicemia | ENUM/TEXT | Condicional | Jejum, pré-refeição, pós-refeição etc. |
| criadoPorUsuarioId | UUID | Sim | Usuário que criou o registro. |
| alteradoPorUsuarioId | UUID | Não | Usuário da última alteração. |
| criadoEm | TIMESTAMPTZ | Sim | Data/hora de criação. |
| atualizadoEm | TIMESTAMPTZ | Sim | Data/hora da última alteração. |

## Regras
- Sistólica e diastólica devem ser preenchidas juntas.
- `situacaoGlicemia` só existe quando `glicemia` existe.
- Pelo menos uma aferição deve existir.
- A data/hora da triagem é independente da data/hora do atendimento.
- Técnicos de enfermagem e Coordenação podem editar.
- Deve ser possível identificar quem criou e quem alterou o registro.
- Nenhuma aferição individual é obrigatória.
- Uma triagem sem qualquer informação de aferição não deve ser registrada.
- A pressão é armazenada separadamente em sistólica e diastólica.
- O peso possui uma casa decimal.
- A temperatura utiliza graus Celsius.
- A glicemia utiliza mg/dL.