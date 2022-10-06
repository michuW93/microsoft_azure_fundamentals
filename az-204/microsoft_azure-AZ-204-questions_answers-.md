1. App is storing medical documents, if the stored intake forms are downloaded from storage by a third party, the contents of the forms must not be compromised. <br>
We can use Azure Key vault and public key encryption and store encrypted form in Azure Storage Blob storage

2. Configure Azure Disk Encryption for the VM: 
Keyvault -> Keyvault Key -> vm -> vm encryption -> all (all means encrypt both data and operating system)
`az keyvault create` then `az keyvault key create` then `az vm create` then `az vm encryption`

3. Requirements: all API calls must be authenticated and callers to the API must not send credentials. Answer: Managed Identity <br>
Basic and Client Certificate will send credential to the API.

4. You have an Azure user account that has access to two subscriptions. You need to retrieve a storage account key secret from Azure Key Vault. </br>
`Get-AzSubscription` because there is more than 1, then `Set-AzContext -SubscriptionId`, then `Get-AzStorageAccountKey`, then `Get-AzKeyVaultSecret -VaultName`

5. You must grant a VM access to specific resource groups in Azure Resource Manager. You need to obtain an Azure Resource Manager access token. Answer: We need to run `Invoke-RestMethod` cmdlet to make a request to the local managed identity for Azure resources endpoint.
