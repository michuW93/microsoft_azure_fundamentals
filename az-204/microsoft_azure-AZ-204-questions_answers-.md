1. App is storing medical documents, if the stored intake forms are downloaded from storage by a third party, 
the contents of the forms must not be compromised. <br>
We can use Azure Key vault and public key encryption and store encrypted form in Azure Storage Blob storage

2. Configure Azure Disk Encryption for the VM: 
Keyvault -> Keyvault Key -> VirtualMachine -> VM encryption -> all (all means encrypt both data and operating system)
`az keyvault create` then `az keyvault key create` then `az vm create` then `az vm encryption`

3. Requirements: all API calls must be authenticated and callers to the API must not send credentials. Answer: Managed Identity <br>
Basic and Client Certificate will send credential to the API.

4. You have an Azure user account that has access to two subscriptions. You need to retrieve a storage account key secret from Azure Key Vault. </br>
`Get-AzSubscription` because there is more than 1, then `Set-AzContext -SubscriptionId`, then `Get-AzStorageAccountKey`, then `Get-AzKeyVaultSecret -VaultName`

5. You must grant a VM access to specific resource groups in Azure Resource Manager. You need to obtain an Azure Resource Manager access token. 
Answer: We need to run `Invoke-RestMethod` cmdlet (Sends an HTTP or HTTPS request to a RESTful web service) to make a request to the local managed 
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
Manager template. You need to move VM1 to Host2. What should you do? When you redeploy a VM, it moves the VM to a new node within 
the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.

14. You want to deploy an ARM template using C#. The template deploys a single virtual machine in a new virtual network with single subnet. 
Which template files are necessary?
`createVMTemplate.json` as the template file (it must be .json because ARM template!), 
`parameters.json` as the parameters file(it also must be .json!), 
`azureauth.properties` as the authorization file

15. Standard tier plan and above supports Kafka messages in Event Hub. The Basic tier does not.

16. `set AZCOPY_CONCURENCY_VALUE` on windows = `export AZCOPY_CONCURENCY_VALUE` on linux and MacOs. 
This environment variable can increase the throughput when transferring small files and specifies the number of concurrent requests that can occur.

17. <b>Blob permission</b> allow an anonymous user to read all the blobs in the container but not enumerate them.

18. <b>Timespan can be used only if the function app is running on a dedicated app service plan</b>, not available for consumption and premium plan.

19. To set up exception reporting, you will need the following:
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
`TableBatchOperation op = new TableBatchOperation()` then `table.executeBatch(op)`

52. Create a new role reusing a default role definition. `Set-AzureRmRoleDefinition Input-File C:/SupportRole.json`

53. You want to avoid a single hot partition key. You can use a partition key with <b>pre-calculated</b> or random suffixes.
We don't want prefix, a suffix appends the value to the end, which makes it easier to read.

54. How to view the logged information in an easy manner? Open the <b>freb.xsl</b> file, failed request traces are stored in XML files named fr###.xml

55. Sharding pattern is used for splitting data across databases, disks, files, or partitions. It can prevent Azure Cosmos DB from being overloaded.
<b>Sharding pattern can resolve database issues for SQL and NoSQL but not MySQL</b>

56. to build cluster named NutexAKSCluster for the resourcegroup test: `az aks create --name NutexAKSCluster --resource-group test`

57. Purpose of `change feed` is to provide transaction logs of all the changes that occur to the blobs and the blob metadata in storage account. The change feed provides ordered, guaranteed, durabled read only logs of changes.

58. You have downloaded an Azure Resource Manager template to deploy numerous virtual machines. The template is based on a current virtual machine, but must be adapted to reference an administrative password.
You need to make sure that the password is not stored in plain text.
You are preparing to create the necessary components to achieve your goal.
Which of the following should you create to achieve your goal? Answer by dragging the correct option from the list to the answer area.
Select and Place: <b>an Azure Key Vault</b> and <b>an access policy</b>

59. You need to deploy the YAML manifest file for the application.
`kubectl apply -f myapp.yaml` applies a configuration change to a resource from a file or stdin.

60. Your company has a web app named WebApp1.
You use the WebJobs SDK to design a triggered App Service background task that automatically invokes a function in the code every time new data is received in a queue.
You are preparing to configure the service processes a queue data item.
Which of the following is the service you should use?
<b>WebJobs</b>

61. Your company has an Azure subscription.
You need to deploy a number of Azure virtual machines to the subscription by using Azure Resource Manager (ARM) templates. The virtual machines will be included in a single availability set.
You need to ensure that the ARM template allows for as many virtual machines as possible to remain accessible in the event of fabric failure or maintenance.
* Which of the following is the value that you should configure for the platformFaultDomainCount property?
Max value - The number of fault domains for managed availability sets varies by region - either two or three per region.

* Which of the following is the value that you should configure for the platformUpdateDomainCount property?
40 Each virtual machine in your availability set is assigned an update domain and a fault domain by the underlying Azure platform. For a given availability set, five non-user-configurable update domains are assigned by default (Resource Manager deployments can then be increased to provide up to 20 update domains) to indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.

62. You are creating an Azure Cosmos DB account that makes use of the SQL API. Data will be added to the account every day by a web application.
You need to ensure that an email notification is sent when information is received from IoT devices, and that compute cost is reduced.
You decide to deploy a function app.
Which of the following should you configure the function app to use? Answer by dragging the correct options from the list to the answer area.
Select and Place: Consumption pland and SendGrid binding

63. You company has an on-premises deployment of MongoDB, and an Azure Cosmos DB account that makes use of the MongoDB API.
You need to devise a strategy to migrate MongoDB to the Azure Cosmos DB account.
You include the Data Management Gateway tool in your migration strategy. <b>mongorestore</b>

64. You are developing an e-Commerce Web App.
You want to use Azure Key Vault to ensure that sign-ins to the e-Commerce Web App are secured by using Azure App Service authentication and Azure Active
Directory (AAD).
What should you do on the e-Commerce Web App?
Enable Managed Service Identity (MSI). - A managed identity from Azure Active Directory allows your app to easily access other AAD-protected resources such as Azure Key Vault.

65. Your Azure Active Directory Azure (Azure AD) tenant has an Azure subscription linked to it.
Your developer has created a mobile application that obtains Azure AD access tokens using the OAuth 2 implicit grant type.
The mobile application must be registered in Azure AD.
You require a redirect URI from the developer for registration purposes.
No change required











Questions also from https://www.examtopics.com/exams/microsoft/az-204/view/ and https://www.kaplanlearn.com/ and <b>itexams.com</b>
