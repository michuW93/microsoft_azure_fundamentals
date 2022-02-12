# microsoft_azure_fundamentals-AZ-900-
Tutorial based on Vlad Catrinescu, Neil Morrissey, Michael Brown and Steve Buchanan tutorial


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

then we have <b>cloud computing</b> - Cloud computing enables companies to consume a compute resource rather than having to build and maintain computing infrastructures in house, it's like buying electricity, not building power station:
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
In past IT expenses have been considered a Capital Expenditure.

# Types of Cloud Computing Services
Infrastructure as a Service(IaaS), Platform as a Service(PaaS) don't allow to configure OS but e.g provide ability to scale the platform automatically and Software as a Service(SaaS). In SaaS you are only responsible for configuring SaaS solution. Software as a service allows users to connect to and use cloud-based apps over the Internet. Common examples are email and calendaring.
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/on_premise_iaas_paas_saas.png?raw=true)

comparing to pizza:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/pizza_as_a_service.png?raw=true)


Most popular cloud providers:
* IaaS: Microsoft Azure, Amazon Web Services, Google Compute Engine, <b>Azure Virtual Machine, Azure Storage</b>
* Paas: Azure Logic Apps, Heroku, Amazon Elastic Beanstalk, <b>Azure SQL, Azure Cosmos DB</b>
* Saas: Office 365, Salesforce (Salesforce Platform (also known as Force.com) is a platform as a service (PaaS) that allows developers to create add-on applications that integrate into the main Salesforce.com application. These third-party applications are hosted on Salesforce.com's infrastructure.), Dropbox

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
combination of public and private cloud with automation and orchestration betweeen them.Azure Stack allows you to run cloud services on-premises. Later you can easily transfer to public cloud. To create a hybrid cloud, you must deploy resources to a public cloud.

<b>Community cloud</b>
Infrastructure is shared between serveral organizations from a specific community with common concerns e.g security, compliance, jurisdiction. The most popular example is <b>Azure Goverment</b> - Azure offering specific to a government entities. To register for Azure Govenment you need to be validated as government organization. It's hosted in separate datacenters from public cloud.

# Azure data centers
Azure is just bunch of physical data centers full of physical servers. They locations are not public, often even Microsoft employees don't know locations. 
Service Level Agreement (SLA) guarantee at least 99.9 percent of service being up, you can increase to 99.95% when adding Azure resources to multiple regions.

# Azure regions
for some Azure services you don't choose location, they are global (non-regional) but for most of them you need to specify in which region your account/storage etc. should be created. When you e.g work in Rotterdam (where is the biggest seaport in Europe) then it's better to choose some place in Europe for server location than e.g some place on smallest continent on the world - Australia because all requests would go from Rotterdam to Canberra (capital of Australia) and responses from Canberra to Rotterdam and it takes time. We need to remember not all services are available in all locations. 

Azure provide Regions Pairs - it means your data can be duplicated between two locations in case of failury of one data center or natural disaster. We don't decide what regions are paired, Microsoft do it.
There are also some special regions: US Gov, China and Germany. It's related to compliance.

<b>Data transfers between Azure services located in different Azure regions are not free. Every Azure region has multiple datacenters. There are three Availability
Zones per supported Azure region</b> 

# Resources groups
Resource is managable iteam in Azure: virtual machines, storage accounts , web apps, databases. You can create as many resource groups as you want, <b>you don't pay for it</b>.

Resource group is container that hold related resources which share the same lifecycle (you update, delete, deploy them together). Resources can only exists in one Resource Group. You can move resource to another resource group but it can't be in two resources groups in the same time. <b>Of course resources can communicate between different resource groups.</b> Example: you have three applications with the same database. Database can be in completely different Resource group but still all three apps can use this database. <b>One resource group can contains resources from many Azure regions.</b>
You can create accounts e.g for developers who can only check what resources are in resource group and admin account who can make changes. When you create resource group you specify region that it gets created in. If you delete resource group all resources in this resource group will be also deleted.

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/resource_group.png?raw=true)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/resources_in_resource_group.png?raw=true)

# Azure Resource Manager(ARM)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/azure_resource_manager.png?raw=true)

If you are using e.g Azure Portal you send requests to the ARM endpoint. ARM handles authentication using Azure Active Directory (Azure AD) and authorizes that you can perform action. <b>Up to 5000 custom roles can be creater for each Azure Active Directory.</b> ARM then send request to Azure service that you try to create e.g Virtual machine, Machine learning workspace etc.
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

You can also create alert when you want to be notified (by email/sms/push notification/mobile app) if there will be any changes to your services e.g planned maintenance. For example you can create `Budget alerts` when cost of the current billing period for an Azure subscription exceed a limit.

There is also `Monitor` which provide detailed information about resource (can't be applied for whole resource group). <b>Azure Monitor can be used even for monitor performance of on-premises computer</b>.

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

while creating new virtual machine you can choose a lot of images so you can have preinstalled e.g Visual Studio, SQL, etc. You also choose how many CPUs, RAM should virtual machine has. If you choose two or more availability zones you need to configure load balancer by yourself. When you create virtual machine, presented cost is just for virtual machine but beside of that there are other resources that get created: virtual network, disc, azure storage account so that will be additional cost. After you create virtual machine you can still add disc to it, enable auto shutdown so at night you won't pay for it, you can configure backup system. <b>When you already have virtual machines and you create a new subscriptions you can easily move them to the new subscription</b>.

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

<b>You can try Azure App Service for free but then there are some limits e.g custom domain is not available, max number of apps is 10, you can't use auto scale. Azure free account has a 5 GB blob storage limit and a 5 GB file storage limit.</b>

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

or you can use ExpressRoute (inbound traffic from on-premises to Azure is free, <b>outbound from Azure to on-premises is not free</b> and any data traffic between Azure services in the same region is also free)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/expressroute.png?raw=true)

<b>The Azure VPN device is known as a Virtual Network Gateway</b>

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

<b>We need to remember that cost of storage will depend of localization, it's not the same in different locations, also cost depends of how much you write and read. If you want to transfer data between storage accounts in different azure regions you have to pay.</b>

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

<b>Data stored in an Azure Storage account has at least 3 copies.</b>

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

# Azure Services for the Internet of Things
The Internet of things (IoT) describes physical objects (or groups of such objects) that are embedded with sensors, processing ability, software, and other technologies that connect and exchange data with other devices and systems over the Internet or other communications networks. So basically 
IoT are devices and sensors connected to each other and the internet. Examples: smart thermostat, motion sensors and security camers, sensors embedded in concrete, traffic sensors.
They can send <b>alerts</b> in case of issue with a device or the environment the device is sensing or data can be stored in central location and used to generate <b>insights</b> that can improve business or a business process. We need to collect the data from different devices and sensors and <b>act</b> on the data or funnel the data into other systems that can perform deeper analysis.

Problems with IoT:
* lack of standars
* security, IoT devices can be hacked

IoT services from Azure:
* Azure IoT Central - Managed App Platform allows faster to start developing solutions. 
* Azure IoT Hub - platform which provide building blocks for connecting devices to the cloud, managing those devices and ingesting data into the service. Allows bidrectional secure communication with milions of devices. IoT hub is in the middle and all devices are connected to it, it can  get data from devices and send some request e.g device send to IoT Hub that temperature in room is 26 degrees, IoT Hub send request to fan to start working to cool down room. IoT Hub has SDKs and APIs for many languages to allow developer to build custom solution. IoT Hub provide authentication capabilities: X.509 certificates and Shared Access Signatures
* Azure Sphere - it's intended to solve lack of standards and security. Application platform consist of Micro-controller unit (hardware), linux based operating system (software) and cloud based security service. IoT Central and IoT Hub are connected to Azure Sphere which does things like make sure the device boots up with only an authirized version of software. Microsoft takes care of OS updates and patching or any other security issues.

# Big Data
Big Data is gather large datasets, organize the data, process the data and gather insights from the data.
Before sophisticated tools for big data there was good, old excel which allow people to do manipulation, sorts etc. on data.

Big data analytics - good example is Netflix. They collect a lot of data from all subcribers and suggest what should I watch next based on what I watched in past but also based on data from other subscribers but Big Data is also used for other purposes e.g risk management in bank after crash in 2008 when Lehman Brothers went bankrupt, helps to plan modernization in city.

The 3 V's of Big Data: <b>Volume</b> - you have to store huge amount of data, <b>Velocity</b> - it's expected that data will be processed even in real time and <b>Variety</b> - date can come from anywhere, files, streams, IoT Hub, social media, etc.

Categories of Big Data processing:
* ingest
* persist
* analyze
* visualize

# Azure machine learning
machine learning is about using existing data to forecast future behaviour, outcomes and trands. It's called machine learning because machine learn without being explicity programmed that means there are not specific set of instructions to produce specific output instead model is getting created. Then model is trained using real data so after learning model can take unknown data and make prediction base on what it already knows. In Azure there is Machine Learning Studio. There is also a Azure chat bot which is easy to integrate with your web service. <b>Azure provides Azure machine Learning Designer which allows you visually connect datasets and modules to create machine learning models.</b>

# Azure DevOps
Github is central repo while git is local repo on every developer machine. Microsoft purchased GitHUb in 2018. Azure provides <b>Azure DevOps boards</b> to monitor overall status (something similar to jira). Migration from Azure DevOps pipelines to GitHub Actions is really easy, just minor changes are required. Pipeline actions are wrote in YAML.

Azure provides DevTest Lab - pool of virtual machine to which admin has full access, can configure etc. and developers can claim one of this machine but just can use, install artifacts etc. Admin even decide what time there should be auto-shutdown to not pay when machine is not used. DevTest Labs creates labs consisting of pre-configured bases or Azure Resource Manager templates.


# Azure security
Authentication vs authorization. 
<b>Authentication</b> is the process of ascertaining that somebody really is who they claim to be. Examples: user login with a password, user proves she is a member of your team
<b>Authorization</b> refers to rules that determine who is allowed to do what. E.g. Adam may be authorized to create and delete databases, while Usama is only authorised to read. Examples: user can create a virtual machines, user is allowed access to the building.

First you authenticate, then authorization can occur.

# Azure Active Directory
When you ever login to Office365, Azure subscriptions. If you used any of this products and you created a user, a group etc. you used Azure Active Directory. Azure AD is not only securing access to Microsoft product, it can also be used to secure on premise applications. It's single sign-on you have one user and password for many applications.

# Role based access control
Some people should have admin role and do anything, some should have dev role and only be able to deploy.
RBAC:
* Roles allow you to group together sets of permissions
* we can make user or groups members of roles
* members of roles inherit all the permissions assigned to role
* when using roles: choose or create a role, assign role memebrs, configure a scope for a role

There are many buildin roles but there are Three of the most important build-in roles: owner(lets you manage everything including access to resources), contributor(lets you manage everything except granting access to resources), reader(lets you view everything but not make a changes)

# Azure tags
Azure tags:
* Key/value pairs
* Organizations should have a tagging policy enforced by Azure policies
* tags can be used: to control cost, to enforce security requirements, to deploy software 

Azure policy:
* is a collection of rules
* each policy is assigned to a scope such as an Azure subscription
* using Azure policy means that resources will remain compliant with corporate standards

Intiatives:
* are a collection of policies
* initiatives are assigned to a scope such as a resource group

<b>If you have tag assigned to one resource group it doesn't mean all resources in this resource group have the same tag. It is not inherited by default</b>

# Securing Azure Virtual Networks
Security:
* Physical security - managed by Microsoft 
* Identity and access - managed by you using Azure Active Directory
* Perimeter - standard DDoS protection enabled by default
* Network and application - network security groups, firewalls and gateways
* compute and data - os security, access control and encryption

# Azure firewall
There are two options: basic and standard. In standard option which is not free you can contact Azure DDoS experts during an attack, you can have post atack report and everything what is in basic option.

# Azure Information Protection
AIP is used to classify documents and emails, it applies labels to documents (secret, top secret, public etc.) then labeled documents can be protected.
Azure Key Vault (it's resource) is for protect our secrets. <b>Backup of key taken in one Azure location can be restored to key vault in another Azure location if both key vaults belongs to the same subscription. When Key Vault is accidentaly deleted it can't be recovered via Azure Portal, it can be recovered only via CLI or Powershell.</b>

# Azure Compliance
Compliance is 
* process of ensuring that you follow the standards or laws laid out by governing bodies
* people and process monitor system to detect and prevent violations


Complience monitoring can be complex and Azure provides serveral tools to help us asses and maintence our compliance posture

# Adopting Azure
You need to have subcription tied to your account. Management Group contains Subscriptions, subscription contains resource groups and resource group contains resources. Azure Active Directory can have many subscriptions but subscription can be connected to only one Azure Active Directory.
Types of subscription:
* The Basic support plan does not have any technical support for engineers.
* The Developer support plan has only technical support for engineers via email.
* The Standard, Professional Direct, and Premier support plans have technical support for engineers via email and phone
* The Premier support plan provides customer specific architectural support such as design reviews, performance tuning config and implementation delivered by Microsoft Azure specialists

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/cost_diffs.png?raw=true)


When you have free subscription and it will expire you won't be able to start virtual machine. 


# Service Level Agreement
SLA is a commitment between a service provider and its internal and external customers. An SLA outlines what the service provider will provide to its customers and the standards the provider will meet

# Azure previews
Microsoft has an Azure feature preview. These previews are for evaluation while features, product, services, regions are in beta or pre-release.

* Public preview - available for every Azure customer for evaluation process. They may not be SLA about this service, no support etc.
* Private preview - available for only specified Azure customers.

General Availability(GA) - After Azure preview features have been succesfully evaluated they are released for Azure customers becoming part of Azure's default product set. It's basically moving to GA. Then you get SLA, support etc.








# Example questions
1. When Azure machine is stopped you still pay storage costs associated to this virtual machine? Yes, you still have to pay for storage but you don't pay for stopped virtual machine.
2. Platform as a service allow you to control operating system? No, you don't control system in PaaS, you control application. You don't have access to operating system or virtual machine in PaaS. 
3. In SaaS you are responsible for installing the SaaS solution? No, you are responsible only for configuring the SaaS solution. Provider cares about infrastructure, you just pay for renting application and users can connect to Web App with a web browser. 
4. Using what kind of cloud can make company resign from it's own data center? Using Public Cloud, then everything is on provider. 
5. Which statement accurately describes the Modern Lifecycle Policy for Azure services? Microsoft provides a minimum of <b>12 months</b> notice before ending support for a service.
6. Which of the following terms refers to making a service available with no downtime for an extended period? <b>High Availability</b>
7. Which of the following is optimized for storing massive amounts of unstructured data, such as videos and images? Blobs. Azure Blob storage is Microsoft’s object storage solution for the cloud. <b>Blob storage is optimized for storing massive amounts of unstructured data, such as text or binary data.</b>
8. Azure Resource Manager templates use which format? Resource Manager templates are <b>JSON</b> files that define the resources you need to deploy for your solution. You can use the template to easily re-create multiple versions of your infrastructure, such as staging and production
9. What can require two or more elements for full authentication. How it's called? Multi-Factor Authentication (MFA) can require two or more elements for full authentication.
10. <b>With Azure Site Recovery (it provides fault tolerance, it replicates workloads running on physical and VMs from primary to secondary location) you can you can replicate data over VPN? No, you can replicate data over public internet with ExpressRoute</b>
11. What's the leagal agreement between Azure customer and Microsoft secure and process data? Data Protection Addendum (DPA)
12. Let's assume you have 100 offices and you want to generate several billing reports from Azure. Each report will contain the Azure resource utilization for each office. You can use resource tags. Tags consist of pairs key/value. You can create 100 tags and tag every resource and later generate report based on tag.
13. Can Azure subscription contain many administrator account? Yes, you can have many administrator account
14. Do you need Microsoft account to manage subscription? No, you need Azure Active Directory account to manage subscription, not Microsoft account. An account is created in the Azure Active Directory when you create the subscription. Later additional accounts can be created in the AAD to manage the subscription
15. Does Azure resource group contains subsriptions? No, Resource Groups are containers for resources. Subscriptions contain resource groups
16. If you use free account (only one free account per Microsoft account) it gives you 12 months access to the most popular free services. After 12 months free acc are removed.
17. Copying data via VPN from on-premises server to Azure don't generate cost, if you copy from Azure to on-premises you have to pay. Data ingress over a VPN is data ‘coming in’ to Azure over the VPN. You are not charged data transfer costs for data ingress. Data egress over a VPN is data ‘going out’ of Azure over the VPN. You are charged for data egress.
18. All Azure services that are in public preview are excluded from the Service Level Aggrements (SLA). PREVIEWS ARE PROVIDED "AS-IS," "WITH ALL FAULTS," AND "AS AVAILABLE," AND ARE EXCLUDEDFROM THE SERVICE LEVEL AGREEMENTS AND LIMITED WARRANTY. For virtual machines uptime is guaranteed - VM connectivity at least 99.9%.
19. <b>Azure Cost Management doesn't estimate up-front cost for cloud. Azure Pricing Calculator can do it.</b> 
20. Azure Application Insights detects and diagnoses anomalies in web apps
21. Azure Event Hubs is a big data streaming platform and event ingestion service. It can receive and process millions of events per second.
22. PowerApps lets you quickly build app with little or no code, that's all it can do.
23. Azure Databricks is an Apache Spark-based analytics service
