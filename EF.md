## EF

### EF project referenties:

EF Core
`<PackageReference Include="Microsoft.EntityFrameworkCore" Version="5.0.11" />`
EF Migrations
`<PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="5.0.11" />`
SQL Server
`<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="5.0.11" />`
Om een default value te definieren voor de ID kolom
`<PackageReference Include="Microsoft.EntityFrameworkCore.Relational" Version="5.0.11" />`

### Project configuratie:

In het exe project moet opgegeven worden dat het Migrations project niet gelijk is aan het EF project. Dit in de connectionstring:

```csharp
    services.AddDbContext<EF.Context>(
        builder => builder.UseSqlServer(
            context.Configuration["ConnectionString"], 
            options => options.MigrationsAssembly("TestEFMigrations")));
```

### Console:

vanuit de directory van de exe:

```console
    > dotnet tool install --global dotnet-ef
    > dotnet ef migrations add init
    > dotnet ef database update
    > dotnet ef migrations add defaultId
    > dotnet ef database update
```

### In geval van een apart project voor de migrations:

Aanpassen in exe project:
    `options => options.MigrationsAssembly("Migrations")`
en
    `> dotnet ef migrations add init -p ..\Migrations`
