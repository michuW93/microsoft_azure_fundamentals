1. App is storing medical documents, if the stored intake forms are downloaded from storage by a third party, 
the contents of the forms must not be compromised. <br>
We can use <b>Azure Key vault and public key encryption</b> and store encrypted form in Azure Storage Blob storage

2. Configure Azure Disk Encryption for the VM: 
Keyvault -> Keyvault Key -> VirtualMachine -> VM encryption -> all (all means encrypt both data and operating system)
`az keyvault create` then `az keyvault key create` then `az vm create` then `az vm encryption`

3. Requirements: all API calls must be authenticated and callers to the API must not send credentials. Answer: <b>Managed Identity</b> <br>
Basic and Client Certificate will send credential to the API.

4. You have an Azure user account that has access to two subscriptions. You need to retrieve a storage account key secret from Azure Key Vault. </br>
`Get-AzSubscription` because there is more than 1, then `Set-AzContext -SubscriptionId`, then `Get-AzStorageAccountKey`, then `Get-AzKeyVaultSecret -VaultName`

5. You must grant a VM access to specific resource groups in Azure Resource Manager. You need to obtain an Azure Resource Manager access token. <br>
Answer: <b>We need to run `Invoke-RestMethod` cmdlet</b> (Sends an HTTP or HTTPS request to a RESTful web service) to make a request to the local managed 
identity for Azure resources endpoint.

6. Azure AD users must be able to login to the website. auth2Permissions can only accept collections value like an array, not boolean.
<b>oauth2AllowImplicitFlow accepts boolean value</b>. `oauth2AllowImplicitFlow : true`

7. `Start-AzureStorageBlobCopy` to copy blobs between containers.

8. To purge specific file then `single path purge` should be use.

9. Use API Management to access the services, use OpenID Connect for authentication and prevent anonymous usage. 
Answer: <b>validate-jwt</b> policy in API Management to validate OAuth token presented in each incoming API request. Valid requests can be passed to the API. 

10. Inbound - here we need to detect the user identity in the user request and then store the data in the cache. 
So, we need to look at the incoming request for this e.g Cache-lookup-value and cache-store-value. 
Outbound - here we need to update the response body so it should go in the output section e.g find and replace policy.

11. You need to develop code to access a secret stored in Azure Key Vault: `Environment.GetEnvironmentVariable("KEY_VAULT_URI")`, 
then `new SecretClient(new Uri(kvUri), new <b>DefaultAzureCredential()</b>)` 

12. find and replace in `<outbound>` because it's changing response body

13. You have two Hyper-V hosts named Host1 and Host2. Host1 has an Azure virtual machine named VM1 that was deployed by using a custom Azure Resource
Manager template. You need to move VM1 to Host2. What should you do? <br> 
When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.
<b>From the Redeploy blade, click Redeploy.</b>

15. You want to deploy an ARM template using C#. The template deploys a single virtual machine in a new virtual network with single subnet. 
Which template files are necessary?
`createVMTemplate.json` as the template file (it must be .json because ARM template!), 
`parameters.json` as the parameters file(it also must be .json!), 
`azureauth.properties` as the authorization file

16. Standard tier plan and above supports Kafka messages in Event Hub. The Basic tier does not.

17. `set AZCOPY_CONCURENCY_VALUE` on windows = `export AZCOPY_CONCURENCY_VALUE` on linux and MacOs. 
This environment variable can increase the throughput when transferring small files and specifies the number of concurrent requests that can occur.

18. <b>Blob permission</b> allow an anonymous user to read all the blobs in the container but not enumerate them.

19. <b>Timespan can be used only if the function app is running on a dedicated app service plan</b>, not available for consumption and premium plan.

20. To set up exception reporting, you will need the following:
* ensure application insights extension site extension is updated
* add application monitoring extension
* install application insights SDK in your app code

20. Partition key can be skipped if your collection is not partitioned i.e does not have a partition key defined during creation.

21. you want to use a simple SQL API-based solution to remove all date before some date. 
Answer: Time to Live because you can set TTL for documents and/or containers.
You can enable TTL for documents and wait for the cosmos DB cleanup to start.

22. how to create alert?
* in the azure portal under Azure CosmosDB properties, add an Alert Rule
* in the Azure CLI, execute the command `az monitor alert create`
* use an azure PowerShell script to execute `Add-AzMetricAlertRule`

23. Azure Notification Hub can be used for sending push notifications to Android, iOS, Windows and more

24. Azure Event Hubs enable you to automatically capture the streaming data in Event Hubs in Azure Blob storage or Azure Data Lake Storage account

25. You have been using the VM in Azure DevTest Labs. After completing your assigned development task, what must you do to make the VM available
to another developer who is responsible for the next part of the solution? Unclaim the VM and allow the developer to claim it and take over.

26. `--vnet-subnet-id` is optional and specifies the subnet in a VNet where the new AKS cluster will be deployed

27. In Azure Monitor you can see <b>`CPU usage, network usage and disk operations per second`</b>. To see boot diagnostic and application logs you need to enable it,
it's not enabled by default

28. Azure Cosmos DB accounts that are configured to use strong consistency cannot associate more than one Azure region with 
their Azure Cosmos DB account.

29. <b>You cannot implement user delegation SAS though the stored access policy feature</b>. Stored access policies are not supported for a user delegation SAS.
A user delegation SAS is only supported for the Blob service.

30. <b>Durable timers are limited to seven days</b>. The workaround is to simulate using the timer API in a loop, such as a while loop or a for loop

31. port <b>443</b> HTTPS, ports 5671-5672 for advanced message queuing protocol (AMQP), ports 9350-9354 for listeners on service bus relay over TCP

32. NewGUID(.NET) is deterministic API, GUIDs/UUIDs is not deterministic. Deterministic API returns the same value given the same input.

33. you need the workspace ID and workspace (Premium) key to implement Azure OMS log analytics.

34. add a message that does not expire: `await theQueue.AddMessageAsync` and inside `Timespan.FromSeconds(-1)`

35. You have RBAC application. Role is sales but there are some people in this role which shouldn't have access to create customers. 
How to do it without adding new role? Build and register a policy.

36. <b>Helm</b> helps you manage Kubernetes application - Helm charts help you define, install, and upgrade even the most complex Kubernetes applications. 
<b>kubectl</b> - Kubernetes command line tool which allows to run commands against Kubernetes clusters. 
<b>ingress controller</b> is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.

37. You have developed an event-based solution that uses Azure Service Bus. Because of reaching subscription spending limits, 
the system has suspended entities, and you want to reactivate system-disabled entities. Answer: <b>Restore the system-disabled entity</b> 

38. API Management tier consumption does not support rate-limit-by-key or quota-by-key. You need premium tier to use it

39. `Microsoft.Azure.Management.Redis.Fluent` is not a directive which can be used for CDN

40. you can form a partition key by concatenating multiple property values into a single artificial partitionKey. It's called synthetic key then

41. steps to follow to create the app registration to Azure AD:
* sign in to the Azure Portal
* search for and select azure active directory
* select app registration, then new registration
* enter a display name for you application

42. You are using Azure AD and you need to add multifactor authentication:
* In azure AD, create a new conditional access policy
* upgrade to azure AD premium

43. Azure Cosmos DB provides new RBAC role, `Cosmos DB Operator`.
This role lets you provision Azure Cosmos accounts, databases and containers but can't access the keys that are required to access the data.

44. <b>Azure CDN from Akamai</b> purge request is processing the fastest.

45. UseAzureAppConfiguration to allow the configuration setting registered for refresh to be updated while ASP.NET core web app 
continues to receive requests

46. The JWT validation policy pre-authorizes requests in API Management by validation the access tokens of each incoming request.

47. In the dynamic data masking configuration page you need to choose `schema, table, column`

48. Problems with VM. When it's related to backup and restore then `Azure backup`, when it's related to performance then `Accelerated Networking`

49. You need to implement code that creates the object which is used to create indexes in the azure search service. You should use `SeachServiceClient` and `SearchIndexClient`

50. You need to ensure that the web app automatically scales when CPU load is about 85 percent and minimize costs.
* configure the web app to the Standard App Service Tier
* enable autoscaling on the web app
* add a scale rule
* add a scale condition

51. In Azure Table Storage you need to insert multiple sets of user informations.
<b>`TableBatchOperation op = new TableBatchOperation()`</b> then <b>`table.executeBatch(op)`</b>

52. Create a new role reusing a default role definition. <b>`Set-AzureRmRoleDefinition Input-File C:/SupportRole.json`</b>

53. You want to avoid a single hot partition key. You can use a partition key with <b>pre-calculated</b> or random suffixes.
We don't want prefix, a suffix appends the value to the end, which makes it easier to read.

54. How to view the logged information in an easy manner? Open the <b>freb.xsl</b> file, failed request traces are stored in XML files named fr###.xml

55. Sharding pattern is used for splitting data across databases, disks, files, or partitions. It can prevent Azure Cosmos DB from being overloaded.
<b>Sharding pattern can resolve database issues for SQL and NoSQL but not MySQL</b>

56. to build cluster named NutexAKSCluster for the resourcegroup test: `az aks create --name NutexAKSCluster --resource-group test`

57. Purpose of `change feed` is to provide transaction logs of all the changes that occur to the blobs and the blob metadata in storage account. The change feed provides ordered, guaranteed, durabled read only logs of changes.

58. You have downloaded an Azure Resource Manager template to deploy numerous virtual machines. 
The template is based on a current virtual machine, but must be adapted to reference an administrative password.
You need to make sure that the password is not stored in plain text.
You are preparing to create the necessary components to achieve your goal.
Which of the following should you create to achieve your goal?
Select and Place: <b>an Azure Key Vault</b> and <b>an access policy</b>

59. You need to deploy the YAML manifest file for the application.
<b>`kubectl apply -f myapp.yaml`</b> applies a configuration change to a resource from a file or stdin.

60. Your company has a web app named WebApp1.
You use the WebJobs SDK to design a triggered App Service background task that automatically invokes a function in the code every time new data is received in a queue.
You are preparing to configure the service processes a queue data item.
Which of the following is the service you should use? </br>
<b>WebJobs</b>

61. Your company has an Azure subscription.
You need to deploy a number of Azure virtual machines to the subscription by using Azure Resource Manager (ARM) templates. The virtual machines will be included in a single availability set.
You need to ensure that the ARM template allows for as many virtual machines as possible to remain accessible in the event of fabric failure or maintenance.
* Which of the following is the value that you should configure for the platformFaultDomainCount property?
<b>Max value</b> - The number of fault domains for managed availability sets varies by region - either two or three per region.

* Which of the following is the value that you should configure for the platformUpdateDomainCount property?
<b>40</b> Each virtual machine in your availability set is assigned an update domain and a fault domain by the underlying Azure platform. For a given availability set, five non-user-configurable update domains are assigned by default (Resource Manager deployments can then be increased to provide up to 20 update domains) to indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.

62. You are creating an Azure Cosmos DB account that makes use of the SQL API. Data will be added to the account every day by a web application.
You need to ensure that an email notification is sent when information is received from IoT devices, and that compute cost is reduced.
You decide to deploy a function app.
Which of the following should you configure the function app to use? Answer by dragging the correct options from the list to the answer area. </br>
Select and Place: <b>Consumption plan</b> and <b>SendGrid binding</b>

63. Your company has an on-premises deployment of MongoDB, and an Azure Cosmos DB account that makes use of the MongoDB API.
You need to devise a strategy to migrate MongoDB to the Azure Cosmos DB account.
You include the Data Management Gateway tool in your migration strategy. </br> <b>mongorestore</b>

64. You are developing an e-Commerce Web App.
You want to use Azure Key Vault to ensure that sign-ins to the e-Commerce Web App are secured by using Azure App Service authentication and Azure Active
Directory (AAD).
What should you do on the e-Commerce Web App?
<b>Enable Managed Service Identity (MSI)</b>. - A managed identity from Azure Active Directory allows your app to easily access other AAD-protected resources such as Azure Key Vault.

65. Your Azure Active Directory Azure (Azure AD) tenant has an Azure subscription linked to it.
Your developer has created a mobile application that obtains Azure AD access tokens using the OAuth 2 implicit grant type.
The mobile application must be registered in Azure AD.
You require a redirect URI from the developer for registration purposes.
No change required - For Native Applications you need to provide a Redirect URI, which Azure AD will use to return token responses.

66. You have an Azure Active Directory (Azure AD) tenant.
You want to implement multi-factor authentication by making use of a conditional access policy. The conditional access policy must be applied to all users when they access the Azure portal.
Which three settings should you configure?
<b>users and groups, cloud apps, grant</b><br>
The conditional access policy must be applied or assigned to <b>Users and Groups</b>. <br>
The conditional access policy must be applied when users access the Azure portal, which is a <b>cloud app</b>. That is: Microsoft Azure Management <br>
Access control must require multi-factor authentication when <b>granting</b> access. <br>

67. You manage an Azure SQL database that allows for Azure AD authentication.
You need to make sure that database developers can connect to the SQL database via Microsoft SQL Server Management Studio (SSMS). You also need to make sure the developers use their on-premises Active Directory account for authentication. Your strategy should allow for authentication prompts to be kept to a minimum.
Which of the following should you implement? </br>
<b>Active Directory integrated authentication. </b>
Azure AD can be the initial Azure AD managed domain. Azure AD can also be an on-premises Active Directory Domain Services that is federated with the Azure
AD.
Using an Azure AD identity to connect using SSMS or SSDT

68. You have developed a Web App for your company. The Web App provides services and must run in multiple regions.
You want to be notified whenever the Web App uses more than 85 percent of the available CPU cores over a 5 minute period. Your solution must minimize costs.
Which command should you use? To answer, select the appropriate settings in the answer area.
`--condition "avg Percentage CPU > 85" --window-size 5m`

69. You are configuring a web app that delivers streaming video to users. The application makes use of continuous integration and deployment.
You need to ensure that the application is highly available and that the users streaming experience is constant. You also want to configure the application to store data in a geographic location that is nearest to the user.
Solution: <b>You include the use of an Azure Content Delivery Network (CDN) in your design.</b>

70. You develop a Web App on a tier D1 app service plan.
You notice that page load times increase during periods of peak traffic.
You want to implement automatic scaling when CPU load is above 80 percent. Your solution must minimize costs.
What should you do first?
<b>Configure the web app to the Standard App Service Tier.</b> The Standard tier supports auto-scaling, and we should minimize the cost. We can then enable autoscaling on the web app, add a scale rule and add a Scale condition.

71. Your company's Azure subscription includes an Azure Log Analytics workspace.
Your company has a hundred on-premises servers that run either Windows Server 2012 R2 or Windows Server 2016, and is linked to the Azure Log Analytics workspace. The Azure Log Analytics workspace is set up to gather performance counters associated with security from these linked servers.
You must configure alerts based on the information gathered by the Azure Log Analytics workspace.
You have to make sure that alert rules allow for dimensions, and that alert creation time should be kept to a minimum. Furthermore, a single alert notification must be created when the alert is created and when the alert is resolved.
You need to make use of the necessary signal type when creating the alert rules.
Which of the following is the option you should use?
<b>The Metric signal type</b> - Metric alerts in Azure Monitor provide a way to get notified when one of your metrics cross a threshold. Metric alerts work on a range of multi-dimensional platform metrics, custom metrics, Application Insights standard and custom metrics.
Note: Signals are emitted by the target resource and can be of several types. Metric, Activity log, Application Insights, and Log.

72. You are developing a .NET Core MVC application that allows customers to research independent holiday accommodation providers.
You want to implement Azure Search to allow the application to search the index by using various criteria to locate documents related to accommodation.
You want the application to allow customers to search the index by using regular expressions.
What should you do?
<b>Configure the QueryType property of the SearchParameters class</b> - The SearchParameters.QueryType Property gets or sets a value that specifies the syntax of the search query. The default is 'simple'. Use 'full' if your query uses the Lucene query syntax.
You can write queries against Azure Search based on the rich Lucene Query Parser syntax for specialized query forms: wildcard, fuzzy search, proximity search, regular expressions are a few examples.

73. You are a developer at your company.
You need to update the definitions for an existing Logic App.
What should you use?
<b>the Logic App Code View</b>

74. You are developing a solution for a public facing API.
The API back end is hosted in an Azure App Service instance. You have implemented a RESTful service for the API back end.
You must configure back-end authentication for the API Management service instance. </br>
Solution: <b>You configure Client cert gateway credentials for the Azure resource.</b>
YES - API Management allows to secure access to the back-end service of an API using client certificates.

75. You are developing a .NET Core MVC application that allows customers to research independent holiday accommodation providers.
You want to implement Azure Search to allow the application to search the index by using various criteria to locate documents related to accommodation venues.
You want the application to list holiday accommodation venues that fall within a specific price range and are within a specified distance to an airport.
What should you do?
<b>Configure the Filter property of the SearchParameters class.</b>

76. You are a developer at your company.
You need to edit the workflows for an existing Logic App.
What should you use?
<b>the Enterprise Integration Pack (EIP)</b> - For business-to-business (B2B) solutions and seamless communication between organizations, you can build automated scalable enterprise integration workflows by using the Enterprise Integration Pack (EIP) with Azure Logic Apps.

77. You are a developer for a company that provides a bookings management service in the tourism industry. You are implementing Azure Search for the tour agencies listed in your company's solution.
You create the index in Azure Search. You now need to use the Azure Search .NET SDK to import the relevant data into the Azure Search service.
Which three actions should you perform in sequence? To answer, move the appropriate actions from the list of actions from left to right and arrange them in the correct order.
* Create the SearchIndexClient object to connect to the search index.
* Create an IndexBatch that contains the documents which must be added.
* Call the Documents.Index method of the SearchIndexClient and pass the IndexBatch

78. You are developing an application that applies a set of governance policies for internal and external services, as well as for applications.
You develop a stateful ASP.NET Core 2.1 web application named PolicyApp and deploy it to an Azure App Service Web App. The PolicyApp reacts to events from
Azure Event Grid and performs policy actions based on those events.
You have the following requirements:
✑ Authentication events must be used to monitor users when they sign in and sign out.
✑ All authentication events must be processed by PolicyApp.
✑ Sign outs must be processed as fast as possible.
What should you do?
<b>Add a subject prefix to sign-out events. Create an Azure Event Grid subscription. Configure the subscription to use the subjectBeginsWith filter.</b>

79. You are developing a C++ application that compiles to a native application named process.exe. The application accepts images as input and returns images in one of the following image formats: GIF, PNG, or JPEG.
You must deploy the application as an Azure Function.
You need to configure the function and host json files.
Box 1: "type": "http"
Box 2: "customHandler": { "description":{
A custom handler is defined by configuring the host.json file with details on how to run the web server via the customHandler section.
The customHandler section points to a target as defined by the defaultExecutablePath.
Example:
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
Box 3: "enableForwardingHttpRequest": false
Incorrect:
For HTTP-triggered functions with no additional bindings or outputs, you may want your handler to work directly with the HTTP request and response instead of the custom handler request and response payloads. This behavior can be configured in host.json using the enableForwardingHttpRequest setting.
At the root of the app, the host.json file is configured to run handler.exe and enableForwardingHttpRequest is set to true.

80. You are implementing a software as a service (SaaS) ASP.NET Core web service that will run as an Azure Web App. The web service will use an on-premises
SQL Server database for storage. The web service also includes a WebJob that processes data updates. Four customers will use the web service.
✑ Each instance of the WebJob processes data for a single customer and must run as a singleton instance.
✑ Each deployment must be tested by using deployment slots prior to serving production data.
✑ Azure costs must be minimized.
✑ Azure resources must be located in an isolated network.
You need to configure the App Service plan for the Web App.
How should you configure the App Service plan? </br>
Number of VM instances: <b>4</b>, Pricing tier: <b>isolated</b>

81. You are a developer for a software as a service (SaaS) company that uses an Azure Function to process orders. The Azure Function currently runs on an Azure
Function app that is triggered by an Azure Storage queue.
You are preparing to migrate the Azure Function to Kubernetes using Kubernetes-based Event Driven Autoscaling (KEDA).
You need to configure Kubernetes Custom Resource Definitions (CRD) for the Azure Function.
Which CRDs should you configure?
<b>Azure function code: Deployment</b> </br>
<b>Pooling interval: ScaledObject </b> </br>
<b>Azure Storage connection String: Secret</b></br>

82. You develop and deploy an Azure App Service API app to a Windows-hosted deployment slot named Development. You create additional deployment slots named Testing and Production. You enable auto swap on the Production deployment slot.
You need to ensure that scripts run and resources are available before a swap operation occurs.
* <b>Enable auto swap for the Testing slot. Deploy the app to the Testing slot.</b> 
* <b>Disable auto swap. Update the app with a method named statuscheck to run the scripts. Re-enable auto swap and deploy the app to the Production slot.</b>

83. You are developing a serverless Java application on Azure. You create a new Azure Key Vault to work with secrets from a new Azure Functions application.
The application must meet the following requirements:
✑ Reference the Azure Key Vault without requiring any changes to the Java code.
✑ Dynamically add and remove instances of the Azure Functions host based on the number of incoming application events.
✑ Ensure that instances are perpetually warm to avoid any cold starts.
✑ Connect to a VNet.
✑ Authentication to the Azure Key Vault instance must be removed if the Azure Function application is deleted.
You need to grant the Azure Functions application access to the Azure Key Vault.
Which three actions should you perform in sequence?
* create the Azure Functions app with a Consumption plan type
* create a user-assigned managed identity for the application
* create an access policy in Azure Key Vault for the application identity

84. You develop a website. You plan to host the website in Azure. You expect the website to experience high traffic volumes after it is published.
You must ensure that the website remains available and responsive while minimizing cost.
You need to deploy the website.
What should you do?</br>
<b>Deploy the website to an App Service that uses the Standard service tier. Configure the App Service plan to automatically scale when the CPU load is high.</b>

85. You develop an HTTP triggered Azure Function app to process Azure Storage blob data. The app is triggered using an output binding on the blob.
The app continues to time out after four minutes. The app must process the blob data.
You need to ensure the app does not time out and processes the blob data.
Solution: <b>Pass the HTTP trigger payload into an Azure Service Bus queue to be processed by a queue trigger function and return an immediate HTTP success response.</b>
Does the solution meet the goal? YES - Large, long-running functions can cause unexpected timeout issues. General best practices include:
Whenever possible, refactor large functions into smaller function sets that work together and return responses fast. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it's common for webhooks to require an immediate response. You can pass the
HTTP trigger payload into a queue to be processed by a queue trigger function. This approach lets you defer the actual work and return an immediate response.

86. You develop a software as a service (SaaS) offering to manage photographs. Users upload photos to a web service which then stores the photos in Azure
Storage Blob storage. The storage account type is General-purpose V2.
When photos are uploaded, they must be processed to produce and save a mobile-friendly version of the image. The process to produce a mobile-friendly version of the image must start in less than one minute.
You need to design the process that starts the photo processing.
Solution: <b>Move photo processing to an Azure Function triggered from the blob upload.</b>
Does the solution meet the goal? YES - Azure Storage events allow applications to react to events. Common Blob storage event scenarios include image or video processing, search indexing, or any file- oriented workflow.
Events are pushed using Azure Event Grid to subscribers such as Azure Functions, Azure Logic Apps, or even to your own http listener.
Note: Only storage accounts of kind StorageV2 (general purpose v2) and BlobStorage support event integration. Storage (general purpose v1) does not support integration with Event Grid.

87. You are developing an application that uses Azure Blob storage.
The application must read the transaction logs of all the changes that occur to the blobs and the blob metadata in the storage account for auditing purposes. The changes must be in the order in which they occurred, include only create, update, delete, and copy operations and be retained for compliance reasons.
You need to process the transaction logs asynchronously.
What should you do? <b>Enable the change feed on the storage account and process all changes for available events. </b> Change feed support in Azure Blob Storage
The purpose of the change feed is to provide transaction logs of all the changes that occur to the blobs and the blob metadata in your storage account. The change feed provides ordered, guaranteed, durable, immutable, read-only log of these changes. Client applications can read these logs at any time, either in streaming or in batch mode. The change feed enables you to build efficient and scalable solutions that process change events that occur in your Blob Storage account at a low cost.

88. You are developing an Azure Function App that processes images that are uploaded to an Azure Blob container.
Images must be processed as quickly as possible after they are uploaded, and the solution must minimize latency. You create code to process images when the
Function App is triggered.
You need to configure the Function App.
What should you do? <b>Use a Consumption plan. Configure the Function App to use an Azure Blob Storage trigger.</b> The Blob storage trigger starts a function when a new or updated blob is detected. The blob contents are provided as input to the function.
The Consumption plan limits a function app on one virtual machine (VM) to 1.5 GB of memory.

89. You are configuring a development environment for your team. You deploy the latest Visual Studio image from the Azure Marketplace to your Azure subscription.
The development environment requires several software development kits (SDKs) and third-party components to support application development across the organization. You install and customize the deployed virtual machine (VM) for your development team. The customized VM must be saved to allow provisioning of a new team member development environment.
You need to save the customized VM for future provisioning. </br>
Generalize the VM - Azure PowerShell </br>
Store images - Azure Blob Storage

90. You are preparing to deploy a website to an Azure Web App from a GitHub repository. The website includes static content generated by a script.
You plan to use the Azure Web App continuous deployment feature.
You need to run the static generation script before the website starts serving traffic.
<b>Add the path to the static content generation tool to WEBSITE_RUN_FROM_PACKAGE setting in the host.json file </b> and <b>Create a file named .deployment in the root of the repository that calls a script which generates the static content and deploys the website </b>

91. You are developing an application to use Azure Blob storage. You have configured Azure Blob storage to include change feeds.
A copy of your storage account must be created in another region. Data must be copied from the current storage account to the new storage account directly between the storage servers.
You need to create a copy of the storage account in another region and copy the data.
* create a new template deployment
* export a resource manager template
* modify the template by changing the storage account name and region
* deploy the template to create a new storage account in the target region
* use azcopy to copy the data to the new storage account 

92. You are preparing to deploy an Azure virtual machine (VM)-based application.
The VMs that run the application have the following requirements:
✑ When a VM is provisioned the firewall must be automatically configured before it can access Azure resources.
✑ Supporting services must be installed by using an Azure PowerShell script that is stored in Azure Storage.
You need to ensure that the requirements are met.
Firewall configuration - <b>Run command</b></br> 
Supporting services script - <b>Hybrid Runbook Worker</b>

93. You develop a software as a service (SaaS) offering to manage photographs. Users upload photos to a web service which then stores the photos in Azure
Storage Blob storage. The storage account type is General-purpose V2.
When photos are uploaded, they must be processed to produce and save a mobile-friendly version of the image. The process to produce a mobile-friendly version of the image must start in less than one minute.
You need to design the process that starts the photo processing.
Solution: <b>Create an Azure Function app that uses the Consumption hosting model and that is triggered from the blob upload.</b> YES - In the Consumption hosting plan, resources are added dynamically as required by your functions.

94. You are developing a web app that is protected by Azure Web Application Firewall (WAF). All traffic to the web app is routed through an Azure Application
Gateway instance that is used by multiple web apps. The web app address is contoso.azurewebsites.net.
All traffic must be secured with SSL. The Azure Application Gateway instance is used by multiple web apps.
You need to configure the Azure Application Gateway for the web app.
* <b>In the Azure Application Gateway's HTTP setting, enable the Use for App service setting. </b>
* <b>In the Azure Application Gateway's HTTP setting, set the value of the Override backend path option to contoso22.azurewebsites.net.</b>

95. You are developing a web application that runs as an Azure Web App. The web application stores data in Azure SQL Database and stores files in an Azure
Storage account. The web application makes HTTP requests to external services as part of normal operations.
The web application is instrumented with Application Insights. The external services are OpenTelemetry compliant.
You need to ensure that the customer ID of the signed in user is associated with all operations throughout the overall system.
<b>Add the customer ID for the signed in user to the CorrelationContext in the web application</b>

96. You are developing an Azure Function App. You develop code by using a language that is not supported by the Azure Function App host. The code language supports HTTP primitives.
You must deploy the code to a production Azure Function App environment.
You need to configure the app for deployment.
Which configuration values should you use?
Publish <b>docker container</b>, Runtime stack <b>PowerShell core</b>, Version: <b>7.0</b>

97.You are developing an Azure Durable Function to manage an online ordering process.
The process must call an external API to gather product discount information.
You need to implement the Azure Durable Function. </br>
<b>Orchestrator</b> and <b>entity</b>

98. You develop Azure solutions.
You must connect to a No-SQL globally-distributed database by using the .NET API.
You need to create an object to configure and execute requests in the database.
<b>new CosmosClient(EndpointUri, PrimaryKey);</b>

99. You are developing an Azure Cosmos DB solution by using the Azure Cosmos DB SQL API. The data includes millions of documents. Each document may contain hundreds of properties.
The properties of the documents do not contain distinct values for partitioning. Azure Cosmos DB must scale individual containers in the database to meet the performance needs of the application by spreading the workload evenly across all partitions over time.
You need to select a partition key.
Which two partition keys can you use? </br>
<b>a concatenation of multiple property values with a random suffix appended</b> </br>
<b>a hash suffix appended to a property value</b>

100. You develop and deploy a web application to Azure App Service. The application accesses data stored in an Azure Storage account. The account contains several containers with several blobs with large amounts of data. You deploy all Azure resources to a single region.
You need to move the Azure Storage account to the new region. You must copy all data to the new region.
What should you do first?
<b>Export the Azure Storage account Azure Resource Manager template</b>

101. An organization deploys Azure Cosmos DB.
You need to ensure that the index is updated as items are created, updated, or deleted.
What should you do?
<b>Set the indexing mode to Consistent.</b>

102. You are developing a .Net web application that stores data in Azure Cosmos DB. The application must use the Core API and allow millions of reads and writes.
The Azure Cosmos DB account has been created with multiple write regions enabled. The application has been deployed to the East US2 and Central US regions.
You need to update the application to support multi-region writes.
What are two possible ways to achieve this goal?</br>
<b>Update the ConnectionPolicy class for the Cosmos client and set the UseMultipleWriteLocations property to true.</b> </br>
<b>Create and deploy a custom conflict resolution policy.</b>
  
103. You are developing a web application by using the Azure SDK. The web application accesses data in a zone-redundant BlockBlobStorage storage account.
The application must determine whether the data has changed since the application last read the data. Update operations must use the latest data changes when writing data to the storage account.
You need to implement the update operations.
Which values should you use? </br>
HTTP Header Value: <b>Last Modified</b> </br>
Conditional Header: <b>If-Modified-Since</b>

104. An organization deploys a blob storage account. Users take multiple snapshots of the blob storage account over time.
You need to delete all snapshots of the blob storage account. You must not delete the blob storage account itself.
How should you complete the code segment?
<b>`Azure.Storage.Blobs.Models.DeleteSnapshotsOption.OnlySnapshots`</b>
  
105. You are developing a Java application that uses Cassandra to store key and value data. You plan to use a new Azure Cosmos DB resource and the Cassandra
API in the application. You create an Azure Active Directory (Azure AD) group named Cosmos DB Creators to enable provisioning of Azure Cosmos accounts, databases, and containers.
The Azure AD group must not be able to access the keys that are required to access the data.
You need to restrict access to the Azure AD group.
Which role-based access control should you use?
  <b>Cosmos DB Operator</b>

106. You are developing a website that will run as an Azure Web App. Users will authenticate by using their Azure Active Directory (Azure AD) credentials.
You plan to assign users one of the following permission levels for the website: admin, normal, and reader. A user's Azure AD group membership must be used to determine the permission level.
You need to configure authorization.
Solution: </br>
✑ Create a new Azure AD application. In the application's manifest, set value of the groupMembershipClaims option to All.
✑ In the website, use the value of the groups claim from the JWT for the user to determine permissions.

107. You provide an Azure API Management managed web service to clients. The back-end web service implements HTTP Strict Transport Security (HSTS).
Every request to the backend service must include a valid HTTP authorization header.
You need to configure the Azure API Management instance with an authentication policy.
Which two policies can you use?
<b>Certificate Authentication</b> and <b>OAuth Client Credential Grant</b> 

108. You are developing an ASP.NET Core website that can be used to manage photographs which are stored in Azure Blob Storage containers.
     Users of the website authenticate by using their Azure Active Directory (Azure AD) credentials.
     You implement role-based access control (RBAC) role permissions on the containers that store photographs. You assign users to RBAC roles.
     You need to configure the website's Azure AD Application so that user's permissions can be used with the Azure Blob containers.
     How should you configure the application?
Azure Storage: <b>user_impersonation delegated</b> </br>
Microsoft Graph: User.Read <b>delegated</b>

109. You have an application that includes an Azure Web app and several Azure Function apps. Application secrets including connection strings and certificates are stored in Azure Key Vault.
     Secrets must not be stored in the application or application runtime environment. Changes to Azure Active Directory (Azure AD) must be minimized.
     You need to design the approach to loading application secrets.
     What should you do?
<b>Create a system assigned Managed Identity in each App Service with permission to access Key Vault.</b>

110. You are developing a medical records document management website. The website is used to store scanned copies of patient intake forms.
     If the stored intake forms are downloaded from storage by a third party, the contents of the forms must not be compromised.
     You need to store the intake forms according to the requirements.
     Solution:
* Create an Azure Key Vault key named skey.
* Encrypt the intake forms using the public key portion of skey.
* Store the encrypted data in Azure Blob storage.
   Does the solution meet the goal? YES

111. You develop Azure solutions.
     You must grant a virtual machine (VM) access to specific resource groups in Azure Resource Manager.
     You need to obtain an Azure Resource Manager access token.
     Solution: Run the Invoke-RestMethod cmdlet to make a request to the local managed identity for Azure resources endpoint.
     Does the solution meet the goal? YES

112. You develop an app that allows users to upload photos and videos to Azure storage. The app uses a storage REST API call to upload the media to a blob storage account named Account1. You have blob storage containers named Container1 and Container2.
     Uploading of videos occurs on an irregular basis.
     You need to copy specific blobs from Container1 to Container2 when a new video is uploaded.
     What should you do?
<b>Create an Event Grid topic that uses the Start-AzureStorageBlobCopy cmdlet </b>

113. You are developing an Azure App Service REST API.
     The API must be called by an Azure App Service web app. The API must retrieve and update user profile information stored in Azure Active Directory (Azure AD).
     You need to configure the API to make the updates.
     Which two tools should you use?
<b>Microsoft Graph API</b> and <b>Azure API Management</b>

114. You develop a REST API. You implement a user delegation SAS token to communicate with Azure Blob storage.
     The token is compromised. You need to revoke the token.
     What are two possible ways to achieve this goal? Each correct answer presents a complete solution.
     <b>Revoke the delegation key</b> and <b>Delete the stored access policy.</b>

115. You develop and deploy an Azure Logic app that calls an Azure Function app. The Azure Function app includes an OpenAPI (Swagger) definition and uses an
     Azure Blob storage account. All resources are secured by using Azure Active Directory (Azure AD).
     The Azure Logic app must securely access the Azure Blob storage account. Azure AD resources must remain if the Azure Logic app is deleted.
     You need to secure the Azure Logic app.
     What should you do?
     <b>Create a user-assigned managed identity and assign role-based access controls.</b>

116. You deploy an Azure App Service web app. You create an app registration for the app in Azure Active Directory (Azure AD) and Twitter. 
the app must authenticate users and must use SSL for all communications. The app must use Twitter as the identity provider. 
You need to validate the Azure AD request in the app code. What should you validate? <b>ID token header</b>

117. You need to register the app with an active Azure Active Directory tenant.
* In App Registrations select New registration
* select the Azure AD instance
* create a new application and provide the name, account type and redirect URL

118. You need to implement code that creates the object which is used to create indexes in the Azure Search service.
you should use <b>SearchIndexClient</b> and <b>SearchServiceClient</b>

119. You are developing an Azure solution to collect point-of-sale (POS) device data from 2,000 stores located throughout the world. A single device can produce 2megabytes (MB) of data every 24hours. Each store location has one to five devices that send data.
You must store the device data in Azure Blob storage. Device data must be correlated based on a device identifier. Additional stores are expected to open in the future.
You need to implement a solution to receive the device data.
Solution: <b>Provision an Azure Event Grid. Configure the machine identifier as the partition key and enable capture.</b>
Does the solution meet the goal? YES

120. Your company has an Azure Kubernetes Service (AKS) cluster that you manage from an Azure AD-joined device. The cluster is located in a resource group.
     Developers have created an application named MyApp. MyApp was packaged into a container image.
     You need to deploy the YAML manifest file for the application.
     Solution: You install the Azure CLI on the device and run the kubectl apply `"f myapp.yaml command.
     Does this meet the goal? <b>Yes</b> - kubectl apply -f myapp.yaml applies a configuration change to a resource from a file or stdin.

121. ![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/questionAzureFunctionApp.png?raw=true)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/answerAzureFunctionApp.png?raw=true)
122. You are developing a solution for a hospital to support the following use cases:
     ✑ The most recent patient status details must be retrieved even if multiple users in different locations have updated the patient record.
     ✑ Patient health monitoring data retrieved must be the current version or the prior version.
     ✑ After a patient is discharged and all charges have been assessed, the patient billing record contains the final charges.
     You provision a Cosmos DB NoSQL database and set the default consistency level for the database account to Strong. You set the value for Indexing Mode to
     Consistent.
     You need to minimize latency and any impact to the availability of the solution. You must override the default consistency level at the query level to meet the required consistency guarantees for the scenarios.
     Which consistency levels should you implement? To answer, drag the appropriate consistency levels to the correct requirements. Each consistency level may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content.

     Return the most recent patient status: Strong
     Return health monitoring data that is no less than one version behind: Bounded Staleness
     After patient is discharged and all charges are assessed, retrieve the correct billing data with the final charges: Eventual
123. ![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/questionAnswerManagedIdentity.png?raw=true)
124. The AzScheduledQueryRuleSource is Heartbeat, not CPU!
125. You are developing an ASP.NET Core web application. You plan to deploy the application to Azure Web App for Containers.
     The application needs to store runtime diagnostic data that must be persisted across application restarts. You need to configure the application settings so that diagnostic data is stored as required.
     How should you configure the web app's settings?
     If <b>WEBSITES_ENABLE_APP_SERVICE_STORAGE</b> setting is unspecified or set to true, the <b>/home/</b> directory will be shared across scale instances, and files written will persist across restarts
126. You are creating an Azure key vault using PowerShell. Objects deleted from the key vault must be kept for a set period of 90 days.
     Which two of the following parameters must be used in conjunction to meet the requirement?
     EnablePurgeProtection and EnableSoftDelete
127. You are developing an application to transfer data between on-premises file servers and Azure Blob storage. The application stores keys, secrets, and certificates in Azure Key Vault and makes use of the Azure Key Vault APIs.
     You want to configure the application to allow recovery of an accidental deletion of the key vault or key vault objects for 90 days after deletion.
     What should you do?
     Run the az keyvault update --enable-soft-delete true --enable-purge-protection true CLI.
128. You are configuring a web app that delivers streaming video to users. The application makes use of continuous integration and deployment.
     You need to ensure that the application is highly available and that the users' streaming experience is constant. You also want to configure the application to store data in a geographic location that is nearest to the user.
     Solution: You include the use of an <b>Azure Content Delivery Network (CDN)</b> in your design.
129. You develop and deploy an Azure App Service API app to a Windows-hosted deployment slot named Development. You create additional deployment slots named Testing and Production. You enable auto swap on the Production deployment slot.
     You need to ensure that scripts run and resources are available before a swap operation occurs.
     Solution: <b>Enable auto swap for the Testing slot. Deploy the app to the Testing slot</b>
     Solution: <b>Disable auto swap. Update the app with a method named statuscheck to run the scripts. Re-enable auto swap and deploy the app to the Production slot.</b>
130. You develop a website. You plan to host the website in Azure. You expect the website to experience high traffic volumes after it is published.
     You must ensure that the website remains available and responsive while minimizing cost.
     You need to deploy the website.
     Deploy the website to an App Service that uses the Standard service tier. Configure the App Service plan to automatically scale when the CPU load is high.
131. You are authoring a set of nested Azure Resource Manager templates to deploy multiple Azure resources.
     The templates must be tested before deployment and must follow recommended practices.
     You need to validate and test the templates before deployment.
     Which tools should you use?
     Determine whether the templates follow recommended practices: Azure Resource Manager test toolkit
     Test and validate changes that templates will make to the environment: What-if operation
132. You develop Azure Web Apps for a commercial diving company. Regulations require that all divers fill out a health questionnaire every 15 days after each diving job starts.
You need to configure the Azure Web Apps so that the instance count scales up when divers are filling out the questionnaire and scales down after they are complete.
You need to configure autoscaling.
What are two possible auto scaling configurations to achieve this goal?
<b>fixed date profile</b> and <b>Predictive autoscaling</b>
133. You need to implement the bindings for the CheckUserContent function. How should you complete the code segment?
public static class CheckUserContent<br>
{ [FunctionName("CheckUserContent")]<br>
public static void Run(<b>BlobTrigger(userContent/{name}")]</b>) string content, <br>
[<b>Blob("userContent/{name}", FileAccess.Write)</b>]





















Questions also from https://www.examtopics.com/exams/microsoft/az-204/view/ and https://www.kaplanlearn.com/ and <b>[itexams.com](https://www.itexams.com/exam/AZ-204)</b> and https://www.examtopics.com/exams/microsoft/az-204/view/
