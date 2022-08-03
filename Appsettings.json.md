# Appsettings.json

## Binding to objects

### Bound to the root

```csharp
var builder = Host.CreateDefaultBuilder();

builder.ConfigureServices((context, services) =>
{
    services.AddTransient((serviceProvider) => 
        serviceProvider
            .GetService<IConfiguration>()
            .Get<ConsoleTestConfiguration>());
});
```

### Bound to a section

```csharp
var builder = Host.CreateDefaultBuilder();

builder.ConfigureServices((context, services) =>
{
    services.AddTransient((serviceProvider) => 
        serviceProvider
            .GetService<IConfiguration>()
            .GetSection("SectionName")
            .Get<ConsoleTestConfiguration>());
});
```

## Environment dependant publish & loading

Only load and publish the correct appsettings file without the need to merge appsettings using SlowCheetah or similar

### launchSettings.json

```json
{
  "profiles": {
    "Debug": {
      "commandName": "Project",
      "environmentVariables": {
        "DOTNET_ENVIRONMENT": "Debug"
      }
    },
    "Release": {
      "commandName": "Project",
      "environmentVariables": {
        "environment": "Release"
      }
    }
  }
}
```

### initialization

`using Microsoft.Extensions.Configuration;`

```csharp
// Load the appsettings file for the hosting environment
builder.ConfigureAppConfiguration((context, appConfiguration) =>
{
    var env = context.HostingEnvironment;
    appConfiguration.AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true);
});
```

### .csproj

```xml
  <ItemGroup>
    <None Update="appsettings.Debug.json">
      <DependentUpon>appsettings.json</DependentUpon>
      <CopyToOutputDirectory Condition="$(Configuration)=='Debug'">PreserveNewest</CopyToOutputDirectory>
    </None>

    <None Update="appsettings.Release.json">
      <DependentUpon>appsettings.json</DependentUpon>
      <CopyToOutputDirectory Condition="$(Configuration)=='Release'">PreserveNewest</CopyToOutputDirectory>
    </None>
  </ItemGroup>
```
