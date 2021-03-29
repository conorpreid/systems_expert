# Peer-to-Peer Networks

### Terms before beginning
- Peer-to-Peer Network
	- a collection of machines referred to as peers that divide a workload between themselves
	- aim is to complete that work more quickly than would otherwise be possible
	- often used in file-distribution systems
- Gossip protocol
	- when a set of machines talk to eachother in an uncoordinated manner in a cluster 
	- this spreads information through a system without requiring a central source of data


### Getting into it
kinda advanced topic \
lets look at a use case
- design system where you want to deploy or transfer large files to thousands of machines at a time
- ie, deploy 5GB files to 1000 machines from 1 machine, repeatadly (maybe ML models etc)
- 1000 machines request from 1 machine, all lives in a network throughout of 5GB per second (assume big tech company, thats a high throughput)
- simple math, when we want to tranasfer, network == 5GB per second, then transfer will take 1000 seconds (17mins)
- thats quite long for this type of operation. there is a bottle neck in our system
- well, maybe lets just have multiple machines to distribute the files. ie have 10 machines serving the files. 1000 machines request from those machines
- that makes things ten times faster. but, still 1.5mins (not bad, not great)
- but, 5GB files need to be replicated across all 10 machines. thats tough at scale (if we go more than 10 machines)
- sharding? shard the 5GB, have some of the 5GB live in one machine, others in another machine. 
- means we don't have to replicate, but just back to the first problem. each of the 1000 machines has to query each of the 10, there is bottle neck

this is where peer to peer networks comes in \
note: all these machines are actually "peers" in this context \
first, split the 5GB file into small pieces \
then send those peices across the network \ 
then, allow peers to communicate with one another to grab the missing pieces they need to create the file 

back to the example \
- 5GB into 1000 = 1000 5MB files \
now transfer those files to the 1000 machines, one file per machine \
this would take 1second (your just sending the file once) \
at the machine level, each machine needs to talk to the 999 other machines to grab the missing bit they dont have \
how long would that take? 0.999 seconds to get the rest of the file from every other machine \
note that "machines talking to each other" happens in parallel (two machines talking to each other, two others can too at the same time) \ 
note also that while the root machine is transfering the 5GB in shards (size 5MB), the machines that get their 5MB (before the process is done) can begin to share that 5MB \
so parallel transfers is why this is good \
probably useful here to assume that any machine can't transfer its files to multiple machines at the same time \
that is - that one machine cant service multiple other machines at the same time \
note also that peers have to know what other peers to talk to \
peer discovery and peer selection solve this 

maybe you have some central db that controls the peer to peer network \
this db decides what peers a peer should talk to next \
that central machine is known as a tracker \
or, maybe you use a gossip or epidemic protocol \
idea there is that peers recreates what happens in an office when people gossip \
they just kinda figure it out \
"oh you have a chunk I need, and by the way I just talked to another peer who has a chunk you need" \
exchange of information \
often they use a distributed hash table that holds what peers hold what pieces of data \
btw - when the original data gets chunked, each chunk gets a number so that peers can build the entire picture \
kraken is an example of this 

going back to our original problem - peer to peer speeds things up by roughly 600X \
so perfromance increase is significant 
 













