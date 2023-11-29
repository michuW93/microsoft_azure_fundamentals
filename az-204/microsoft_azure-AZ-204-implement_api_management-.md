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
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/az-204/images/APIGateway.png?raw=true)


API Management Pricing Tiers:
* consumption - you will pay for request, not for hour/day/month etc. You pay for what you use
* developer - just for testing, no SLA, supports both cache types
* basic - adds SLA
* standard - larger internal cache, adds azure AD integration
* premium - lareger cache, multi region deployments

API Management cache types:
* internal - cache provided within the API Management service
* external - redis compatible cache outside of API Management, such as Azure Cache for Redis

API Gateway Capabilities:
* accepts API calls and routes them to your backends
* verifies API keys, JWT tokens, certificates, and other credentials
* enforces usage quotas and rate limits e.g you can limit number of requests send to specific service
* caches backend responses

Azure Portal Capabilities:
* define or import API schema
* set up policies like quotas or transformations on the APIs
* package APIs into products
* manage users that have access to API

Developer portal capabilities:
* read API documentation
* create an account and subscribe to get API keys
* try out an API via the interactive console
* access analytics

There are <b>versions</b> and <b>revisions</b>.
<b>Versions</b> allow to present groups of related APIs to the developers. You can use versions to handle breaking changes in your API safely.
https://api-car.com/car/all/v1
https://api-car.com/car/all/v2

<b>Revisions</b> allow you to make changes to the APIs in a controlled and safe way, without disturbing your API consumers
https://api-car.com/car/all;rev=3

Each versions can have multiple revisions, just like a non-versioned API. You can use revisions without using versions, or the other way around <br>
Typically, versions are used to separate API versions with breaking changes, while revisions can be used for minor and non-breaking changes to an API

APIs are the foundation of the Azure API Management service

Products are how APIs are surfaced to developer, and have one or more APIs, title, description and terms of use. </br>
Groups are used to manage the visibility of products to developers

<b>Products Overview</b>
Products can be Open or Protected. Protected products must be subscribed to before they can be used. So you subscribe get token and then you can call API</br>
When a product is ready for use by developers, it can be published for developers to use it </br>
Subscription approval is configured at the product level. Developers need this subscription to access products

<b>Azure API Management Groups</b>
Administrators - manage API Management service instances creating the APIs, operations, and products </br>
Developers (can be created or invited to join by administrators or they can sign up from the Developer portal, each developer is a member of one or more groups) - are granted access to the developer portal and build applications that call the operations of an API. Each developer is a member of one or more groups </br>
Guests - unauthenticated developer portal users with certain read-only access, such as the ability to view APIs but not call them </br>
Custom groups - Administrators can also create custom groups or leverage external groups in associated Azure Active Directory tenants

<b>Policies</b> are a powerful capability of Azure API Management that allow changing the behavior of the API through configuration.
Policies are a collection of statements that are executed sequentially on the request or response of an API.

Examples of Azure API Management Policies:
* it can convert format of e.g response of API. Let's say response is in XML and we want JSON
* restrict the amount of incoming calls
* enforces existence and/or value of a HTTP Header
* caches response according to the specified cache control configuration

Access restriction policies:
* limit call rate by key - Prevents API usage by limiting call rate, on a per key basis
* validate JWT tokens - Enforces existence and validity of a JWT token in header or query parameter
* set usage quota by key - enforces a renewable or lifetime call volume and/or bandwidth quota
* check HTTP header presence - enforces existence and/or value of a HTTP header
* limit call rate by subscription - prevents API usage by limiting call rate, on a per subscription basis

Advanced policies:
* Mock response - returns a mocked response directly to the caller
* Forward request - forwards the request to the backend service
* retry - retries execution of a request at the specified time intervals
* set request method - allows changing the HTTP method for a request
* Trace - adds custom traces into the API inspector output or Application Insights

Transformation policies:
* convert XML to JSON and JSON to XML - converts request or response body from one extension to another
* Find and replace string in body
* set backend service - changes the backend service for an incoming request
* set query string parameter - adds/replaces/deletes request query string parameter

Caching policies:
* store to cache - caches response according to the specified cache control configuration
* get from cache - perform cache look up and return a valid cached response when available
* remove value from cache - remove and item in the cache by key

there are many more policies in Azure API management service

Policy Scopes:
* global scope - affects all APIs within the instance of API Management
* Product scope - manages access to the product as a single entity
* API scope - affects only a single API
* operation scope - affects only one operation within the API

When do policies execute?
* inbound policies execute when a request is received from a client
* backend policies execute before a request is forwarded to a managed API
* outbound policies execute before a response is sent to a client
* on-error execute when an exception is raised

Policies are defined in XML format and it supports inheritance

# Event base solutions

Event types:
* discrete: report state changes and are actionable (Event grid) e.g image was upload, account was created
* Series: report a condition, time-ordered, and analyzable (Event Hub) 
* user notification: prompt user or their device for attention (Notification Hub)

Azure Event Grid:
* event-based architectures (published/subscriber)
* publishers emit and subscribers consume
* supports many subscribers to one publisher
* filter events so if subscriber if not interested in sth then can ignore
* scalable up and down
* pay for what you use

`az provider register --namespace Microsoft.EventGrid`


Publisher/Subscriber concepts:
* event signifies something changed
* published has no expectation of what happens with event, he doesn't care was happens later
* subscriber determines what to do with even, he doesn't care what was before


<b>Azure Event Hub</b>:
* scalable event processing service
* great for big data scenarios with millions of events per second like IoT or Banking
* decouples sending and receiving data like in event grid consumer and sender don't know each other
* it can be easily integrated with Azure and Non-Azure services
* capture events to azure blob storage or data lake

Typical scenarios:
* telemetry e.g many sensors to predict earthquake
* transaction processing e.g banking
* anomaly detection for e.g transaction processing in bank

before creating event hub you need to create namespace `az eventhubs namespace create --resource-group`
then `az eventhubs eventhub create --name`

<b>Azure Notification Hubs</b>:
* send push notifications - app to user e.g phone buzzez to let you know that you got email or when someone link you on facebook

# Message-based Solutions

<b>Message-based Solutions</b> - it enables fault tolerance between modules. Even if service which consumes something go down, we still have all info in queue.
Once service will be back we can proceed all messages from queue

Azure Queue Storage: fully-managed service that is a part of the Azure Storage suite that enables you to create durable 
and configurable message queues to enable application modularity and fault tolerance.

How to interact with Azure Queue Storage:
* first you need an Azure Storage Account (general-purpose v2)
* queues are created within a single storage account
* it can support messages up to 64KiB in size
* messages exist withing a single queue
* number of messages limited only by size of the storage account
* it supports a configurable time to live per message (withing the default 7 days) - when something came to message queue and something pick it up then it's done,
however there can be a situation that noone pick this message from queue then it will be auto removed after time to live expire. You set it for second, month or even no expire

Queue URL structure: https://<b>storageaccount</b>.queue.core.windows.net/<b>queuename</b>  

Queue security
* data in queues is encrypted by default
* azure storage stored access policies can work with queues
* can interact with queue date via HTTP or HTTPS
* supports the following authorization approaches: Shared key, Shared access signature (SAS) or Azure AD

Visibility timeout - message are delivered to consumers but are not immediately deleted from the queue (Can happen that consumer pick up message from the queue but are working on this for some time and then error occurs - message stays in queue)
However, messages will not be visible in the queue again until a period of time has passed from the initial delivery.
This period of time is the visibility timeout, and it enables fault tolerance for your apps.

Scalability limits for Queues:
* a single queue cannot exceed 500TiB
* a single message cannot exceed 64 KiB
* a queue supports no more than 5 stored access policies
* a store account can support 20000 messages per second (1KiB message)
* a single queue can support 2000 messages per second (1 KiB message)

create a queue: `az storage queue create --name mysamplequeue` </br>
delete a queue: `az storage queue delete --name mysamplequeue` </br>
view messages in queue without affecting visibility `az storage message peek --queue-name mysamplequeue` </br>
delete all messaged in a queue: `az storage message clear --queue-name mysamplequeue` </br>

you can also play with queue via Azure Portal

<b>Azure Service Bus</b> is fully managed enterprise message broken service that enables multiple modes of messaging with integrations for common messaging systems including Java Message Service (JMS)

Azure service bus consist of Namespace in which there is a queue or topic. Queue is filled with producer and messages are taken by consumer while in topic there is publisher who publish sth into topic and then we can have many subscribers which can work on these data.

Azure service bus:
* supports both HTTP and HTTPS like Azure Queue Storage but also AMQP protocols
* includes messaging for both queues and topics
* supports advanced configurability: ordering, batching, DLQ and Duplicate detection

Azure service bus supports three different performance tiers:
* Basic tier - only supports queues and not topics. To fully utilize the functionality of this service, it is recommended to use the Standard or Premium tier 
* standard tier - pricing is pay as you go, utilizes shared resources, provides automatic scaling, support messages up to 256kb, does not support geo-disaster recovery or availability zones
* pricing is fixed based on messaging units, utilized dedicated resources, requires configuration of scaling rules, support messages up to 1 mb and supports geo-disaster recovery and availability zones

Azure service Bus supports message FIFO (first in, first out), it also supports Dead letter queue (DLQ) - this enables you to capture messages that were not processed during their lifetime and act accordingly with those messages.

Azure Queue Storage Use cases:
* total storage for queue needs to be over 80GB
* logs needed for all transactions executed against queue
* need to track progress of message processing

Azure Service Bus use cases:
* need support for receiving messages without polling so something else than just HTTP/HTTPS
* there is a need to guarantee message processing order (FIFO)
* there is a need to detect duplicate messages
* you need to support messages up to 256KB
* you may need to support topic based notifications (one to many)
* you need to support publishing and consuming in batches

to create a queue: `az servicebus queue create --namespace-name`

Azure service bus topics:
* enables a one-to-many relationship between messages and consumers
* a consumer creates a subscription to a topic
* subscriptions act as dedicated queues for a subscriber with configuration options
* topic filers can be specified as: boolean filters, SQL filters or correclation filters

to create a topic: `az servicebus topic create --namespace-name`

# Review
Do you need a solution to send events to mobile device as push notifications? Select <b>Azure Notification Hub</b> </br>
Does your solution product discrete events, that report state changes that a system can act on? Select <b>Azure Event Grid</b> </br>
Does your solution report state over time for analysis by another system, such as in a data pipeline? Select <b>Azure Event Hub</b>

Choose Azure Queue Storage when:
* total storage for queue needs to be over 80GB
* logs needed for all transactions executed against queue
* need to track progress of message processing
