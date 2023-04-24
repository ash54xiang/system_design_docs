# Caching Overview

## Concepts
1. Take advantage of the locality reference principle: recently requested data is likely to be requested again.
2. Exist at all levels in architecture, but often found at the level nearest to the front end.
3. A cache is like short-term memory which has a limited amount of space. It is typically faster than the original data source.
4. Caching consists of:
    * precalculating results
    * pre-generating expensive indexes
    * storing copies

## Caches in different layers
* Client side
  * Use case: Accelerate retrieval of web content from websites (browser or device)
  * Tech: HTTP cache headers (cache-control in HTTP header), browsers
  * Solution: browser specific
* DNS
  * Use case: Domain to IP Resolution
  * Tech: DNS Servers
  * Solution: Amazon Route 53
* Web Server
  * Use case: Accelerate retrieval of web content from web/app servers. Manage Web Session (server-side)
  * Tech: HTTP Cache Headers, CDNs, Reverse Proxies, Web Accelerators, Key/Value Stores
  * Solution: Amazon CloudFront, ElastiCache for Redis, ElastiCache for memcached, Partner Solutions
* Application
  * Use case: Accelerate application performance and data access
  * Tech: Key/Value data stores, Local Caches
  * Solution: Redis, Memcached
  * Note:
    * Basically it keeps a cache directly on the Application Server. 
    * Each time a request is made to the service, the node will quickly return local, cached data if it exists. If not, the requesting node will query the data by going to network storage such as a database.
    * When the application server is expanded to many nodes, we may face the following issues:
      * the load balancer randomly distributes requests across the nodes
      * the same request can go to different noeds, increase cache misses
      * extra storage since the same data will be stored in two or more different nodes
      * Solution to the issues:
        1. Global caches
        2. Distributed caches
* Database
  * Use case: Reduce latency associated with database query requests
  * Tech: Database buffers, Key/Value data stores
  * Solution: the database usually includes some level of caching in a default configuration, optimized for a generic use case. Tweaking these settings for specific usage patterns can further boost performance, can also use Redis, Memcached
* Content Delivery Network (CDN)
  * Use case: Take the burden of serving static media off of your application servers and provide a geographic distribution
  * Solution: Amazon CloudFront, Akamai
  * Note:
    * If the system is not large enough for CDN, it can be built like this:
        1. Serving static media off a separate subdomain using a lightweight HTTP server (eg. Nginx, Apache)
        2. Cutover the DNS from this subdomain to a CDN layer
* Other Cache
  * CPU Cache
  * GPU Cache
  * Disk Cache

## Cache Invalidation
* If the data is modified in the database, it should be invalidated in the cache, if not, this can cause inconsistent application behavior. There are majorly three kinds of caching systems:
  * Write-through cache - where writes go through the cache and write is confirmed as success only if writes to DB and the cache BOTH succeed
    * Pro: Fast retrieval, complete data consistency, robust to system disruption
    * Con: Higher latency for write operation
  * Write-around cache - where write directly goes to the DB, bypassing the cache
    * Pro: This may reduce latency
    * Con: it increases cache misses because the cache system reads the information from DB in case of a cache miss. As a result, this can lead to higher read latency in the case of application s that write and re-read the information quickly. Read must happen from slower back-end storage and experience higher latency
  * Write-back cache - where the write is directly done to the caching layer and the write is confirmed as soon as the write to the cache completes. The cache then asynchronously syncs this write to the DB
    * Pro: This would lead to a really quick write latency and high write throughput for the write-intensive applications
    * Con: there is a risk of losing the data in case the caching layer dies because the only single copy of the written data is in the cache. We can improve this by having more than one replica acknowledging the write in the cache

## Cache Eviction Policies
1. First In First Out (FIFO)
2. Last In Last Out (LIFO)
3. Least Recently Used (LRU)
4. Most Recently Used (MRU)
5. Least Frequently Used (LFU)
6. Random Replacement (RR)

## Other
* Global caches
  * all the nodes use the same single cache space (a server or file store)
  * each of the application nodes queries the cache in the same way it would a local one
  * however, it is very easy to overwhelm a single global cache system as the number of clients and requests increase but is very effective in some architectures.
  * Two forms of hanlding cache miss:
    *  Cache server handles cache miss, which is used by most applications.
    *  Request nodes handle cache miss:
       *  have a large percentage of the hot data set in the cache
       *  an architecture where the files stored in the cache are static and should not be evicted
       *  the application logic understands the eviction strategy or hotspots better than the cache
*  Distributed caches
   *  The cache is divided up using a consistent hashing function and each of its nodes owns part of the cached data. If a requesting node is looking for a certain piece of data, it can quickly use the hashing function to locate the information within the distributed cache to determine if the data is available
   *  Pros: Cache space can be increased easily by adding more nodes to the request pool
   *  Cons: A missing node can lead to cache loss. We may get around this issue by storing multiple copies of the data on different nodes
*  Design a Cache System
   *  a single machine is going to handle 1M QPS
   *  Map and linkedList should be used as the data structures. We may get better performance on the double-pointer linked-list on the remove operation
   *  Master-Slave technique

## Caching Algorithm
1. Round Robin
2. Stick Round Robin
3. Weighted Round Robin
4. IP/URL Hash
5. Least Connections
6. Least Time