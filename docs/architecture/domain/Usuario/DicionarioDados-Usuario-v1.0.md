# Dicionário de Dados — Usuario

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Gerado automaticamente |
| nome | VARCHAR(150) | Sim | Nome completo |
| cpf | VARCHAR(11) | Sim | Único |
| email | VARCHAR(150) | Sim | Único |
| telefone | VARCHAR(20) | Não | Opcional |
| login | VARCHAR(50) | Sim | Único |
| senhaHash	| VARCHAR(255) | Sim | Nunca armazenar senha em texto |
| perfilId | UUID | Sim | FK para Perfil |
| ativo | BOOLEAN |	Sim | Usuário ativo/inativo |
| ultimoLogin | TIMESTAMPTZ | Não	Atualizado automaticamente |
| criadoEm | TIMESTAMPTZ |	Sim | Auditoria |
| atualizadoEm | TIMESTAMPTZ |	Sim | Auditoria |
| matricula	| VARCHAR (30) | não | Identificação interna do servidor, caso a unidade utilize esse controle |