## ConsoleApps

### Project referenties

 `<PackageReference Include="Microsoft.Extensions.Hosting" Version="5.0.0" />`

### Method om Host te creëren

```csharp
private static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
    .ConfigureServices((context, services) =>
    {
        services.AddTransient<ConsoleTest>();
    });
```

### Main aanpassen om Host te gebruiken

Er moet een scope worden aangemaakt waarbinnen de andere services aangemaakt kunnen worden die aan 'ConsoleTest' moeten toegekend worden:

```csharp
static void Main(string[] args)
{
    var host = CreateHostBuilder(args).Build();

    using var scope = host.Services.CreateScope();

    var consoleTest = scope.ServiceProvider.GetRequiredService<ConsoleTest>();

    consoleTest.Run();
}
```
