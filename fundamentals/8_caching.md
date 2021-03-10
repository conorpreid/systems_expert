# Caching

### Terms before beginning
- Cache
  - hardware or software that holds data, with the purpose of returning that data faser than otherwise
  - often used to store responses to network requests, or results of computationally expensive operations
  - this data can become stale if the SOT for that data gets updated and the cache does not
- Cache hit
  - when the requested data is found in a cache
- Cache miss
  - when the requested data could have been found in the cache but wasn't.
  - the result of bad design or system failure
  - ie: *if our server goes down, the load balancer will have to forward requests to a new server, which will result in cache misses*
- Cache Eviction Policy
  - the policy by which values get evicted or removed from a cache
  - could be LRU (least-recently used) or FIFO, or LFU (least-frequently used)
- Content Delivery Networks
  - CDN: third party service, that acts like a cache
  - often the users of your service are geographically far away from that service, and thus netowrk requests are slow
  - CDN providers have servers all over the world, so you give them your content and they serve the traffic more quickly (ie less latency) than you could have
  - often referred to as Points of Presense
  - examples are Cloudflare and Google Cloud CDN


### Getting into it
one of the main reasons to use this - prevent having to do expensive operations over and over \
this helps with latency \
if you already have the answer, you can serve it super quick \
you can cache is muitple places
- client level: doesnt have to go server
- server: maybe doesnt need to go database
- between server and database
- also happens at the hardware level

instances
- if you are doing loads of network requests, and you want to avoid that. client -> server -> database -> server -> client. if the client makes the same request again, maybe you use cache to answer that request.
- maybe the operation is computationally long (client to server, server performs some algo). you cache that answer on return to serve future requests.
- what about multiple servers? all hitting the database with the same requests? might overload the database, use caching to prevent those long reads.

examples
- questions list on algoexpert. its static content, so cache. its quicker (thats at the client level)
- running code on algoexpert, cache the results of the code they provide to make that quicker (that happens at the server level. client to server, server has oh I have that in cache maybe in server maybe separate)

imagine you cache social network posts at the server level, you now have two sources of truth? \
two types of cache
- write through: when you write, you write to both the cache and the source of truth. in this case, you need to get to the db (expensive)
- write back: when you write, only to cache. system asyncroniously writes back to the db periodically. downsides here, are that if you lose the cache then you lose the data

when systems get large, this gets tricky \
think of YT comments - you don't want some viewers reading out of date comments (stale cache) \
maybe good here to move cache out of server, migrate to other service (redis) \
other cases, we don't really care \
YT view count is an exmaple of this, not super big deal if one users see's a slightly out of date number \
cache is really good when data is non-mutable \
when its mutable, things get hard. 

rules of thumb
- defo use if using static or inmutable data
- harder when data is mutable (gets stale)
- consider if only having 1 single thing reading or writing data
- dont care about consistency (staleness) of data
- design the system to properly get rid of stale cache when needed

leads us to eviction policy \
somethimes will have stale data, how do we get rid of it \
few popular rules
- LRU policy (least recently used): get rid of the least recently used piece of data (assumption that the data that is least recently used is what we dont care about)
- LFU policy (least frequenly used)
- FIFO / FILO

all depends on the use case you are designing
