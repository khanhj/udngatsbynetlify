---
title: Configuring Logging for Isolated Azure Functions
date: 2024-04-03T12:49:29+07:00
description: Configuring Logging for Isolated Azure Functions
---




Logging is a critical aspect of monitoring and troubleshooting your Azure Functions. In isolated Azure Functions, logging can be configured using the `appsettings.json` file and the logging services provided by the .NET SDK. This article will guide you through setting up logging for isolated Azure Functions.





## Step 1: Create or Update `appsettings.json`





First, ensure that your Azure Functions project has an `appsettings.json` file. This file is used to configure various settings, including logging levels.





### Example `appsettings.json`:





```json

{

  "Logging": {

    "LogLevel": {

      "Default": "Information",

      "Function": "Information",

      "Microsoft": "Warning"

    }

  },

  "ApplicationInsights": {

    "ConnectionString": "InstrumentationKey=your-instrumentation-key;IngestionEndpoint=https://<region>.in.applicationinsights.azure.com/"

  }

}

```





In this example:

- The `LogLevel` section defines the minimum log level for different categories. You can adjust these as needed:

  - `Default` applies to all categories.

  - `Function` applies to the Azure Functions logs.

  - `Microsoft` applies to logs from Microsoft libraries.





- The `ApplicationInsights` section configures Application Insights for telemetry. Replace `your-instrumentation-key` and `<region>` with your actual Application Insights instrumentation key and region.





## Step 2: Modify `Program.cs`





Next, configure logging in your `Program.cs` file. This is where you set up the host builder and configure services.





### Example `Program.cs`:





```csharp

using Microsoft.Extensions.Configuration;

using Microsoft.Extensions.Hosting;

using Microsoft.Extensions.Logging;

using Microsoft.ApplicationInsights.Extensibility;

using Microsoft.ApplicationInsights.WorkerService;





public class Program

{

    public static void Main(string[] args)

    {

        var host = new HostBuilder()

            .ConfigureAppConfiguration((hostingContext, config) =>

            {

                config.AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)

                      .AddEnvironmentVariables();

            })

            .ConfigureFunctionsWorkerDefaults()

            .ConfigureLogging((context, logging) =>

            {

                var configuration = context.Configuration.GetSection("Logging");

                logging.ClearProviders();

                logging.AddConsole();

                logging.AddApplicationInsights();





                // Apply logging configuration from appsettings.json

                logging.AddConfiguration(configuration);

            })

            .ConfigureServices((context, services) =>

            {

                services.AddApplicationInsightsTelemetryWorkerService(

                    options => options.ConnectionString = context.Configuration["ApplicationInsights:ConnectionString"]);

            })

            .Build();





        host.Run();

    }

}

```





### Explanation:





- **ConfigureAppConfiguration**: Adds the `appsettings.json` and environment variables to the configuration.

- **ConfigureFunctionsWorkerDefaults**: Configures default settings for Azure Functions.

- **ConfigureLogging**: Sets up logging providers and configurations:

  - Clears existing providers.

  - Adds console logging.

  - Adds Application Insights logging.

  - Applies logging configuration from `appsettings.json`.

- **ConfigureServices**: Adds Application Insights telemetry services using the connection string from `appsettings.json`.





## Step 3: Deploy and Monitor





Once you have configured your logging, deploy your Azure Functions to Azure. You can monitor your logs in the Azure portal under **Monitor** > **Logs** and in your Application Insights resource.





## No ConnectionString





If you prefer not to specify the `ConnectionString` in your configuration files, you can rely on environment variables or Azure-managed service identities to automatically configure Application Insights.





### Using Environment Variables:





1. **Set the `APPLICATIONINSIGHTS_CONNECTION_STRING` environment variable in your Azure Function App settings.**





#### In Azure Portal:





- Navigate to your Azure Function App.

- Go to **Configuration** under the **Settings** section.

- Click on **New application setting**.

- Add the key `APPLICATIONINSIGHTS_CONNECTION_STRING` and set its value to your Application Insights connection string.





### Example `Program.cs` Without ConnectionString:





In this scenario, you don't need to set the connection string in your `appsettings.json` or `Program.cs`. The SDK will automatically pick up the environment variable.





```csharp

using Microsoft.Extensions.Configuration;

using Microsoft.Extensions.Hosting;

using Microsoft.Extensions.Logging;

using Microsoft.ApplicationInsights.Extensibility;

using Microsoft.ApplicationInsights.WorkerService;





public class Program

{

    public static void Main(string[] args)

    {

        var host = new HostBuilder()

            .ConfigureAppConfiguration((hostingContext, config) =>

            {

                config.AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)

                      .AddEnvironmentVariables();

            })

            .ConfigureFunctionsWorkerDefaults()

            .ConfigureLogging((context, logging) =>

            {

                var configuration = context.Configuration.GetSection("Logging");

                logging.ClearProviders();

                logging.AddConsole();

                logging.AddApplicationInsights();





                // Apply logging configuration from appsettings.json

                logging.AddConfiguration(configuration);

            })

            .ConfigureServices((context, services) =>

            {

                // No need to explicitly set the connection string here

                services.AddApplicationInsightsTelemetryWorkerService();

            })

            .Build();





        host.Run();

    }

}

```





### Explanation:





- The `ApplicationInsightsTelemetryWorkerService` will automatically use the `APPLICATIONINSIGHTS_CONNECTION_STRING` environment variable if it is set in the Azure Function App settings.





## Additional Tips:





- **Local Development**: Ensure you have the correct settings in `local.settings.json` for local development. You can set the `APPLICATIONINSIGHTS_CONNECTION_STRING` environment variable in your development environment as well.

- **Environment Variables**: Use environment variables for sensitive information like the Application Insights connection string.

- **Log Levels**: Adjust log levels in `appsettings.json` to control the verbosity of logs.





### Example `local.settings.json` for Local Development:





```json

{

  "IsEncrypted": false,

  "Values": {

    "AzureWebJobsStorage": "UseDevelopmentStorage=true",

    "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated",

    "APPLICATIONINSIGHTS_CONNECTION_STRING": "your-connection-string"

  },

  "Logging": {

    "LogLevel": {

      "Default": "Debug",

      "Function": "Debug",

      "Microsoft": "Information"

    }

  }

}

```





## Conclusion





Configuring logging for isolated Azure Functions involves setting up your `appsettings.json` for logging levels and Application Insights, modifying your `Program.cs` to configure logging services, and deploying your function app. If you prefer not to include the connection string in your configuration files, you can leverage environment variables to securely manage your Application Insights configuration. This setup allows you to effectively monitor and troubleshoot your functions using the Azure portal and Application Insights.
