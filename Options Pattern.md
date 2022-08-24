# Options Pattern

## Why the Options Pattern over regular IConfiguration?

IOptionsFactory<TOptions> can be overridden to supply a separate configuration value for testing

## Code

### Startup

```csharp
builder.ConfigureServices((context, services) =>
{
   services.Configure<ConsoleTestConfiguration>(
        context.Configuration.GetSection(
            ConsoleTestConfiguration.SectionName));
});
```

### Usage

```csharp
internal class ConsoleTest
{
    private ConsoleTestConfiguration _configuration;

    public ConsoleTest(IOptions<ConsoleTestConfiguration> options)
    {
        _configuration = options.Value;
    }
}
```

### Configuration class

```csharp
internal class ConsoleTestConfiguration
{
   public const string SectionName = "Section";
   public string Sleutel { get; set; }
}
```
