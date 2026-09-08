# Dicionário de Dados — Usuario

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Gerado automaticamente |
| nome | VARCHAR(150) | Sim | Nome completo |
| cpf | VARCHAR(11) | Sim | Único |
| login | VARCHAR(50) | Sim | Único |
| senhaHash	| VARCHAR(255) | Sim | Nunca armazenar senha em texto |
| perfilId | UUID | Sim | FK para Perfil |
| ativo | BOOLEAN |	Sim | Usuário ativo/inativo |
| ultimoLogin | TIMESTAMPTZ | Não	Atualizado automaticamente |
| criadoEm | TIMESTAMPTZ |	Sim | Auditoria |
| atualizadoEm | TIMESTAMPTZ |	Sim | Auditoria |
| matricula	| VARCHAR (30) | Não | Identificação interna do servidor, caso a unidade utilize esse controle |

### Regras

- Cada usuário possui um único perfil no MVP.
- O perfil determina suas permissões.
- A matrícula não é obrigatória.
- Usuários inativos não devem acessar o sistema.