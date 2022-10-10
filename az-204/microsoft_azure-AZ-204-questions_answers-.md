1. App is storing medical documents, if the stored intake forms are downloaded from storage by a third party, the contents of the forms must not be compromised. <br>
We can use Azure Key vault and public key encryption and store encrypted form in Azure Storage Blob storage

2. Configure Azure Disk Encryption for the VM: 
Keyvault -> Keyvault Key -> vm -> vm encryption -> all (all means encrypt both data and operating system)
`az keyvault create` then `az keyvault key create` then `az vm create` then `az vm encryption`

3. Requirements: all API calls must be authenticated and callers to the API must not send credentials. Answer: Managed Identity <br>
Basic and Client Certificate will send credential to the API.

4. You have an Azure user account that has access to two subscriptions. You need to retrieve a storage account key secret from Azure Key Vault. </br>
`Get-AzSubscription` because there is more than 1, then `Set-AzContext -SubscriptionId`, then `Get-AzStorageAccountKey`, then `Get-AzKeyVaultSecret -VaultName`

5. You must grant a VM access to specific resource groups in Azure Resource Manager. You need to obtain an Azure Resource Manager access token. Answer: We need to run `Invoke-RestMethod` cmdlet (Sends an HTTP or HTTPS request to a RESTful web service) to make a request to the local managed identity for Azure resources endpoint.

6. Azure AD users must be able to login to the website. auth2Permissions can only accept collections value like an array, not boolean. <b>oauth2AllowImplicitFlow accepts boolean value</b>. `oauth2AllowImplicitFlow : true`

7. `Start-AzureStorageBlobCopy` to copy blobs between containers.

8. To purge specific file then `single path purge` should be use.

9. Use API Management to access the services, use OpenID Connect for authentication and prevent anonymous usage. Answer: <b>validate-jwt</b> policy in API Management to validate OAuth token presented in each incoming API request. Valid requests can be passed to the API. 

10. Inbound - here we need to detect the user identity in the user request and then store the data in the cache. So, we need to look at the incoming request for this e.g Cache-lookup-value and cache-store-value. Outbound - here we need to update the response body so it should go in the output section e.g find and replace policy.

11. You need to develop code to access a secret stored in Azure Key Vault: `Environment.GetEnvironmentVariable("KEY_VAULT_URI")`, then `new <b>SecretClient</b>(new Uri(kvUri), new <b>DefaultAzureCredential()</b>)` 

12. cache-store in `<outbound>`

13. You have two Hyper-V hosts named Host1 and Host2. Host1 has an Azure virtual machine named VM1 that was deployed by using a custom Azure Resource
    Manager template. You need to move VM1 to Host2. What should you do? When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.

14. You want to deploy an ARM template using C#. The template deploys a single virtual machine in a new virtual network with single subnet. Which template files are necessary?
`createVMTemplate.json` as the template file (it must be .json because ARM template!), `parameters.json` as the parameters file(it also must be .json!), `azureauth.properties` as the autorization file






Questions also from https://www.examtopics.com/exams/microsoft/az-204/view/
https://www.kaplanlearn.com/