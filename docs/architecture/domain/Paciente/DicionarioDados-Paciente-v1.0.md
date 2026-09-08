# Dicionário de Dados — Paciente

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Gerado automaticamente |
| nome | VARCHAR(150) | Sim | Nome completo |
| nomeSocial | VARCHAR(150) | Não | Opcional |
| sexo | ENUM | Sim | Sexo ao qual o paciente se identifica. |
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
| queixaPrincipal | TEXT | Sim | Relato comportamental do paciente |
| informacoesEncaminhamento | TEXT | Não | Informações referentes à requisição de encaminhamento apresentada no primeiro cadastro |
| status | ENUM | Sim | ATIVO/INATIVO |
| motivoInativacao | TEXT | Condicional | Obrigatório quando INATIVO |
| tipoPaciente | ENUM | Sim | AMBULATORIAL/INTENSIVO |
| criadoEm | TIMESTAMPTZ | Sim | Data e hora da criação |
| atualizadoEm | TIMESTAMPTZ | Sim | Atualizado automaticamente |

## Regras

- Pacientes não são excluídos.
- A inativação não remove o histórico do paciente.
- `motivoInativacao` é obrigatório quando `status` for `INATIVO`.
- A idade não é armazenada; é calculada a partir de `dataNascimento`.
- O endereço permanece simplificado no MVP.
- As informações do encaminhamento podem ser preservadas.