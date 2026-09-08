
## Um ponto importante para nossa revisão

Introduzi propositalmente **`AtividadeGrupoParticipante`** neste documento.

Isso **não contradiz nossa decisão anterior de não criar uma nova entidade de domínio**. No modelo de domínio continuamos tendo apenas:

> **AtividadeGrupo ↔ Paciente**

Mas, no modelo de dados, um relacionamento **N:N precisa ser materializado** de alguma forma. Portanto, no banco teremos uma estrutura associativa para guardar, por exemplo:

```text
atividadeGrupoId | pacienteId
-----------------|-----------
1                | 15
1                | 23
1                | 31