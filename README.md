# microsoft_azure_fundamentals-AZ-900-
Tutorial based on Vlad Catrinescu and Neil Morrissey tutorial


# Introduction to cloud computing
In past each company got tons of servers for different purposes. They could run on different hardware, different operating systems. Each server got it's own RAM, CPU etc.
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/old_servers.png?raw=true)

Problems: 
* a lot of money 
* often servers were under utilized (e.g take only 20% of servers resources)
* for safety in case of disaster e.g flood, fire company need two serverrooms in different part of the world

then we switch to <b>virtualization</b>:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/virtualization.png?raw=true)

it was cheaper, needed less space but still got some disadventages - high up-front cost, need space in datacenter, need to pay for electricity

then we have <b>cloud computing</b> - Cloud computing enables companies to consume a compute resource rather than having tobuild and maintain computing infrastructures in house, it's like buying electricity, not building power station:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/cloud_computing.png?raw=true)

Cloud provider owns data center and manages servers, networking, virtualization etc.
All those resorces are shared between many clients, clients don't know which server is their, all they care is that they have enought resorces which cloud provider guarantee.

Cloud infrastructure is on demand self-service - you pay for using resources. Usually it's paid for seconds, minutes or hours. Azure is charging for seconds - your app worked 35secs, you pay for 35secs.

When you order Microsoft Azure you choose in which region server should be, which oparating system you want, how many RAM you need, how many CPU, how many storage and if it should be scaled on demand or automatically. Automatically mean that if CPU usage goes to 70% it can automatically add another CPU e.g when a lot of people want to use your website it will scale automatically and allow server to not go down. You'll pay a bit more for this time and then when additional CPU won't be needed anymore it will be taken away. It's called rapid elasticity. 

Cloud computing reliability - cloud provider take care about high availibility (HA) and disaster recovery (DR). High availibility is eg. power supply, disk failure etc. Disaster recovery is fire, flood, earthquake. Fault tolerance - zero downtime. If you would implement disaster recovery yourself you would need another data center so if your first datacenter is in Manila (capital of Philippines) then your second datacenter can be in Minsk (the capital of Belarus) or e.g Podgorica (the capital of Montenegro). With cloud provider you benefit from scale because cloud providers already have it. Azure datacenters are in 60 regions world wide.

Conclusion:
* allows organisations to consume computing resources as utility
* rapid elasticity
* billed per second/minute/hour
* reliability
* economies of scale

# CAPEX vs OPEX
Capital expenditures are depreciated over the useful life of the asset, you can't fully deduct the cost from the fiscal year the asset was paid for it. E.g buying servers for more than one year. 

Operating Expenses are deducted in the same year they are made. Cloud computing - you know (more or less) how much you'll pay for cloud.

# Types of Cloud Computing Services
Infrastructure as a Service(IaaS), Platform as a Service(PaaS) and Software as a Service(SaaS)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/on_premise_iaas_paas_saas.png?raw=true)

comparing to pizza:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/pizza_as_a_service.png?raw=true)


Most popular cloud providers:
* IaaS: Microsoft Azure, Amazon Web Services, Google Compute Engine
* Paas: Azure Logic Apps, Heroku, Amazon Elastic Beanstalk
* Saas: Office 365, Salesforce, Dropbox

Cloud Computing Services by Microsoft:
* IaaS: Azure Compute, Azure Storage
* PaaS: Azure Logic Apps, Azure Functions, Azure Web Jobs, Azure Automation
* SaaS: SharePoint, OneDrive for Business, Microsoft Teams, Power Platform


<b>Infrastructure as a service</b>:
perfect for test and development scenarios because you can turn on and turn off dev machines only when needed so you dont need to pay all the time.
Storage and backups as price is good. High performance computing and data analyzis - require very powerful computers for a short time.

<b>Platform as a service:</b>
analytics or business inteligence - alows company to analyze and mine data finding insights and patterns and predict outcomes to improve forecasting, product design decisions etc. it's also great for developers.

<b>Software as a service:</b>
getting access to sophisticated applications and no need to manage any infrastructure yourself. Imagine all of the work needed to install Skype for business, SharePoint servers on premises vs just using the same tools in a matter of minutes.

# Cloud computing deployment models
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/Cloud_Computing_Deployment_Models.png?raw=true)

<b>Public Cloud</b>
Multiple clients, shares hardware and backend. Most Azure customers are in public cloud.

<b>Private cloud</b>
Hardware used by a single company, usually (but not necesairly) who owns the datacenter. Close to traditional way. Azure Stack allows you to run cloud services on-premises. Later you can easily transfer to public cloud

<b>Hybrid cloud</b>
combination of public and private cloud with automation and orchestration betweeen them.Azure Stack allows you to run cloud services on-premises. Later you can easily transfer to public cloud

<b>Community cloud</b>
Infrastructure is shared between serveral organizations from a specific community with common concerns e.g security, compliance, jurisdiction. The most popular example is <b>Azure Goverment</b> - Azure offering specific to a government entities. To register for Azure Govenment you need to be validated as government organization. It's hosted in separate datacenters from public cloud.

# Azure data centers
Azure is just bunch of physical data centers full of physical servers. They locations are not public, often even Microsoft employees don't know locations. 

# Azure regions
for some Azure services you don't choose location, they are global (non-regional) but for most of them you need to specify in which region your account/storage etc. should be created. When you e.g work in Rotterdam (where is the biggest seaport in Europe) then it's better to choose some place in Europe for server location than e.g some place on smallest continent on the world - Australia because all requests would go from Rotterdam to Canberra (capital of Australia) and responses from Canberra to Rotterdam and it takes time. We need to remember not all services are available in all locations. 

Azure provide Regions Pairs - it means your data can be duplicated between two locations in case of failury of one data center or natural disaster. We don't decide what regions are paired, Microsoft do it.

# Resources groups
Resource is managable iteam in Azure: virtual machines, storage accounts , web apps, databases.

Resource group is container that hold related resources which share the same lifecycle (you update, delete, deploy them together). Resources can only exists in one Resource Group. You can move resource to another resource group but it can't be in two resources groups in the same time. Of course resources can communicate between different resource groups. Example: you have three applications with the same database. Database can be in completely different Resource group but still all three apps can use this database.
You can create accounts e.g for developers who can only check what resources are in resource group and admin account who can make changes. When you create resource group you specify region that it gets created in

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/resource_group.png?raw=true)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/resources_in_resource_group.png?raw=true)

# Azure Resource Manager(ARM)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_resource_manager.png?raw=true)

If you are using e.g Azure Portal you send requests to the ARM endpoint. ARM handles authentication using Azure Active Directory (Azure AD) and authorizes that you can perform action. ARM then send request to Azure service that you try to create e.g Virtual machine, Machine learning workspace etc.
There are also another way to call ARM endpoint e.g Azure PowerShell, Azure CLI (`az --version`, `az login`, `az group list`, `az resource list --resource-group resourcename`)

# Infrastructure as code using Azure Resource Manger Templates
you can deploy automatically by CI/CD pipelines. Azure has Azure Resources Manager Templates written in JSON, where you defines infrastructure and configuration for Azure resources. Significant point: it's declarative syntax. Example:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_resource_manager_template.png?raw=true)

You can save such template into library and then you can find it in `Templates`.

# Azure Service Health and Azure Monitor
In `Service Health` you have:
`Services issues` - if some services in any location are not down. You can also see if all services which you use are working correctly.
`Planned maintenance` - to check if some maintenance actions can affect you
`Health advisories` -  if Microsoft upgrade something or one of you features which you use are being deprecated and you need to upgrade
`Security advisiories` - notification or violations that may affect the availability of your Azure services.

You can also create alert when you want to be notified (by email/sms/push notification/mobile app) if there will be any changes to your services e.g planned maintenance.

There is also `Monitor` which provide detailed information about resource (can't be applied for whole resource group).

# Azure Mobile App
you can use mobile app to check notifications, monitor status of your applications or even run commands using cloud shell. You can open all of your resources group, start virtual machines, connect to the VM etc.

# Azure Advisor for Optimizing your Azure Resources
Azure Advisor is personalized cloud consultant that helps you follow best practices to optimize your Azure deployments. It's a tool which provides recommendations. It's even send recommendations how to optimize costs - pay less and it's not just generic recomendations, it's checking your actual deployments. If you are not interested in some recomendations you can postpone(so you won't see them for some time) them or dissmiss
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_advisor.png?raw=true)

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/recomendation_example.png?raw=true)

# Azure Compute
Azure compute is a set of services that provide on-demand computing power. Compute isn't really a service in itself, it's logical grouping of several services in Azure related to running application workloads. 

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_compute.png?raw=true)

# Azure Virtual Machines
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_virtual_machines.png?raw=true)

while creating new virtual machine you can choose a lot of images so you can have preinstalled e.g Visual Studio, SQL, etc. You also choose how many CPUs, RAM should virtual machine has. If you choose two or more availability zones you need to configure load balancer by yourself. When you create virtual machine, presented cost is just for virtual machine but beside of that there are other resources that get created: virtual network, disc, azure storage account so that will be additional cost. After you create virtual machine you can still add disc to it, enable auto shutdown so at night you won't pay for it, you can configure backup system

# Container options in Azure
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/vm_vs_containers.png?raw=true)

Here we have <b>Docker</b> is open source. There is docker hub, it's library for images. Docker provides standard for container format, it's runtime process which you can install on vm. For smaller/easier infrastructure there is Azure Container Instances.

You can deploy containers on VMs in Azure of course. For complex architecture there is Azure Kubernetes Service (container management system in Azure, scale out container-based applications, monitoring and deploying containers, nodes are virtual machine) so containers orchestrator. Pods are groups of containers.

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/creating_container.png?raw=true)

when creating container you can upload your own image, use image from docker hub. In the same way you can create kubernetes cluster.

# Azure App Service
Azure App Service is more like traditional web hosting where the frameworks are already installed on server like .NET, Java and you deploy your code onto those servers. The difference with traditional web hosting is that Azure App Service handles the management and patching for you but you still have lots of configuration options.

Azure App Service can host:
* web application, 
* API apps, 
* mobile apps, 
* you can deploy containers if you want  
* WebJob.

When you deploy application then address will be `https:<your app service name>.azurewebsites.net`. Suffix `azurewebsites.net` is default, you can change it.

You can try Azure App Service for free but then there are some limits e.g custom domain is not available, max number of apps is 10, you can't use auto scale.

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/example_app.png?raw=true)

There is a lot of details from deployed app - how much time response from app took, how many request there were etc. You don't have to build the whole authentication subsystem into your app, you can just mark integration with Facebook, Twitter, etc. You can get console window to the virtual machine your app is deploy, you can check logs

# Serverless compute
Azure functions - which developer write enable to develop serverless applications on Azure. You write small pieces of code without worrign about the whole application and infrastructure. You can write in .NET, C#, even Powershell. Functions have triggers e.g HTTP endpoint so it can be trigger by endpoint call, timer trigger, bus storage, blob etc.
Azure Logic Apps - visual designer to model and automate process as steps/workflow. Pros+ (pre-buuld templates, easy to use design tools)
Azure Event Grid - event routing service using publish-subscribe model. You can react on events, event sources, topics, event subscriptions and event handlers. Use Event Grid for reactive programming, as it is just an event distributor. Notify me when I need to do something or notify some other service when it needs to do something.

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/event_grid.png?raw=true)

# Azure Networking
Azure Virtual Network is Azure virtual block in your private network. Vnet enables many types of Azure resources to communicate. Virtual network has an address space that you define in Azure, which is group of IP addresses that can be assigned to resources like Virtual Machines. VNet is segmented into one or more subnetworks called subnets, which are allocated a portion of the VNet's IP address space. Virtual Machine is assigned to a subnet and Virtual Machine can communicate with other VMs on the same network. By default, resources assigned to one virtual network can't communicate with resources in another virtual network. You can enable communication between VMs in other Virtual Network by feature called VNet peering. You can enable VNet peering even between virtual machines which are in other regions. 

To communicate with the world VM need to has public IP address. IP address is a separate resource in Azure.

When you have two Virtual Machines in the same subnet you can implement LoadBalancer. 


![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/load_balancer.png?raw=true)

You can use Application Gateway like in screenshot above. So traffic from internet can be encrypted but then behind Application Gateway it doesn't need to be encrypted.

In hybrid cloud you need connection between your on-premises network with azure virtual network (VNet).
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/hybrid_cloud_connection.png?raw=true)

or you can use ExpressRoute
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/expressroute.png?raw=true)

# Windows virtual desktop
You can access virtual desktop from any browser because many operating systems are supported: Windows, mac, android, ios.
In past you got single virtual machine for single user, windows virtual desktop let to work people on the same machine, sharing resources, just with different discs so everyone feels like working on local computer.

# Azure content delivery network
Caching is a process of storing data locally so it can be provided quickly when it's requested again in future.

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_content_delivery_network.png?raw=true)

AppService/WebApp from which we want to get data is called `Origin server`. CDN server can cache from Web app, blob service or any public web server in internet. CND server which get date from Origin server and provide to user is called `edge server`.

# Data storage in Azure
In Azure there are different storage services for specific data types. Benefits to Azure data storage solutions:
* Automated backup and recovery
* Replication across the world
* encryption options
* security and platform integration
* development features and support

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/categories_of_data.png?raw=true)

# Database products in Azure
SQL Server on Virtual Machines:
* full control over the SQL server
* can provision from the Azure Marketplace
* Flexible pricing options
* Automated updates scheduling
* Manage backups to Microsoft Azure

Azure SQL Database:
* Fully managed platform-as-a-service
* always running the latest version of SQL Server
* Flexible pricing model (Vcores or DTU's)
* Single database or Elastic Pool (many dbs with shared resources)
* Automatic scaling
* Service tiers for different workloads e.g hyper scale for huge databases

Azure SQL Managed Instance:
* Broadest set of SQL server capabilities
* Benefits of managed platform
* deploy VM onto your own VNET
* List and shift with minimal changes

# Azure Cosmos DB for semi structured data
when there is data that don't fit perfectly to relational database as PostgreSQL, MySQL etc. then Azure Cosmos DB helps.
Adventages:
* fast repsonse times
* multi-modal
* ability to scale rapidly and globally, elastically scale throughput and storage across any number of Azure regions and you can add or remove regions easily
* backed by SSD storage
* consistency options to ensure distributed data is updated

Use cases for Cosmos DB: 
* Retail Application (Attributes can vary and change over time, flexible schema), 
* gaming applications< e.g HALO 5, skype, office365 (millions of simultaneous updates, millisecond reads), 
* social media applications - comments, likes etc. (Flexible data schemas, needed for user generated content)

Cosmos DB APIs: SQL API, Cassandra, Mongo DB, Gremlin, Azure Table Storage

# Azure storage account
BLOB is acronym for Binary Large Object. Like a file, a blob can be any type of file documents, video files, text files. Blob storage is optimized for storing massive amounts of unstructured data. 

Azure storage Services:
* Blob Storage (unstructured data: files and documents)
* File Storage (supports SMB protocol (port 445 or call via Azure VNET))
* Disk Storage (infra as a service)
* Table storage (structured date in the form of NoSQL non relational data, similar data you can store using Cosmos DB)
* queue store (asynchronous)

Zone Redundant Storage (GRS) data is stored in three times in the primary data center by default and you can choose to copy data to another availability zone and other regions. Data from Azure Storage can be reached by https and each storage service within an Azure Storage has it's own REST endpoint. You can manage access to database by RBAC in Azure AD, storage account keys or shared access signature.

Programatic access to storage accounts: REST APIs, SDKs, Powershell, Azure CLI, Azure Storage Explorer, AzCopy

Blob types:
* Block Blob, composed of blocks (optimize uploading)
* Append Blob (optimized for appending only, good choose for logs)
* Page Blob (8TB max, disk for Vm are stored as page blob, optimized for random and frequently read-write operations)

Blob access tiers:
* hot tier - for data which is access frequently so <b>highest storage cost, lowest data access cost</b>
* cool tier - for storing infrequently accessed data so <b>lowest storage cost, highest data access cost</b>
* archive tier - for data which you rarely access <b>lowest storage cost</b>

# Data migration options

Azure database migration service (DMS) it's managed service to migrate database data to Azure data platforms:
* on premises databases
* azure databases
* amazon web services 

There are two possibilities for migration: <b>offline and online</b>. 
In offline migration database is down when migration start, in online migration timedown is limited to cutover.

Usually migration is:
* create target database in Azure
* assess source database for compability (just to check if there are no compatibility issuess, there is a tool called <b>database migration assistent</b> which you can download and run against your database)
* create instance of Azure DMS
* configure source and target databases
* migrate data
* switchover production application

# Example questions
1. When Azure machine is stopped you still pay storage costs associated to this virtual machine? Yes, you still have to pay for storage but you don't pay for stopped virtual machine.
2. Platform as a service allow you to control operating system? No, you don't control system in PaaS, you control application. You don't have access to operating system or virtual machine in PaaS. 
3. In SaaS you are responsible for installing the SaaS solution. No, you are responsible only for configuring the SaaS solution. Provider cares about infrastructure, you just pay for renting application and users can connect to Web App with a web browser. 
