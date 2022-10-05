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
