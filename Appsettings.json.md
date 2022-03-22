

## Appsettings.json

Only load and publish the correct appsettings file without the need to merge appsettings using SlowCheetah or similar

### initialization

`using Microsoft.Extensions.Configuration;`

```csharp
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


