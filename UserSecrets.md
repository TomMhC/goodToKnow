## User Secrets

### Referenties:

Om eender welke configuration properties op te vragen:
`<PackageReference Include="System.Configuration.ConfigurationManager" Version="5.0.0" />`
Zodat user sercrets geladen kunnen worden:
`<PackageReference Include="Microsoft.Extensions.Configuration.UserSecrets" Version="5.0.0" />`

### Configuration:

Om een onderscheid te kunnen maken tussen DEV en PROD environment in console applicatie wordt het project gestart met parameters:
    `--environment Development`
Dit geeft launch settings:

```json
{
  "profiles": {
    "TestEFMigrations": {
      "commandName": "Project",
      "commandLineArgs": "--environment Development"
    }
  }
}
```

### User secrets toevoegen:

Het maken van de HostBuilder kan dan als volgt uitgebreid worden:

```csharp
    Host.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((context, builder) =>
            {
                if (context.HostingEnvironment.IsDevelopment()) 
                    builder.AddUserSecrets<Program>();
            })
```

### User secret consumen vanuit console app:

```Csharp
services.AddDbContext<EF.Context>(
    builder => builder.UseSqlServer(
        context.Configuration["ConnectionString"], 
        options => options.MigrationsAssembly("TestEFMigrations")));
```