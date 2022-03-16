## Configuration in ASP.Net CORE

### Order

- Settings files, such as *appsettings.json*
- Environment variables
- Azure Key Vault
- Azure App Configuration
- Command-line arguments
- Custom providers, installed or created
- Directory files
- In-memory .NET objects

### Manual specification

```csharp
builder.Host.ConfigureAppConfiguration((hostingContext, config) => {
    var env = hostingContext.HostingEnvironment;
    config.AddJsonFile("appsettings.{env.Environment}.json"); // Custom appsettings file

    config.AddEnvironmentVariables(); // Environment Variables

    config.AddUserSecrets<Program>(); // User secrets
})
```

### Usage

```csharp
public class SomeService {
    public SomeService(IConfiguration configuration) { 
        var x = configuration["someKey"];
    }
}
```

### Appsettings.environment.json

```json
{
    "key": "value",
    "key2": "value2"
}
```
