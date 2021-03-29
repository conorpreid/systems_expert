# Leader Election

### Terms before beginning
- Leader Election
	- the process by which nodes in a cluster (servers in a bunch of servers) decide who the *leader* is
	- the leader is responsible for the primary operations of the service that the nodes (servers) support
	- when done correctl, guarantees that all nodes know who the leader is, and can elect a new one if the leader dies
- Consensus Algorithm
	- a type of algo used to have multiple entities agree on a single data value
	- eg who the "leader" is amoungs the group
	- examples are Paxos and Raft
- Paxos and Raft
	- consensus algos
	- allows for the synchronization of certain operations, even in a distributed setting
- Etcd
	- strongly consistent and highly available key-value store
	- often used to implement leader election in a system
- Zookeeper
	- strongly consistent and highly available key-value store
	- often used to store important confiduration or to perfrom leader election

### Getting into it
This is kinda an advanced topic \
all you really need here is a high level understanding \
imagine an example system
- like a product that you can subscribe to (netflix for example)
- you'd need a db, store info about user subs (are they currently subbed, renew date, price to renew etc)
- then use 3rd party service to handle the actual charging (paypal, stripe)
- 3rd party needs to talk to db 
- maybes that'd possible, maybe not. but db is very sensitive, don't want to expose to 3rd pary
- reasonable thing to do, put in a middle service to talk to the db (periodic) and pass on info to 3rd party service
- but what happens when that intermediary service fails? single point of failure for payments, terrible
- so, introduce redundency in that service, pretty typical
- a problem here is that we're making requests that we definitly dont want to duplicate (like "charge user")
- we want to ensure only one request gets made, so leader election
- servers election one of themselves as the leader, that server is responsible for the service

so leader election allows redundency, when you have a service that has requests that issue requests that can't be duplicated \
this isn't actually that simple \
for all the elect, and know who's the leader, and reelect, its tough \
the reason is that shared consensus (who the leader is) in a distributed system is very difficult \
what if there is a network failure (partition), machines can't communicate \
act of election is fine, consensus (agree on something) is difficult \
to achieve this, we use a consensus algo which are very complex (math heavy) \
allows this to happen, too complex to implement yourself \
3rd party service is used in relatity \
Zookeeper and Etcd are examples of tools, not primarily designed for leader election but can be 

Etcd
- key value store
- highly available
- strongly consistency (multi machines reading/writing at the same time, you will be returned the same value)
- not many that get both, this does so by implementing a consensus algo
- uses Raft
- multi machines that can read/write (to get availability so high), also make sure they have a SSOT for key/value store
- ensures nothing is duplicated
- to use this for leader election, store "who the leader is" in the key value store in Etcd
- Etcd gives you availability and consistency, and you know who the leader is and everyone sees the same leader







  


