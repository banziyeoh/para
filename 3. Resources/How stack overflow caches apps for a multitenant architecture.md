---
tags:
  - cache
  - case-study
source:
  - https://stackoverflow.blog/2019/08/06/how-stack-overflow-caches-apps-for-a-multi-tenant-architecture/
type:
  - "[[TILT]]"
created: 2023-10-16T19:27:00
areas:
  - "[[API Development]]"
archived: false
---
Stack Overflow and the Stack Exchange network of sites is [a multi-tenant architecture](https://nickcraver.com/blog/2016/02/17/stack-overflow-the-architecture-2016-edition/). Need to spit up the caching where needed, and purge it too.

- **“Global Cache”**: In-memory cache (global, per web server, and backed by Redis on miss)
- - Usually things like a user’s top bar counts, shared across the network
    - This hits local memory (shared keyspace), and then Redis (shared keyspace, using Redis database 0)
- **“Site Cache”**: In-memory cache (per site, per web server, and backed by Redis on miss)
- - Usually things like question lists or user lists that are per-site
    - This hits local memory (per-site keyspace, using prefixing), and then Redis (per-site keyspace, using Redis databases)
- **“Local Cache”**: In-memory cache (per site, per web server, backed by _nothing_)
- - Usually things that are cheap to fetch, but huge to stream and the Redis hop isn’t worth it
    - This hits local memory only (per-site keyspace, using prefixing)

# Why Redis?
It’s an open source key/value data store with many useful data structures, additional publish/subscriber mechanisms, and rock solid stability.

Stack overflow uses the pub/sub mechanism [for our websockets](https://nickcraver.com/blog/2016/02/17/stack-overflow-the-architecture-2016-edition/#websockets-httpsgithubcomstackexchangenetgain) that provide real-time updates on scores, rep, etc. Redis 5.0 [added Streams](https://redis.io/topics/streams-intro) which is a perfect fit for the WebSocket.

# Key takeaways

- Stack Overflow uses a shared cache to reduce the amount of data that needs to be stored in each tenant's cache. This shared cache is used to store data that is common to all tenants.

- The shared cache is implemented using Memcached, a high-performance distributed memory object caching system.

- Stack Overflow's multi-tenant architecture allows different tenants to have their own isolated instances of the application. This is achieved by using a separate database and isolated cache for each tenant.

- The tenant cache is a local cache that stores data specific to a particular tenant. It is used to reduce the load on the shared cache and to provide faster access to data for that tenant.

- Stack Overflow uses a combination of local and shared caching to balance the need for fast access to data with the constraints of the multi-tenant architecture.

- The caching strategy is designed to be flexible and can be easily adjusted based on the needs of the application and the specific requirements of each tenant.