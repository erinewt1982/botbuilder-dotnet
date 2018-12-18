# Azure Template for Bot Analytics Dashboard

## Background on Azure Dashboards
We are creating an Azure Dashboard.  This is also what Application Insights uses for their dashboards.

Look at [create a template from the json](https://docs.microsoft.com/en-us/azure/azure-portal/azure-portal-dashboards-create-programmatically#create-a-template-from-the-json) documentation for details on how the contents of the template works, but essentially you name variables and replace when deploying.

## Parameters
We define three parameters for our template.
```json
"parameters": {
    "insightsComponentName": {
      "type": "string"
    },
    "insightsComponentResourceGroup": {
      "type": "string"
    },
    "dashboardName": {
      "type": "string"
    }
  }
```

## Testing
Easiest way to test is using [Azure portal's template deployment page](https://portal.azure.com/#create/Microsoft.Template).  
- Click ["Build your own template in the editor"]
- Copy and Paste
- Click "Save"
- Populate `Basics`: 
   - Subscription: <your test subscription>
   - Resource group: <a test resource group>
   - Location: <such as West US>
- Populate `Settings`:
   - Insights Component Name: <like `core672so2hw`>
   - Insights Component Resource Group: <like `core67'>
   - Dashboard Name:  <like `'Bot Analytics Dashboard'>
- Click `I agree to the terms and conditions stated above`
- Click `Purchase`
- Validate
   - Click on [`Resource Groups`](https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups)
   - Select your Resource Group from above (like `core67`).
   - If you don't see a new Resource, then look at "Deployments" and see if any have failed.
   - Here's what you typically see for failures:
```json
{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/arm-debug for usage details.","details":[{"code":"BadRequest","message":"{\r\n \"error\": {\r\n \"code\": \"InvalidTemplate\",\r\n \"message\": \"Unable to process template language expressions for resource '/subscriptions/45d8a30e-3363-4e0e-849a-4bb0bbf71a7b/resourceGroups/core67/providers/Microsoft.Portal/dashboards/Bot Analytics Dashboard' at line '34' and column '9'. 'The template parameter 'virtualMachineName' is not found. Please see https://aka.ms/arm-template/#parameters for usage details.'\"\r\n }\r\n}"}]}
```