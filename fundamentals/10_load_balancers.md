# Load Balancers

### Terms before beginning
- Load balancer
  - a type of reverse proxy that distributes traffic across servers
  - "reverse proxy" because it sits inbetween the client and the server
  - ....and acts on behalf of the server
  - can be found in many parts of the system, from DNS layer to DB's
- Server selection strategy
  - how a laod balancer chooses servers when distributing traffic
  - could be round-robin, random selection, performance-based (exsisting traffic or latency) and IP based
- Hot spot
  - when some servers receive a lot more traffic than others
  - this is caused by sub-optimal sharding (sharding key) or hashing (function)
  - or if workload is naturally skewed
- nginx
  - populate open source webserver that's often used as a reverse proxy and LB

### Getting into it
LB will be in pretty much all applications of sys design \
note that servers have limited throughout, can handle a limited num of requests \
so if you have lots of clients, you'll likley overload the server \
you *can* vertically scale the system, by increasing power of the single server \
thats limited though, cant go on forever \
so horizontally scale by adding more servers \
have 4 servers, handle client load more evenly and handle 4x load \
but you need a way to ensure clients issue requests in a balanced way amoung those servers \
this is what a load balancer does - balances load amoung services \
clients go to the load balancer, then on from there to servers \
these means we have a better throughout, naturally have better latency \
also make better use of your servers and resources \
there are diff types of LB's - software and hardware \
hardware - actual machines. limited to the hardware you have \
you can do more with software based LB's \
we'll focus on software LB's \
you register servers to LB's \
methods
- redirection: redirects traffic to servers randomly.
- round robin
  - dns round robin
  - goes through all servers and then back to the start
  - first request to first server, second to second, and back and again
  - evenly distributes traffic
- weighted round robin
  - place weights on servers
  - redirct more requests to a particular server (when its that servers turn)
- performance
  - or laod
  - performs health checks on servers (latency, how much resources they are using)
  - redirect traffic based on that
  - say, skip a server that is not handling requests well
- IP based
  - hash ip of client, and redirect accoringly
  - so this kind of matches clients to servers
  - helpful when you are caching at the server level
  - keep directing traffic from a client to where the cache might be
  - if that traffic went to a diff server, you can't utilise the caching
- path-based
  - redirect all traffic for a specfic portion of your service to a particular server
  - ie: all traffic that has to do with running code on algoexpert
  - that goes to a specfic server or set of servers
  - payments somewhere eles etc
  - good for deploying big changes, they thus only effect certain servers, not all
  - isolates issues

Pick one of these according to the usescase \
might be useful to have multiple LB's using a diff strategy \
maybe you would have
- 1 LB using path based LB-ing
- which directs traffic to one of a set of other LB's
- themselves using round robin

so you can design this according to whatever you want \
can also have multiple LB's at the same point in the system \
use a LB to prevent another LB getting overloaded with requests 
