---
title: Adding Correlation to Logs in Isolated Azure Functions
date: 2024-05-17T14:31:05+07:00
description: Adding Correlation to Logs in Isolated Azure Functions
---

In distributed systems, tracing requests and understanding the flow of operations across different components is crucial. Adding correlation to logs helps in achieving this by linking related telemetry data. In this article, we’ll explore how to add and manage correlation in isolated Azure Functions using Application Insights.
## Prerequisites
1. ****Azure Function App****: Ensure you have an Azure Function App deployed in your Azure subscription.2. ****Application Insights****: Make sure Application Insights is enabled for your Azure Function App.
## Step 1: Enable Application Insights
First, ensure that Application Insights is set up for your Azure Function App.
1. ****Navigate to your Function App**** in the Azure portal.2. Select ****Application Insights**** in the left-hand menu.3. If not already configured, enable Application Insights and link it to your Function App.
## Step 2: Install Application Insights SDK for Isolated Functions
To use Application Insights in your isolated Azure Function, install the necessary NuGet packages.
```shdotnet add package Microsoft.ApplicationInsightsdotnet add package Microsoft.ApplicationInsights.WorkerServicedotnet add package Microsoft.Extensions.Logging.ApplicationInsights```
## Step 3: Configure Application Insights in Your Function
In an isolated Azure Function, you configure Application Insights in the `Program.cs` file.
### Example `Program.cs`:
```csharpusing Microsoft.ApplicationInsights.Extensibility;  using Microsoft.Extensions.DependencyInjection;  using Microsoft.Extensions.Hosting;    public class Program  {      public static void Main(string[] args)      {                var host = new HostBuilder()              .ConfigureFunctionsWorkerDefaults()              .ConfigureServices((context, services) =>              {                  services.AddApplicationInsightsTelemetryWorkerService();              })            .ConfigureServices((hostContext, services) =>              {                  services.AddApplicationInsightsTelemetryWorkerService();                  services.ConfigureFunctionsApplicationInsights();              })            .ConfigureLogging((hostContext,logging) =>              {                  logging.Services.Configure<LoggerFilterOptions>(options =>                  {                      LoggerFilterRule defaultRule = options.Rules.FirstOrDefault(rule => rule.ProviderName                          == "Microsoft.Extensions.Logging.ApplicationInsights.ApplicationInsightsLoggerProvider");                        if (defaultRule is not null)                      {                        options.Rules.Remove(defaultRule);                      }                });                  var configuration = hostContext.Configuration.GetSection("Logging");                  logging.ClearProviders();                  logging.AddApplicationInsights();                  // Apply logging configuration from appsettings.json                  logging.AddConfiguration(configuration);              }).Build();            host.Run();      }}```You will need to also configure the log configuration in appsettings.json```json{  "Logging": {    "LogLevel": {      "Default": "Debug",      "Function": "Trace",      "Microsoft": "Warning"    }  },
  "ApplicationInsights": {    "LogLevel": {      "Default": "Debug"    }  }}```
## Step 4: Add Correlation to Logs (Optional)
All the log lines will be automatically have Opereation Id as Correlation Id. You do not need to do anything to add the Correlation Id when call \_logger.Log. You can go directly to Step 5 without any problem.In isolated Azure Functions, you can manually add correlation information to your logs using `TelemetryClient`. Here’s how you can do it:
### Example Function Class:
```csharpusing Microsoft.ApplicationInsights;using Microsoft.ApplicationInsights.DataContracts;using Microsoft.Azure.Functions.Worker;using Microsoft.Azure.Functions.Worker.Http;using Microsoft.Extensions.Logging;
public class MyFunction{    private readonly TelemetryClient _telemetryClient;    private readonly ILogger<MyFunction> _logger;
    public MyFunction(TelemetryClient telemetryClient, ILogger<MyFunction> logger)    {        _telemetryClient = telemetryClient;        _logger = logger;    }
    [Function("MyFunction")]    public async Task<HttpResponseData> RunAsync(        [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req)    {        var operationId = req.FunctionContext.TraceContext.TraceParent.TraceId;        var parentId = req.FunctionContext.TraceContext.TraceParent.ParentId;
        // Log a custom event with correlation        var telemetry = new EventTelemetry("CustomEvent")        {            Context =            {                Operation =                {                    Id = operationId,                    ParentId = parentId                }            }        };
        _telemetryClient.TrackEvent(telemetry);
        _logger.LogInformation($"OperationId: {operationId}, ParentId: {parentId}");
        // Your function logic here
        var response = req.CreateResponse();        response.StatusCode = System.Net.HttpStatusCode.OK;        await response.WriteStringAsync("Hello, world!");
        return response;    }}```
In this example, `TelemetryClient` is used to log a custom event with correlation information. The `operationId` and `parentId` are extracted from the `HttpRequestData` and included in the telemetry.
## Step 5: Verify Correlation in Azure Portal
After deploying your Azure Function, you can verify the correlation in the Azure portal:
1. ****Go to your Application Insights resource****.2. ****Navigate to the **Transaction Search** or **End-to-End Transaction Details**:**   - You should see correlated telemetry items grouped by operation IDs.3. ****Use the **Application Map** to visualize the end-to-end flow of requests across services****.
## Additional Tips
- ****Custom Telemetry****: For non-.NET languages or custom telemetry, you can manually add correlation IDs to your logs and telemetry items.- ****HTTP Headers****: Ensure that your services pass correlation headers (`Request-Id` and `Correlation-Context`) along with HTTP requests to maintain correlation across services.
By following these steps, you can add and manage correlation in your isolated Azure Functions, ensuring that you have a clear view of the flow of operations across your distributed system. This will help in diagnosing issues and understanding the interactions between different components in your application.
