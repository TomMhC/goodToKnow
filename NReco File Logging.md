## NReco File Logging

### Package

`<PackageReference Include="NReco.Logging.File" Version="1.1.2" />`

### Specification

```csharp
Host.CreateDefaultBuilder(args)
.ConfigureServices((context, services) => {
    var logPath = @"C:\Temp\logs";
    services.AddLogging(builder => {
        builder.AddConsole();
        builder.AddFile(
            IO.Path.Combine(logPath, $"{DateTime.Now.ToString("yyyy-MM-dd")}.log")
),
            options => {
                options.MinLevel = LogLevel.Debug;
                options.Append = true;
                options.FormatLogEntry = (msg) => {
                    return $"{DateTime.Now.ToString("yy-MM-dd HH:mm ss.ff")} {msg.LogLevel} {msg.Message}";
                }
            }
        });
    });
```
