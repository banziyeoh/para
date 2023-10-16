---
tags:
  - backend
  - cache
source:
  - https://stackoverflow.blog/2019/08/06/how-stack-overflow-caches-apps-for-a-multi-tenant-architecture/
type:
  - "[[TILT]]"
created: 2023-10-16T19:27:00
areas:
  - "[[API Development]]"
archived: false
---
# Cost of having a cache
- Purging values if and when needed (cache invalidation)
- Memory used by the cache
- Latency to access the cache (weight against access to the source)
- Additional time and mental overhead spent debugging something more complicated

# Questions to ask when considering to add cache layer
- Is it that much faster to hit cache?
- What are we saving?
- Is it worth the storage?
- Is it worth the clean-up of said storage (e.g. garbage collection)?
- Will it go on the large object heap immediately?
- How often do we have to invalidate it?
- How many hits per cache entry do we think we’ll get?
- Will it interact with other things that complicate invalidation?
- How many variants will there be?
- Do we have to allocate just to calculate the key?
- Is it a local or remote cache?
- Is it shared between users?
- Is it shared between sites?
- Does it rely on quantum entanglement or does debugging it just make you think that?
- What colour is the cache?

# Case study
[[How stack overflow caches apps for a multitenant architecture]]