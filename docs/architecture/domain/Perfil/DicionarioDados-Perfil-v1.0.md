# Dicionário de Dados — Perfil

| Campo | Tipo | Obrigatório | Regra |
|--------|------|-------------|-------|
| id | UUID | Sim | Gerado automaticamente|
| nome | VARCHAR(100) | Sim | Único |
| descricao | TEXT | Não | Opcional |
| criadoEm | TIMESTAMPTZ | Sim | Auditoria |