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
```
### 2. Classe de Extensão de Serviço (ServiceExtensions.cs)

No arquivo ServiceExtensions.cs, configuramos o serviço para utilizar o banco de dados PostgreSQL.

```csharp
public static class ServiceExtensions
{
    public static void ConfigurePersistenceApp(this IServiceCollection services,
                                                IConfiguration configuration)
    {
        var connectionString = configuration.GetConnectionString("PostgreSQL");
        services.AddDbContext<AppDbContext>(opt => opt.UseNpgsql(connectionString));

        services.AddScoped<IUnitOfWork, UnitOfWork>();
        services.AddScoped<IUserRepository, UserRepository>();
    }
}

```
ConfigurePersistenceApp: Método de extensão que configura os serviços necessários para a persistência de dados.

GetConnectionString("PostgreSQL"): Obtém a string de conexão do arquivo de configuração.

AddDbContext<AppDbContext>: Configura o contexto do banco de dados para usar o PostgreSQL com a string de conexão fornecida.

AddScoped<IUnitOfWork, UnitOfWork> e AddScoped<IUserRepository, UserRepository>: Adiciona as injeções de dependência para UnitOfWork e UserRepository.
