microsoft_azure_developer-AZ-204-

Tutorial based on Sahil Malik videos

# Ways to secure Azure Storage

Securing Azure Storage:
* management plan - plan who can access storage account, who can manage storage acc, who can add users etc.
* data plane - keys (Azure generates it automatically), shared access signature, Azure Active Directory (is a system in Microsoft Azure that enables the identity management to configure accessibility of users and groups to services and resources, azure AD base on access token)
* encryption

Management plane: RBAC (role based access control).
<b>`Security principal`</b> can be:
* user, 
* group of users, 
* service principal, 
* managed identity(it's managed by Microsoft)

<b>Role definition</b> - it contains e.g roleName, roleType. There are sections `actions` and `dataActions` which tells what this role can do and `nonActions` and `notDataActions` which tells what role can't do.

<b>Scope</b> - set of resources which you want to apply certain access. Scopes can be: Management group, subscription, resource group, resource (Storage account is example of resource)

These three comes together as Role Assignment. Role assignment is attach role definition to a security principal on a scope. Example: Sahil (security principal) is attached "Storage account contributor" (role definition) to "storage account sahilstorage123" (scope)

Deny assignments can block access.

<b>Shared access signatures (SAS)</b> - secure, delegated access, without sharing the key. Control what the clients access, for how long etc.
There are three kind of SAS: User delegation SAS (using Azure AD), Service SAS(secured with storage acccount key), account SAS (secured with Storage account key)

Kinds of SAS:
* ad-hoc 
* Service SAS with Stored Access Policy - all rules packed into policy

Stored Access policy: Reused by multiple SAS, defined on resource container, permissions and validity period, Service Level SAS only

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/sas.png?raw=true)

On the left is Ad-hoc shared access signature while on the right is Service SAS with Stored Access Policy. So all these stuff like srt, se, spr etc. are now packed into `mypolicy`

# Authenticate using Azure Active Directory
The Microsoft Identity Platform  is and authentication service, open-source libraries, and applicaiton menagement tools.

Identity platform conist of: <br/>
Authentication Service - Azure Active Directory (allows single sign on), <br/>
Open-Source Libraries - MSAL, Microsoft.Identity.Web, Open ID connect (you can use it in no supported languages as Ruby) <br/>
Application Management tools - Gallery and non gallery apps (e.g Dropbox), single tenant and Multi Tenant apps, authorization, consent, logs

<b>Modern authentication</b>
WS-* and SAML, OAuth, OpenID Connect

OpenID Connect:
User ----> App ---->API -----> Downstream API

User is calling App with User identity but then App can call API with user identity or App identity and then App can call another API with again user or app identity 

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/openid_connect.png?raw=true)

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/token_openid_connect.png?raw=true)

OpenID Connect Tokens:
* Access token - enough info to allow API know who you are and what you can do
* ID Token - users identity
* refresh token


Authorization - what you can do?

Entities:
* App as service principle, app can authenticate, for app there is no id token
* user login to a browser or app

Authorization Azure Ad is helping:
* groups - can be used for both users and apps
* custom claims - info which you can put to access token e.g country to know if person can authorize
* app roles - defined on app level, can be assigned to user or app


# Microsoft Graph
Microsoft Graph is the gateway to data and intelligence in Microsoft 365, Windows 10 and Enterprise Mobility + Security. It can work with office 365, Excel, Windows 10, Calendar, Mail etc. it provides a unified programming model that you can use to access data in Microsoft 365, Windows 10 and Enterprise Mobility + security. By Microsoft Graph we can treat office 365 informations as data, query it and write to it! It can be used by REST APIs or SDKs. There is https://graph.microsoft.com where are some already created calls to endpoint like in Postman. You can get your profile info, all docs linked to your account etc.

# Azure Key Vault
is an Azure Service which allows you to securely store and access secrets

Types of Azure Key Vault Secrets:
* Keys - cryptographic keys used in other Azure services such as Azure Disk Encryption
* Secrets - any sensitive information including connection strings or passwords
* certifiactes - x509 certificates used in HTTPS/SSL/TLS communications (encryption in transit)

There are two pricing tiers for Azure Key vault: standard with software protected or Premium - all in standard + hardware security modules (HSM)

You can provison Azure Key Vault in Azure Portal or programatically in PoweShell (`New-AzKeyVault -VaultName`), AzureCLI, REST API or ARM templates

Configuring auth for Azure Key Vault:
* Use Azure AD app registration
* Use managed identity
* use key vault references

Key Vault References allow to move secrets to Key Vault without single line change in code. How to read a Key Vault Secret? `string secret = client.GetSecretAsync("secretmessage")Result.Value` <br/>
<b>Use Key Vault references to move app setting values to Azure Key Vault with no code changes.</b>

Using Key Vault References:
1. Move the configuration to Key Vault </br>
2. Deploy your App Service or Azure Function </br>
3. Create a system-assigned identity for your App </br>
4. Give GET KV SECRETS access to the app identity </br>
5. Update the configuration values with the KV reference syntax </br>
6. Verify your application functionality

2 syntaxes to use when updating app setting value:
`@Microsoft.KeyVault(VaultName=az204;SecretName=blobConnectionString;SecretVersion=fsj2nj3nj23n23323232)` or `@Microsoft.KeyVault(SecretUri=https://az204.vault.azure.net/secrets/blobConnectionString/fsj2nj3nj23n23323232)`

