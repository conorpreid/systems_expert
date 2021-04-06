# Rate Limiting

### Some terms before beginning
- Rate Limiting
	- The act of limiting the num of requests send to or from a system (client?) 
	- most often used to limit the num of incoming requests in order to prevent DoS attacks
	- can be enforced at the IP address level, user-account level or region level
	- can also be implemented in tiers, eg 1 per second, 5 per 10 seconds, 10 per minute (granularities)
- DoS Attack
	- denial of service attack
	- when a malicious user tries to bring down or damage a system in order to render it unavailable to users
	- much of the time, it involves flooding it with traffic
	- some are easily preventable with rate limiting, others harder to defend against
- DDoS Attack
	- distributed DoS attack
	- happens when traffic is flooding the target system from many diff sources (XK machines), making it harder to defend against
- Redis
	- in memory key-value store
	- often used for best-effort caching
	- used to implment rate limiting  


### Getting into it
talking about security and performance here \
setting some thresholds, after which errors start happening \
without this - you can get taken down by DoS \
this is when a bad actor floods a system with requests, cloggs the system \
can be based on users (using header in the request eg) \
or IP addr, region, entire system \
not the ultimate way to protect the system \
DDoS is harder to prevent, more complex to handle (loads of machines that issue requests) \
how do you recognise the group of machines that are causing the DDoS \
note that (for example) rate limiting at the server level on user can be tough in a distributed system \
load balancer design is needed to ensure each server that is capabale of serving requests keeps the same state on each user \
for this reason, you handle your rate limiting in a separate server or database that all servers read from (instead of in memory in the server) \
redis helps here \
in memory key value store - is checked by servers when client issues a request 

rate limiting can be much more complex \
maybe not just on users \
not just "let them issue requests every 0.5seconds", but also "three times in 10seconds" and "ten times in 10minutes" \
so you have tiers - more complex to handle (operations on windows of time) 

