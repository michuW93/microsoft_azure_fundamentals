microsoft_azure_developer-AZ-204-

Tutorial based on James Millar videos

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
