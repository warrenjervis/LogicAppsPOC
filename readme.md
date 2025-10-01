# Logic Apps POC

This POC is a simple Logic Apps Stateless Workflow, that waits for an HTTP request, connects to a SQL Server database, and returns a list of database names.

## Setup

### SQL Server
If SQL Server is not installed, you can quickly spin up an instance, using Docker:

```sh
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<password>" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest
```

### VS Code
This uses VS Code, to design and debug the Logic App.

1. [Download and install VS Code][vscode].
1. Open the repo in VS Code. 
1. Open Extensions, and ensure all recommended extensions are installed (Open Extensions menu, and type `@recommended` in the search bar):
  ![VS Code Extensions][sc_extensions]

## Running Locally

Open the `LogicAppsPOC.code-workspace` file, and you will see an option to open the workspace. 

Once the workspace is opened, you can view the designer, by expanding the `StatelessPOC` folder, so you can view the `workflow.json` file, and right-clicking the file, and selecting **Open Designer**, from the context menu.

![VS Code Open Designer][sc_opendesigner]

The designer will allow you to edit the workflow.
![VS Code Designer View][sc_designer]

`local.settings.json` should be generated, under the `LogicAppsPOC` folder. Add a `sql_connectionString` setting, under `Values`. Set it to the connection string that should be used, to connect to your instance of SQL Server. The settings file should look similar to the following:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_INPROC_NET8_ENABLED": "1",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "APP_KIND": "workflowapp",
    "ProjectDirectoryPath": "/Users/warrenjervis/repos/LogicAppsPoC/LogicAppsPOC/LogicAppsPOC",
    "WORKFLOWS_SUBSCRIPTION_ID": "",
    "sql_connectionString": "Data Source=localhost;Application Name=Logic Apps;Integrated Security=false;User ID=sa;Password=<password>;Encrypt=true;TrustServerCertificate=true;"
  }
}
```

Once the connection string is set, open the **Run and Debug** tab, and click the button for **Start Debugging**.

![VS Code Debug][sc_debug]

Once it has started, right-click the `workflow.json` file, and select **Overview** from the context menu.
  ![VS Code Open Overview][sc_openoverview]

In the overview, you'll see a URL. You can click the URL, to open it in your browser, or, copy it.
  ![VS Code Overview][sc_overview]

However you decide to make the request, you should see a list of the databases in your SQL Server instance, in the response:
  ![Logic Apps Response][sc_response]



[vscode]:https://code.visualstudio.com/
[sc_extensions]:/screenshots/vscode_extensions.png
[sc_opendesigner]:/screenshots/vscode_opendesigner.png
[sc_designer]:/screenshots/vscode_designer.png
[sc_debug]:/screenshots/vscode_debug.png
[sc_openoverview]:/screenshots/vscode_openoverview.png
[sc_overview]:/screenshots/vscode_overview.png
[sc_response]:/screenshots/response.png