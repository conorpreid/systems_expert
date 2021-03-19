# Hashing

### Terms before beginning
- Consistent Hashing
  - A type of hashing
  - minimises the number of keys that need to be remapped when a hash table is resized
  - often used by LB's to distribute traffic to servers
  - minimizes the number of requests that get forwarded to diff servers when new servers are added / removed
- Rendezvous hashing
  - otherwise known as highest random weight
  - allows for minimal redistribution of mappings when a sever goes down
- SHA
  - short for secure hash algorithms
  - collection of crytographic hash functions used in the industry

### Getting into it
simpliest form is diff from the above types \
hashing is an action to transform some piece of data into a fixed sized value / integer \
that data could be ip address / http request etc

core problem:
- you have multiple clients
- you have multiple servers
- you have caching at the server level
- you have a LB using round robin
- ...this means you'll miss a lot of cache hits
- ...because a client won't always be talking to the same server, where its requests are getting cached

this is where hashing comes into play \
you hash the name of the clients into an int \
then mod that int by the number of servers you have \
this gives you an *index* of what server that clients requests should *always* go to \
note that a good hashing function will give you uniformity - it'll evenly spread the load accross the available servers

what happens now when we add a new server \
we need to go back to our hashing function and mod by the new num servers \
this will give us completely diff results - ie clients now mapped to totally diff servers \
this causes us to miss cache hits \
so - hashing the name then modding doesnt work in this case (ie large systems design)

so - how to solve this \
this is where these complex hashing strategies come in \
consistent hashing (conceptually)
- hash servers, then place on a circle
- hash the clients, and superimpose them on the same circle
- then, for each client, go clockwise and give that clients traffic to the first server you find on that circle

why is this good? \
think of when a server dies \
then the clients that were using that server will move to a new server, but nothing else will have to \
same when we add a new server \
some clients will move, but not all \

what if you want to *even more* evenly distribute traffic \
you can pass servers through multiple hashing functions \
so each server can be placed in multiple places \
clients can get caught by diff servers then \
maybe one server is way more powerful than others \
you want that server to get more traffic \
pass that server through more hashing functions to get more locations \

what about rendezvous hashing? \
for each client, creates a ranking of the servers using some logic for \
when you remove a server, all the clients that mapped to the server will move to the second highest ranking server they were originally mapped to \
so again, only clients that have to move do move

note you basically never write your own hashing function \
