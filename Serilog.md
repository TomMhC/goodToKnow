# Serilog

## Packages

```xml
    <!-- Application -->
    <PackageReference Include="Serilog" Version="2.11.0" />
    <!-- Web application -->    
    <PackageReference Include="Serilog.AspNetCore" Version="5.0.0" />
    <!-- Extensions-->
    <PackageReference Include="Serilog.Exceptions" Version="8.2.0" />
    <PackageReference Include="Serilog.Extensions.Logging" Version="3.1.0" />
    <!-- Sinks -->
    <PackageReference Include="Serilog.Sinks.Console" Version="4.0.1" />
    <PackageReference Include="Serilog.Sinks.EventLog" Version="3.1.0" />
    <PackageReference Include="Serilog.Sinks.File" Version="5.0.0" />    
    <PackageReference Include="Serilog.Sinks.MariaDB" Version="1.0.1" />
```

## Configuration

### Application

```csharp
hostbuilder
.ConfigureLogging((context, logging) =>
    {
        var path = context.Configuration["LogPath"];

        Log.Logger = new LoggerConfiguration()
                .MinimumLevel.Override("Microsoft", LogEventLevel.Warning)
                .Enrich.FromLogContext()
                .WriteTo.Console()
                .WriteTo.EventLog("GZABasicsExportHix")
                .WriteTo.File(Path.Combine(path, $"{DateTime.Now:yyyy-MM-dd}.log"), rollingInterval: RollingInterval.Day)
                .CreateLogger();

        logging.ClearProviders();
        logging.AddSerilog();
    })
```

### WebApplication

```csharp
var host = CreateHostBuilder(args).Build();

host.InitDatabase();    

Log.Logger = CreateLoggerConfig()
   .WriteTo.MariaDB(
       connectionString: host.Services.GetRequiredService<IConfiguration>().GetDatabaseConnectionString(),
       tableName: "Logs",
       autoCreateTable: true,
       options: new Serilog.Sinks.MariaDB.MariaDBSinkOptions() { })
   .CreateLogger();
```

```csharp
CreateHostBuilder()
...
UseSerilog()
...
```


