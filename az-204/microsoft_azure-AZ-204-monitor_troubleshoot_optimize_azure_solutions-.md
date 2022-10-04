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
