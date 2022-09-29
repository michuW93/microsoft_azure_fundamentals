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
