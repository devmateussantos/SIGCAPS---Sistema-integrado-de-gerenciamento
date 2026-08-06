# Dicionário de Dados — Paciente

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Gerado automaticamente |
| nome | VARCHAR(150) | Sim | Nome completo |
| nomeSocial | VARCHAR(150) | Não | Opcional |
| sexo | ENUM | Sim | Masculino/Feminino/Outro/Não informado |
| cpf | VARCHAR(11) | Sim | Único |
| cartaoSus | VARCHAR(15) | Sim | Único |
| dataNascimento | DATE | Sim | Utilizada para cálculo automático da idade |
| telefonePrincipal | VARCHAR(20) | Sim | Aceita máscara no Frontend |
| telefoneSecundario | VARCHAR(20) | Não | Opcional |
| logradouro | VARCHAR(150) | Sim | Endereço |
| numero | VARCHAR(10) | Sim | Endereço |
| bairro | VARCHAR(80) | Sim | Endereço |
| cidade | VARCHAR(80) | Sim | Endereço |
| estado | CHAR(2) | Sim | UF |
| cep | VARCHAR(8) | Sim | Armazenado sem máscara |
| nomeMae | VARCHAR(150) | Não | Opcional |
| nomePai | VARCHAR(150) | Não | Opcional |
| responsavelLegal | VARCHAR(150) | Não | Opcional |
| queixaPrincipal | TEXT | Sim | Motivo da admissão |
| status | ENUM | Sim | ATIVO/INATIVO |
| motivoInativacao | TEXT | Não | Obrigatório quando INATIVO |
| tipoPaciente | ENUM | Sim | AMBULATORIAL/INTENSIVO |
| criadoEm | TIMESTAMPTZ | Sim | Data e hora da criação |
| atualizadoEm | TIMESTAMPTZ | Sim | Atualizado automaticamente |