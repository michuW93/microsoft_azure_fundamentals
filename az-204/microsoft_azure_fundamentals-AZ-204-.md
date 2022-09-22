microsoft_azure_fundamentals-AZ-204-

Tutorial based on Matthew Kruczek, Anthony E.Nocentino, Mike Pfeiffer videos

1. 
# Develop Azure Compute Solutions:
* Implement IaaS Solutions (Provision Virtual Machines but you need to take care of rest, Configure, validate and deploy ARM templates, Configure container images for solutions, publish an image to the Azure Container Registry, Run Containers by using Azure Container Instance)
* Create Azure App Service Web Apps (Create an Azure App Service Web App, enable diagnostic logging, deploy code to a web app, configure web app settings, implement autoscaling rules, including scheduled autoscaling and scaling by operational or system metrics)
* Implement Azure Functions (create and deploy Azure Functions, Implement input and output bindings for a function, implement function triggers by using data operations, timers and webhooks, implement azure durable functions, implement custom handlers)

# Implement Azure security
* Implement user authentication and authorization (authenticate and authorize users and apps by using Azure Active Directory, create and implement shared access signatures)
* implement secure cloud solutions (Azure services which deals with security: Azure Key Vault, Microsoft Graph)

# Connect to and Consume Azure Services and Third-party Services
* Implement API Management (Create an APIM instance, configure authentications for APIs, Define policies for APIs)
* Develop Event-Based Solutions (Implement solutions that use Azure Event Grid and Azure Event Hub)
* Develop Message-Based Solutions (Implement solutions that use Azure Service Bus and Azure Queue Storage Queues)

# Develop for Azure Storage
* Develop Solutions that use Cosmos DB storage(Select the appropriate API and SDK for solution, implement partitioning schemes and partition keys, perform operations on data and Cosmos DB containers, set the appropriate consistency level for opertations, manage change feed notifications)

# Monitor, Troubleshoot and optimize azure solutions
* Integrate caching and content delivery within solutions (Configure cache and expiration policies for Azure Redis cache, Implement data sizing, connections, encryption and expiration)
* instrument solutions to support monitoring and logging (configure an app to use Application Insights, analyze and troubleshoot solutions by using Azure Monitor, Implement Application Insights web tests and alerts)

# 2. Virtual Machines 
Virtual Machine Components: Resource group, VM Size, Network, Images, Storage/Virtual Disk

How to create VM in Azure? Via Azure Portal, Azure CLI, Azure PowerShell(AZ module), Azure ARM Templates

For Windows <b>RDP: 3389, for Linux SSH: 22. </b>

It's possible to create VM programmatically, it's a bit better because add consistency to your deployments and VM creation, any production system should be implemented using automation, it's allow to construct similar down-level environments, such as DEV/TEST. It can be done via tools: Azure CLI, Azure PowerShell or ARM Templates.

Create VM from Azure CLI:
1. create resource group
az group create \ <br/>
  --name "resource_group_name" \ <br/>
  --location "centralus" <br/>

  
2. create VM
az vm create \ <br/>
  --resource-group "psdemo" \ <br/>
  --name "psdemo-win-cli" \ <br/>
  --image "win2019datacenter" \ <br/>
  --admin-username "demo" \ <br/>
  --admin-password "pass123@!$#@@!" <br/>
  
To enable remote access with Azure CLI:
az vm open-port \ <br/>
  --resource-group "psdemo-rg" \ <br/>
  --name "psdemo-win-cli" \ <br/>
  --port "3389"<br/>
  
To get ip adresses:
az vm list-ip-addresses \<br/>
  --resource-group "psdemo-rg" \<br/>
  --name "psdemo-linux-cli"<br/>


To remove resource group: `az group delete --name "psdemo-rg"`

# Creating a VM with Azure PowerShell
$username = 'demoadmin'<br/>
 $password = ConvertTo-SecureString 'pass' -AsPlainText -Force<br/>
 $WindowsCred = <br/>
  
  
  and then create VM with above credentials:
 New-AzVM \<br/>
  -ResourceGroupName 'psdemo-rg'<br/>
  -Name 'psdemo-win-az'<br/>
  -Image 'Win2019Datacenter'<br/>
  -Credential $WindowsCred<br/>
  -OpenPorts 3389<br/>
  
To get public IP: `Get-AzPublicIpAddress -ResourceGroupName 'psdemo-rg'`


# Creating a VM with ARM (Azure Resource Manager) Templates
with ARM Templates you can create any resource, not only VM. ARM Templates base on JSON files. It is possible to export ARM Template in Azure Portal or write on your own, then deploy from Quickstart template library. Once .json file is created you can import it into Azure Portal and deploy from file which you created, this template.json can also be used via CLI

Example (just part) of json template Downloaded from Azure Portal:
{<br/>
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",<br/>
    "contentVersion": "1.0.0.0",<br/>
    "parameters": {<br/>
        "location": {<br/>
            "type": "string"<br/>
        },<br/>
        "networkInterfaceName1": {<br/>
            "type": "string"<br/>
        }<br/>


# CONCLUSION
There are many ways to create VM in Azure. First Resource Group needs to be created, then VM (with open ports)

# 3. Containers
Docker / Azure Container Registry (ACR) / Azure Container Instances (ACI)

In general - containers allows to package binaries, libraries and other components into one file which is called <b>Container image</b> - binary application package. Container is place where image is running. There is one app inside the container. Container is very small and very portable. <b>Container Registires enables exchanging of container images</b>

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-900/images/containers_vs_old_way.png?raw=true)

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-900/images/containers_vs_old_way.png?raw=true)

To build image: `docker build -t image:v1 .`
To check images: `docker ps`

# Azure Container Registry (ACR) - build, store and manage container images
it has ACR Tasks for container image automation - building, testing, pushing, deploying images in Azure, it has Service tiers.

ACR requires authentication for operations (Azure Active Directory Identities, ACR Admin (by default disabled))
to login to ACR: `az acr login` or `docker login`. It has Role-based access controls to know who can do what. There are some predefined roles but also new customized roles (e.g owner, contributor, reader, AcrPush, AcrPull, AcrDelete and AcrImageSigner) can be created. 

Create and Authenticating to Azure Container Registry:
ACR_NAME='login name' #this needs to be global<br/> 
az acr create \ <br/>
  --resource-group psdemo-rg \ <br/>
  --name $ACR_NAME \ <br/>
  --sku Standard<br/>

az acr login --name $ACR_NAME

Pushing an Image into ACR (it can be done via Docker tools and ACR Tasks):
ACR_NAME='psdemoacr' <br/>
ACR_LOGINSERVER=$(az acr show --name $ACR_NAME --query loginServer --output tsv) <br/>
docker tag webappimage:v1 (this is local image built earlier) $ACR_LOGINSERVER/webappimage:v1 <br/>
docker push $ACR_LOGINSERVER/webappimage:v1<br/>


#Build using ACR Tasks
az acr build --image "webappimage:v1-acr-task" --registry $ACR_NAME .

# Deploying Containers in Azure Container Instances
it's serverless container platform, it allows access application via Internet or on an Azure Virtual Network, it can run on Windows or Linux containers, it can use Azure Files for persistent storage, restart policy - always (default), on failure or never.
You can deploy container in Azure Container Instances from Azure Container Registry but it can also be done from Docker Hub or other container registries

# creating a Service Principal for ACI to Pull From ACR
ACR_NAME='psdemoacr'<br/>
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME)<br/>

SP_NAME=acr-service-principal
SP_PASSWD=$(az ad sp  create-for-rbac \ <br/>
  --name http://$ACR_NAME-pull <br/>
  --scopes<br/>
  --role acrpull<br/>
  --query password<br/>
  --output tsv)<br/>
  
SP_APPID=$(az ad sp show <br/>
  --id<br/>
  -- query appId<br/>
  --output tsv<br/>
  
# Running a container from ACR in ACI
ACR_LOGINSERVER -> took $ACR_NAME

az container create \<br/>
  --resource-group psdemo-rg<br/>
  --name<br/>
  --dns-name-label<br/>
  --ports 80 <br/>
  --image $ACR_LOGINSERVER/webappimage:v1 <br/>
  --registry-login-server $ACR_LOGINSERVER <br/>
  --registry-username $SP_APPID
  --registry-password $SP_PASSWD
