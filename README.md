# Contain Yourself: Containers and Serverless

## Prereq's

### Install Docker on MacOS

https://docs.docker.com/get-docker/

## The Basics & Review for Some: 

### Hello World 

**Download Docker Image and Run It**

```
docker run -p 8888:80 mackhendricks/static-site
```

**Open a web browswer and point to** 

http://localhost:8888

**Kill/Stop the Image**

Enter Control-C

**Run the container in the background**

```
docker run -d -p 8888:80 mackhendricks/static-site
```

Docker will generated a container ID.  It will look something lke this

```
3ba42b3f8366e00bf8866b3b863eb3228d97090c81488648d60da5bab00e203
```
**Open a web browswer and point to** 

http://localhost:8888

**Lets look at the running image**

```
docker ps
```

It only shows you the first 12 digits of the image id for readability purposes

### Inspect Hello World Container


### Build Our Own

Use Case: 

We have an application the will be built by a team of 5 people. The development team has selected Python and they have a set of dependencies that should be installed in each persons development environment.

- Step 1: Figure out the base image
- Step 2: Setup Python and the Requirements file
- Step 3: Setup ENV variables to allow developers to provide state to the container and/or enable the deployment pipeline
- Step 4: Configure it so that the development team can mount their instance of the repo into the container

## Push IT

## Deploy IT 

## Why Do Any of This? Go Serverless!
Create a function that responds to HTTP requests. After running the code locally, deploy it to Azure's serverless platform.
### Prereq's
- [An Azure Account](https://azure.microsoft.com/en-us/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio- )
- [The Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
- [Azure Functions Core Tools version 3.x](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=macos%2Ccsharp%2Cbash#create-a-local-functions-project)
- [Azure CLI version 2.4 or later](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- You will need the correct language runtimes installed for the type of function app you want to create.
### Create your local project

1. Run the func init command, as follows, to create a functions project in a folder named LocalFunctionProj with the specified runtime:

```
func init LocalFunctionProj --javascript
```
2. Navigate into the project folder:

```
cd LocalFunctionProj
```
This folder contains various files for the project, including configurations files named local.settings.json and host.json. Because local.settings.json can contain secrets downloaded from Azure, the file is excluded from source control by default in the .gitignore file.

3. Add a function to your project by using the following command, where the --name argument is the unique name of your function (HttpExample) and the --template argument specifies the function's trigger (HTTP).

```
func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"
```
func new creates a subfolder matching the function name that contains a code file appropriate to the project's chosen language and a configuration file named function.json.
### Run the function locally 
1. Run your function by starting the local Azure Functions runtime host from the LocalFunctionProj folder:
```
func start
```
Toward the end of the output, the following lines should appear:
```
 ...

 Functions:

[2021-02-23T23:41:12.154Z] Worker process started and initialized.
	HttpExample: [GET,POST] http://localhost:7071/api/HttpExample


 ...

 
```
2. Copy the URL of your HttpExample function from this output to a browser and append the query string ?name=<YOUR_NAME>, making the full URL like http://localhost:7071/api/HttpExample?name=Functions. The browser should display a message like Hello Functions:

### Create supporting Azure resources for your function

Before you can deploy your function code to Azure, you need to create three resources:

- A resource group, which is a logical container for related resources.
- A Storage account, which is used to maintain state and other information about your functions.
- A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Use the following commands to create these items.
1. If you haven't done so already, sign in to Azure:
```
az login
```
2. Create a resource group named AzureFunctionsQuickstart-rg in the eastus region:
```
az group create --name AzureFunctionsQuickstart-rg --location eastus
```
3. Create a general-purpose storage account in your resource group and region:
```
az storage account create --name <STORAGE_NAME> --location eastus --resource-group AzureFunctionsQuickstart-rg --sku Standard_LRS
```
In the previous example, replace <STORAGE_NAME> with a name that is appropriate to you and unique in Azure Storage. Names must contain three to 24 characters numbers and lowercase letters only. Standard_LRS specifies a general-purpose account, which is supported by Functions.

4. Create the function app in Azure:
```
az functionapp create --resource-group AzureFunctionsQuickstart-rg --consumption-plan-location eastus --runtime node --runtime-version 12 --functions-version 3 --name <APP_NAME> --storage-account <STORAGE_NAME>
```
In the previous example, replace <STORAGE_NAME> with the name of the account you used in the previous step, and replace <APP_NAME> with a globally unique name appropriate to you. The <APP_NAME> is also the default DNS domain for the function app. 

This command creates a function app running in your specified language runtime under the Azure Functions Consumption Plan, which is free for the amount of usage you incur here. The command also provisions an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see Monitor Azure Functions. The instance incurs no costs until you activate it. It will take a few seconds to create the app.

### Deploy the function project to Azure

After you've successfully created your function app in Azure, you're now ready to deploy your local functions project by using the func azure functionapp publish command.

In the following example, replace <APP_NAME> with the name of your app.

```
func azure functionapp publish <APP_NAME>
```
The publish command shows results similar to the following output 
```
Deployment completed successfully.
Syncing triggers...
Functions in sheltoG:
    HttpExample - [httpTrigger]
        Invoke url: https://sheltog.azurewebsites.net/api/httpexample

```
Copy the complete Invoke URL shown in the output of the publish command into a browser address bar, appending the query parameter ?name=Functions. The browser should display similar output as when you ran the function locally.

## Resources

Serverless Basics: https://serverless-stack.com/chapters/what-is-serverless.html
