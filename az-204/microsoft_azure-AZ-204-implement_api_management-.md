microsoft_azure_developer-AZ-204-

Tutorial based on Daniel Krzyczkowski videos

<b>Azure API Management</b> - Azure service to create consistent and modern API gateways for existing back-end services.
It provides secure, scalable API access for your applications.

Azure API Management Components:
* API gateway - accepts API calls and routes them to your backends
* Azure portal - the administrative interface where you set up your API program
* Developer portal - web user interface for developers where they can read API documentation

API gateway example:
Web App calling many Web API services. We can add proxy (API gateway between web app and web API services) so client will always call API Gateway which decide to which API service call should go.

API Gateway Capabilities:
* accepts API calls and routes them to your backends
* verifies API keys, JWT tokens, certificates, and other credentials
* enforces usage quotas and rate limits
* caches backend responses

Azure Portal Capabilities:
* define or import API schema
* set up policies like quotas or transformations on the APIs
* package APIs into products
* Manage users

Developer portal capabilities:
* read API documentation
* create an account and subscribe to get API keys
* try out an API via the interactive console
* access analytics

There are versions and revisions.
<b>Versions</b> allow to present groups of related APIs to the developers. You can use versions to handle breaking changes in your API safely.
https://api-car.com/car/all/v1
https://api-car.com/car/all/v2

<b>Revisions</b> allow you to make changes to the APIs in a controlled and safe way, without disturbing your API consumers
https://api-car.com/car/all;rev=3

Each versions can have multiple revisions, just like a non-versioned API. You can use revisions without using versions, or the other way around

Typically versions are used to separate API versions with breaking changes, while revisions can be used for minor and non-breaking changes to an API

APIs are the foundation of the Azure API Management service

Products are how APIs are surfaced to to developer, and have one or more APIs, title, description and terms of use. </br>
Groups are used to manage the visibility of products to developers

<b>Products Overview</b>
Products can be Open or Protected. Protected products must be subscribed to before they can be used. So you subscribe get token and then you can call API</br>
When a product is ready for use by developers, it can be published for developers to use it </br>
Subscription approval is configured at the product level. Developers need this subscription to access products

<b>Azure API Management Groups</b>
Administrators - manage API Management service instancesm creating the APIs, operations, and products </br>
Developers (can be created or invited to join by administrators or they can sign up from the Developer portal) - are granted access to the developer portal and build applications that call the operations of an API. Each developer is a member of one or more groups </br>
Guests - unauthenticated developer portal users with certain read-only access, such as the ability to view APIs but not call them </br>
Custom groups - Administrators can also create custom groups or leverage external groups in associated Azure Active Directory tenants
