microsoft_azure_developer-AZ-204-

Tutorial based on James Millar and Daniel Krzyczkowski videos

# Content Delivery Network
A content delivery network (CDN) is a distributed network of servers that can efficiently deliver web content to users. CDNs store cached content on edge servers in point-of-presence (POP) locations that are close to end users, to minimize latency. Benefit is low latency, reducing hosting bandwidth. It has protection from denial-of-service attacks

Application has two content types:
* static content - images, CSS files, JS files. Static content can be delivered via CDN
* dynamic content - changes on user interaction, dashboards, query results

Caching Rules:
* Azure CDN Standard Verizon
* Azure CDN Standard Akamai
* Azure CDN Microsoft - it's standard rules engine
* Azure CDN Premium Verizon - premium rules engine

Caching Rules types:
* Global - Only one per endpoint, overrides cache headers
* Custom - one or many rules, extension or path, override global rule
* query string - it's about parameters (key/value) in header. Ignoring query strings, bypass query strings, cache every unique URL (include Query String)

# Redis
Azure Cache for Redis provides an in-memory data store based on the Redis software. Redis improves the performance and scalability of an application that uses backend data stores heavily. It's able to process large volumes of application requests by keeping frequently accessed data in the server memory, which can be written to and read from quickly. Redis brings a critical low-latency and high-throughput data storage solution to modern applications.

Pricing tiers for Redis Azure Cache:
* basic - minimal feature set, no SLA, <b>not for PROD</b>
* standard - 2 replicated nodes, 99.9 availability, 53 GB of memory and 20k clients
* premium - redis cluster, low latency, 99.95% availability, 100GB memory + Enterprise (99.99% availability) and Enterprise Flash

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


# Azure Monitoring and Logging
