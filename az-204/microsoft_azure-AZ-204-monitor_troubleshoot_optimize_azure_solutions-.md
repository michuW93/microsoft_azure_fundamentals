microsoft_azure_developer-AZ-204-

Tutorial based on James Millar and Daniel Krzyczkowski videos

# Content Delivery Network
A content delivery network (CDN) is a distributed network of servers that can efficiently deliver web content to users. CDNs store cached content on edge servers in point-of-presence (POP) locations that are close to end users, to minimize latency. Benefit is low latency, reducing hosting bandwidth. It has protection from denial-of-service attacks

Application has two content types:
* static content - images, CSS files, JS files. Static content can be delivered via CDN
* dynamic content - changes on user interaction, dashboards, query results

Caching Rules:
* Azure CDN Standard Verizon
* Azure CDN Standard Akamai (purge for this works the fastest)
* Azure CDN Microsoft - it's standard rules engine
* Azure CDN Premium Verizon - premium rules engine

Caching Rules types:
* Global - Only one per endpoint, overrides cache headers
* Custom - one or many rules, extension or path, override global rule
* query string - it's about parameters (key/value) in header. Ignoring query strings, bypass query strings, cache every unique URL (include Query String)

# Redis
Azure Cache for Redis provides an in-memory data store based on the Redis software. Redis improves the performance and scalability of an application that uses backend data stores heavily. It's able to process large volumes of application requests by keeping frequently accessed data in the server memory, which can be written to and read from quickly. Redis brings a critical low-latency and high-throughput data storage solution to modern applications.

Pricing tiers for Redis Azure Cache (considerations: cache size, network performance, number of client connections):
* basic - minimal feature set, no SLA, <b>not for PROD, only for testing</b>, no replication
* standard - 2 replicated nodes, 99.9 availability, 53 GB of memory and 20k clients, supports failover
* premium - redis cluster, low latency, 99.95% availability, 100GB memory
* Enterprise (99.99% availability) 
* Enterprise Flash - 1.5 TB in cache

you can scale up e.g from basic to standard but you can't scale down - if you have standard you can't switch to basic

When should we cache?
* repeatedly accessed data
* data source performance
* data contention
* physical location to reduce network latency. When we cache in region East US and database is in Europe then caching helps a lot

Managing lifetime in redis cache
* no default expiration
* content exists until it's removed (typically there should be expiration time set)
* must set TTL (time to live) manually

object from redis cache can be deleted via scheduled deletion (TTL), Manual Deletion or Eviction which we are not controlling but we can controll policy of Eviction

Eviction Policy Options:
* volatile-lru (default)
* allkeys-lru - not only volatile keys
* noeviction
* volatile-random
* allkeys-random
* volatile-ttl - remove base on TTL rather than when they were last used

Calculating cache duration:
* rate of change - long expiry for static data e.g list of countries, short expiry for volatile data e.g concurency values
* risk of outdated data - lower ttl to match data change

Setting expiration times for redis cache: `_cache.StringSet("myKey", "myValue", new TimeSpan(3,0,0))` - it set for 3 hours

Best practices:
* watch out for data loss
* set expiry times to manage content lifetime
* add jitter to spread database load
* avoid caching large object - better split them into small
* host redis in the same region as your applications
* reuse client connections whenever possible


Cache patterns:
<b>cache aside pattern</b>
Application <-------> Data Strore(eg. SQL db) <-------> physical disk 

we can add Redis Cache

Redis Cache <-------> Application <-------> Data Strore(eg. SQL db) <-------> physical disk 

1. Does the data exist in the cache?
2. If not, retrieve from the data store
3. Store a copy in the cache

<b>Content cache pattern</b> Cache static content (images, templates, style sheets), reduces server load

<b>user session caching pattern</b> - maintain application state e.g shopping cart, usually it can be done via session cookies or local storage but Redis cache is better because it's faster 

Estimating cache size:
* number of concurent cached objects
* size of cached objects
* number of cache requests
* cache expiration policy

There is a benchmark which can help `Redis-benchmark -q -n 10000` so more or less you can know how it will work however it can't run from the Azure portal but in RedisCLI

Data Encryption in Azure Redis Cache
* encryption in transit - use TLS1.2 so communication between redis and app is encrypted, HTTP connections are disabled by default
* encryption at rest - in memory data is not encrypted but in Premium Tiers data persistence is encrypted

Encryption can be disabled via the Azure Portal or API but dont do it

# Azure Monitoring and Logging
there are two types of Azure Monitor:
* metrics - are numerical values that describe some aspect of a system at a particular time. Example of metrics can be CPU or memory usage value.
* logs - logs are events that occured within the system. Example: exception thrown during application execution

configuring web server logging to the filesystem `az webapp log config --name` </br>
tail logs from web service app `az webapp log tail --name`

Azure monitor capabilities:
* correlate infrastructures issues e.g not enough memory
* detect and diagnose issues across applications and dependencies
* support operations with smart alerts and automated actions e.g when there is a problem we can get email notification about it
* create visualizations with Azure dashboards and workbooks

What date does azure monitor collect
* data about the performance and functionality of the application's source code
* data about operating system
* data about the operation of an Azure resources e.g performance of Azure web app
* data about the operation of tenant-level azure services, such as Azure Active Directory

Azure Monitor can collect log data from any REST client what allows to create custom monitoring scenarios, including on-premises solutions

<b>Azure application insight</b> is an extensible application performance management (APM) service for developers and DevOPs professionals. It's part of Azure Monitor

Application Insights Capabilities:
* check performance of server machines like CPU or memory usage
* detect thrown exceptions in the applications source code
* add custom events and metrics in the client or server code to track business events
* collect request rates, response times, failure rates
* collect page views and load performance reported by client web browser

How can I see collected telemetry from my apps? 
* Smart detection - automatically warns you of potential performance problems and failure anomalies in your web applications
* application map - helps spot performance bottlenecks or failure hotspots across all components of the distributed application
* live metrics tab provides real time information about application performance
* failures tab provides details about issues detected inside your applications like exceptions and server errors

# Alerts and Handle Transient faults
With Azure Application Insights you can set up recurring tests to monitor availability and responsiveness of your web apps and web services

Types of availability tests:
* URL ping test - a single URL test that you can create in the Azure portal to test single endpoint
* Custom Track Availability Tests - send information about availability of an application using TrackAvailability() method from SDK
* Multi-step web test - a recording of a sequence of web requests which can be played back to test more complex scenarios

Azure Applicaiton Insights can alert if your app isn't responding or if it responds too slowly during availability tests

<b>An action group</b> - collection of notification preferences defined by the owner of and Azure subscription. 
Azure Monitor and Service Health alerts use action groups to notify users that an alert has been triggered

Each action is made up of the following properties:
* type: notification or action performed
* name: unique identifier of the group
* action: additional action like Webhook

Once there is a failure, new alert is sent to the target group

<b>Transient faults</b> include the momentary loss of network connectivity to components and services, the temporary unavailability of a service, 
or timeouts that arise when a service is busy. Transient fault is likely self-correcting 

Transient fault challenges:
* The app must be able to detect faults when they occur and determine if these faults are likely to be transient
* the application must be able to retry the operation if it determines that the fault is likely to be transient
* the app must use an appropriate strategy for the retries. This strategy specifies the number of times it should retry

There is `Polly` open source library which has implemented retry pattern, timeout pattern and circuit breaker

Circuit breaker policy:
* service is unavailable and can't respond to a request
* avoid sending request for some time
* when the circuit is opened, no request is sent until it is closed again

Common use:
Assume that an application connects to a database 100 times per second and the database fails. The application designer does not want to have the same error reoccur constantly. They also want to handle the error quickly and gracefully without waiting for TCP connection timeout.
Generally Circuit Breaker can be used to check the availability of an external service. An external service can be a database server or a web service used by the application.
Circuit breaker detects failures and prevents the application from trying to perform the action that is doomed to fail (until it's safe to retry).

The Circuit Breaker design pattern is used to stop the request and response process if a service is not working, as the name suggests.

The circuit breaker’s basic concept is to wrap a protected function call in a circuit breaker object that monitors for failures. When the number of failures reaches a certain threshold, the circuit breaker trips, and all requests to the circuit breaker return with an error.

So how is it going to connect back?
🌟 In the background, it sends a ping request or a default request to service A in a timely manner. So, when the response time comes back to the normal threshold it will turn on the request again.

Docker environment variables for app service:
* WEBSITE_CONTAINER_START_TIME_LIMIT - this will set the amount of time the platform will wait before it restarts your container
* WEBSITES_ENABLE_APP_SERVICE_STORAGE - if this value is not set or if it is set to true the /home directory will be shared across container instances
and files will persist
* WEBSITE_WEBDEPLOY_USE_SCM - if you want to deploy your container-based web application using WebDeploy/MSDeploy, this value must be set to false

# Preparation
Azure Cache for Redis is a fully managed, <b>in-memory cache</b> that enables high-performance and scalable architectures. Use it to create cloud or hybrid deployments
that handle millions of requests per second at sub-millisecond latency

