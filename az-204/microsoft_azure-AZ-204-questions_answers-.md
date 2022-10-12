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
`azureauth.properties` as the autorization file

15. Standard tier plan and above supports Kafka messages in Event Hub. The Basic tier does not.

16. `set AZCOPY_CONCURENCY_VALUE` on windows = `export AZCOPY_CONCURENCY_VALUE` on linux and MacOs. 
This environment variable can increase the throughput when transferring small files and specifies the number of concurrent requests that can occur.

17. Blob permission allow an anonymous user to read all the blobs in the container but not enumerate them.

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

27. In Azure Monitor you can see `CPU usage, network usage and disk operations per second`. To see boot diagnostic and application logs you need to enable it,
it's not enabled by default

28. Azure Cosmos DB accounts that are configured to use strong consistency cannot associate more than one Azure region with 
their Azure Cosmos DB account.

29. <b>You cannot implement user delegation SAS though the stored access policy feature</b>. Stored access policies are not supported for a user delegation SAS.
A user delegation SAS is only supported for the Blob service.

30. Durable timers are limited to seven days. The workaround is to simulate using the timer API in a loop, such as a while loop or a for loop

31. port 443 HTTPS, ports 5671-5672 for advanced message queuing protocol (AMQP), ports 9350-9354 for listeners on service bus relay over TCP

32. NewGUID(.NET) is deterministic API, GUIDs/UUIDs is not deterministic

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

40. you can form a partition key by concatenating multiple property values into a single artificial partitionKey. It's synthetic key then

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

44. Azure CDN from Akamai purge request is processing the fastest.

45. UseAzureAppConfiguration to allow the configuration setting registered for refresh to be updated while ASP.NET core web app 
continues to receive requests

46. The JWT validation policy pre-authorizes requests in API Management by validation the access tokens of each incoming request.

47. In the dynamic data masking configuration page you need to choose `schema, table, column`





Questions also from https://www.examtopics.com/exams/microsoft/az-204/view/ and https://www.kaplanlearn.com/
