---
title: How to Edit the host.json File for Azure Functions and Deploy Changes
date: 2024-05-30T12:49:29+07:00
description: How to Edit the host.json File for Azure Functions and Deploy Changes
---
Editing the `host.json` file for an Azure Function doesn't necessarily require you to go to the Azure portal. You can edit this file locally in your development environment and then deploy the changes to Azure. Here’s how you can do it:





### 1. **Edit `host.json` Locally**





The `host.json` file is typically found in the root directory of your Azure Functions project. You can open this file in your preferred code editor and make the necessary changes.





#### Example `host.json` Configuration:

```json

{

  "version": "2.0",

  "logging": {

    "logLevel": {

      "default": "Trace",

      "Function": "Trace"

    },

    "applicationInsights": {

      "samplingSettings": {

        "isEnabled": false

      }

    }

  }

}

```

In this example:





- The `logLevel` setting is configured to capture `Trace` level logs for detailed logging.

- `samplingSettings` is set to `false` to ensure that all telemetry data is sent to Application Insights without sampling.





### 2. **Deploy Changes to Azure**





After editing the `host.json` file locally, you need to deploy your changes to Azure. The deployment process can vary depending on your workflow, but common methods include:





#### Using Azure Functions Core Tools:

1. **Build and Deploy**:

    ```sh

    func azure functionapp publish <your-function-app-name>

    ```





#### Using Visual Studio:

1. **Right-click your project** in Solution Explorer.

2. Select **Publish**.

3. Follow the prompts to deploy your project to Azure.





#### Using GitHub Actions or Azure Pipelines:

If you have CI/CD pipelines set up, commit your changes and push them to your repository. Your pipeline will handle the deployment.





### 3. **Verify Changes in Azure Portal**





After deploying, you can verify that your changes have been applied by checking the Application Insights logs in the Azure portal.





#### Steps to Verify:

1. **Go to your Azure Function App** in the Azure portal.

2. **Navigate to Application Insights**:

   - Select the **Application Insights** resource linked to your Function App.

3. **Check Logs**:

   - Go to **Logs** under the **Monitoring** section.

   - Run queries to ensure your detailed logging is being captured.





### Additional Tips





- **Local Testing**: You can also run and test your Azure Functions locally using Azure Functions Core Tools. This allows you to see the effects of changes in the `host.json` file before deploying.

    ```sh

    func start

    ```

- **Documentation**: Refer to the [Azure Functions host.json reference](https://docs.microsoft.com/en-us/azure/azure-functions/functions-host-json) for more detailed information on available settings and configurations.





By following these steps, you can edit the `host.json` file locally and deploy the changes to Azure, ensuring that your Azure Functions are configured correctly for detailed trace logging.
