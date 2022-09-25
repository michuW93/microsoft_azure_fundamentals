microsoft_azure_developer-AZ-204-

Tutorial based on Matthew Kruczek, Anthony E.Nocentino, Mike Pfeiffer, Mark Heath, David Tucker videos

# General Overview
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

# Preparation
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
az vm list-ip-addresses \ <br/>
  --resource-group "psdemo-rg" \ <br/>
  --name "psdemo-linux-cli" <br/>


To remove resource group: `az group delete --name "psdemo-rg"`

# Creating a VM with Azure PowerShell
$username = 'demoadmin' <br/>
 $password = ConvertTo-SecureString 'pass' -AsPlainText -Force<br/>
 $WindowsCred = <br/>
  
  
  and then create VM with above credentials:
 New-AzVM \ <br/>
  -ResourceGroupName 'psdemo-rg' <br/>
  -Name 'psdemo-win-az' <br/>
  -Image 'Win2019Datacenter' <br/>
  -Credential $WindowsCred <br/>
  -OpenPorts 3389 <br/>
  
To get public IP: `Get-AzPublicIpAddress -ResourceGroupName 'psdemo-rg'`


# Creating a VM with ARM (Azure Resource Manager) Templates
with ARM Templates you can create any resource, not only VM. ARM Templates base on JSON files. It is possible to export ARM Template in Azure Portal or write on your own, then deploy from Quickstart template library. Once .json file is created you can import it into Azure Portal and deploy from file which you created, this template.json can also be used via CLI

Example (just part) of json template Downloaded from Azure Portal:
{<br/>
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",<br/>
    "contentVersion": "1.0.0.0", <br/>
    "parameters": { <br/>
        "location": { <br/>
            "type": "string" <br/>
        }, <br/>
        "networkInterfaceName1": { <br/>
            "type": "string" <br/>
        } <br/>


# CONCLUSION
There are many ways to create VM in Azure. First Resource Group needs to be created, then VM (with open ports)

# 3. Containers
Docker / Azure Container Registry (ACR) / Azure Container Instances (ACI)

In general - containers allows to package binaries, libraries and other components into one file which is called <b>Container image</b> - binary application package. Container is place where image is running. There is one app inside the container. Container is very small and very portable. <b>Container Registires enables exchanging of container images</b>

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/containers_vs_old_way.png?raw=true)

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/woring_with_containers_in_azure.png?raw=true)

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
docker push $ACR_LOGINSERVER/webappimage:v1 <br/>


#Build using ACR Tasks
az acr build --image "webappimage:v1-acr-task" --registry $ACR_NAME .

# Deploying Containers in Azure Container Instances
it's serverless container platform, it allows access application via Internet or on an Azure Virtual Network, it can run on Windows or Linux containers, it can use Azure Files for persistent storage, restart policy - always (default), on failure or never.
You can deploy container in Azure Container Instances from Azure Container Registry but it can also be done from Docker Hub or other container registries

# creating a Service Principal for ACI to Pull From ACR
ACR_NAME='psdemoacr' <br/>
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME) <br/>

SP_NAME=acr-service-principal
SP_PASSWD=$(az ad sp  create-for-rbac \ <br/>
  --name http://$ACR_NAME-pull <br/>
  --scopes <br/>
  --role acrpull <br/>
  --query password <br/>
  --output tsv) <br/>
  
SP_APPID=$(az ad sp show <br/>
  --id<br/>
  -- query appId<br/>
  --output tsv<br/>
  
# Running a container from ACR in ACI
ACR_LOGINSERVER -> took $ACR_NAME

az container create \ <br/>
  --resource-group psdemo-rg <br/>
  --name <br/>
  --dns-name-label <br/>
  --ports 80 <br/>
  --image $ACR_LOGINSERVER/webappimage:v1 <br/>
  --registry-login-server $ACR_LOGINSERVER <br/>
  --registry-username $SP_APPID
  --registry-password $SP_PASSWD

# 4. Azure App Service Web Apps
What is Azure App Service? Http-based service for hosting web apps. It can run and scale on Windows and Linux. Security, load balancing and automation e.g deploying code. Costs use are determined by the App Service plan.

There are two types of App Service Plans: Non isolated and Isolated.
In App Service (Web Apps, API Apps, or Mobile Apps), an app always runs in an App Service plan. In addition, Azure Functions also has the option of running in an App Service plan. An App Service plan defines a set of compute resources for a web app to run. These compute resources are analogous to the server farm in conventional web hosting. One or more apps can be configured to run on the same computing resources (or in the same App Service plan).

When you create an App Service plan in a certain region (for example, West Europe), a set of compute resources is created for that plan in that region. Whatever apps you put into this App Service plan run on these compute resources as defined by your App Service plan. Each App Service plan defines:

Operating System (Windows, Linux)
Region (West US, East US, etc.)
Number of VM instances
Size of VM instances (Small, Medium, Large)
Pricing tier (Free, Shared, Basic, Standard, Premium, PremiumV2, PremiumV3, Isolated, IsolatedV2)

The pricing tier of an App Service plan determines what App Service features you get and how much you pay for the plan. The pricing tiers available to your App Service plan depend on the operating system selected at creation time. There are a few categories of pricing tiers:

Shared compute: Free and Shared, the two base tiers, runs an app on the same Azure VM as other App Service apps, including apps of other customers. These tiers allocate CPU quotas to each app that runs on the shared resources, and the resources cannot scale out.
Dedicated compute: The Basic, Standard, Premium, PremiumV2, and PremiumV3 tiers run apps on dedicated Azure VMs. Only apps in the same App Service plan share the same compute resources. The higher the tier, the more VM instances are available to you for scale-out.
Isolated: This Isolated and IsolatedV2 tiers run dedicated Azure VMs on dedicated Azure Virtual Networks. It provides network isolation on top of compute isolation to your apps. It provides the maximum scale-out capabilities.


Non-isolated App Service Plans:
* free and shared (F1, D1) = not for prod
* basic (b1, b2, b3) = not for prod, more for testing, doesn't require scalable
* standard (s1, s2, s3) for prod, cost depends on how many instances you run
* premium v2 
* premium v3 (upgraded premium v2)

Isolation with App Service Environments(ASE):
* Fully isolated and dedicated env for running web apps
* high scale, high memory utilization
* isolation and secure network access
* fine-grainded control over network traffic
* apps can connect over VPN to on-premises resources

We can create Web app via Azure Portal (Web App), Azure CLI, Azure PowerShell, ARM Template. There are 3 steps: create resource group, create app service plan and then finally create web app

Example with Azure CLI:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/create_app_service_via_azure_cli.png?raw=true)

# Secure a Domain with SSL/TLS Binding
You must at least use Basic plan type to be able to use HTTPS. You can then enforce HTTPS and TLS versions.

First you need to add custom domain and then add binding TLS/SSL because there would be a warning message. 

# Configuring a Database Connection String
App Service Web App -----> Connection string e.g SQLServerDB -------> Azure SQL Database

we don't want to hardcode connection string

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/connection_string.png?raw=true)

It's like a variable - if you name it `DatabaseConnection` and then in app you can query it via this name. Connection Strings can also map to the values from Key Vault (some secrets).

Diagnostic logging:
* application logging (linux or windows) - logs generated by application, can be stored in Azure Storage
* web server logging (windows) - method which were used, http requests etc.
* detailed error messages (windows) - you don't want to show all details to end user but you need it while debugging
* failed request tracing (windows) - detailed error for requests
* deployment logging (win/linux) - when you do deploy

it can be turned on in Azure Portal: Monitoring -> App Service Logs

How to deploy code to App Service Web Apps: configure continous deployment so App Service pulls code from GitHub or Azure Repos. You need to authorize Azure App Service and enable continous deployment.
In Azure Portal it's in Deployment section and `Deployment Center`. First you choose source of code e.g GitHub, then specify `Build Provider` e.g Azure Pipelines or App Service Kudu, then configure GitHub setting e.g repository and branch.

# Scaling Azure App Service
Scaling up Vertically vs Scaling up horizontaly <br/>
Vertically - you have 1vCore and 2GB RAM but app is getting bigger and bigger then you switch machine for 8vCore and 64 GB RAM <br/>
Horizontally - adding new machines e.g add azure load balancer and second virtual machine, then add third machine

Auto scale is available for standard, premium and isolated pricing tiers. Scaling can be done manually or on schedule e.g take out 1 machine after 5 p.m or it can autoscale using rules (base on resource metrics e.g add virtual machine if CPU is above 70%)

# Azure functions
What are Azure Functions? A serverless application platform, a simple way to run small piece of code ("functions") in the cloud, FaaS - function as a service.
Serverless - delegate server management responsibility to the cloud provider, supports automatic scaling to meet demand, billed only when it's running
Azure function app - one or more related Azure Functions, that are developed, deployed and hosted as a group

You can create Azure Functions in C#, Java, JS, Python and many others
Azure Functions usually run in a `Service plan` on Azure App Service. You can choose Consumption plan - it's serverless, automatic scale, 5 min limit and you pay if use or App Service plan in which is traditional pricing model - paying X per month, or Premium Plan which offers better speed, security and reserved instances. Or you can run Azure functions in Docker Container or Locally for development and testing. 

You can develop azure functions in Azure Portal or Visual Studio or Azure Functions Core Tools

Azure function trigger - when trigger is trigerred then Azure Function is executed. It can be implemented using data operations(BLOB Storage Trigger), timers(scheduled task) and webhooks(HTTP Request Trigger). Every Azure function has exactly one trigger. For timer trigger you need to provide CRON expression.

Azure Function Binding is a connection to data. Input binding provide read-access to data. Output bindings let us write to an external system. Functions can have multiple input and output bindings. Input/Output bindings are defined in .json file.

Azure <b>Durable Function</b> is an extension to Azure Functions which enables to create stateful, serverless workflows. It consist of 3 types of function:
* Client(Started) Function - initiate a new orchestration, can use any trigger
* orchestrator function - defines the steps in the workflow, handle errors
* activity function - implements a step in the workflow, use any bindings

Orchestration patterns: 
* Function chaining = do activities in defined order Activity1 -> Activity2 -> Activity3
* Fan-out Fan-in
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/fan_out_fan_in.png?raw=true)

* Async HTTP API's
* Monitoring
* Human Interaction
* Aggregator(Stateful Entities)

What if you would like to create Azure Function in Rust or Go which are not supported? You need to use Custom Handler. Custom Handler can be implemented using your language or runtime of choice.

# Review
Managed Identities - how to login into VM, how to allow user do sth etc. Get credentials in PowerShell <br/>
$username = 'demoadmin' <br/>
 $password = ConvertTo-SecureString 'pass' -AsPlainText -Force<br/>
 $WindowsCred = <br/>
  
 and then create VM with above credentials:
 New-AzVM \ <br/>
  -ResourceGroupName 'psdemo-rg' <br/>
  -Name 'psdemo-win-az' <br/>
  -Image 'Win2019Datacenter' <br/>
  -Credential $WindowsCred <br/>
  -OpenPorts 3389 <br/>

Backup and Restore Approaches - how to backup VM
Accelerated Networking
When to not to use an Azure VM - cost effective solutions

Deployment slot and slot swapping.

App Service Tiers:
* Free (F) 
* Shared (D) - designed for development and testing, not for Prod!
* Basic (B) - doesn't provide app scaling but provide e.g loadbalancing, but also not for Production
* Standard (S) - allow <b>autoscaling</b>
* Premium (P) - higher scale level, better machines
* Isolated (I) - it's in isolated network, azure app service environment (ASE)

Azure functions - input and output bindings
