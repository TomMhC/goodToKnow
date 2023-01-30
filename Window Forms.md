# Window Forms

## Program.cs

```c#
internal static class Program
{
    /// <summary>
    ///  The main entry point for the application.
    /// </summary>
    [STAThread]
    static void Main()
    {
        ApplicationConfiguration.Initialize();

        var services = new ServiceCollection();

        ConfigureServices(services);

        using var serviceProvider = services.BuildServiceProvider();
        var frmMain = serviceProvider.GetRequiredService<FrmMain>();
        Application.Run(frmMain);
    }

    private static void ConfigureServices(ServiceCollection services)
    {
        services.AddScoped<FrmMain>();
    }
}
```


            

