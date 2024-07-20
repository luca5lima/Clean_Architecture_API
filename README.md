# README

## Configuração de Conexão com PostgreSQL

Este documento descreve as mudanças realizadas para configurar a conexão do projeto com um banco de dados PostgreSQL.

### 1. **Arquivo de Configuração (`appsettings.json`)**

No arquivo `appsettings.json`, adicionamos a string de conexão para o PostgreSQL:

```json
{
  "ConnectionStrings": {
    "PostgreSQL": "Server=localhost;Database=host;User ID=user;Password=54321;Port=5432;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
