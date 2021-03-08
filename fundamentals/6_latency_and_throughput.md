# Latency and Throughput

### Terms before beginning
- latency
  - the time take for a given operation to complete in a system
  - most often this is time duration (seconds etc)
  - some nice rule-of-thumb measures, see content itself
- throughput
  - the number of operations that a system can handle properly per unit time.
  - throughput of a server can often be measured in requests per second (RPS, QPS)

### Getting into it
these are the two most important measures of the performance of a system \
latency is how long it takes for data to get to one point in the system to another, ie client to server to client \
latency could also be reading data from memory or disk \
latency varies in a system by the operation. in a given system, some operations will have low latency and some will have high latency, its often a tradeoff and something to design your system for.
- eg video games. you need super low latency (to prevent lag). server might be located very far away from you, the network requests might just take ages to round trip
- maybe websites dont really care about page load time, but uptime might be more important.
- ...all depends on priorities

some orders to know
- 1MB from RAM: 0.25ms
- 1MB from SSD: 1ms (x4 on RAM)
- 1MB from HDD: 20ms (x20 on SSD)
- 1MB over 1Gbps network: 10ms
- intercontinental round trip for a packet: 150ms

*latency == delta(I ask, I get)*

throughput is how much work a machine can do in a period of time \
refferring to how much data can be transferred from one point to another in a system \
measured in GB per sec / KB per sec etc \
imagine numerous clients interacting with a server
- how many requests can the server hhandle in unit time
- thats throughput
- the server is like a bottleneck, you can only fit a certain amount of bytes through at a given time

how to improve throughput?
- you pay to increase throughput
- pay Google for example, to increase throughput
- doesn't always solve your problems though
- a better way to fix is to have *multiple servers* to handle requests

latency and throughput are related and good measures, but not nessesarily corrolated \
can have low latency (fast data transfers), low throughput might cancel this out. \
dont make assumptions about one based on the other \
