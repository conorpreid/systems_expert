# Key Value Stores

### Terms before beginning
- Key value store
  - flexible noSQL database
  - often used for caching and dynamic config
  - Etcd / Redis/ZooKeeper etc
- Etcd
  - strongly consistent and highly available
  - often used to implment leader election in a system
- Redis
  - in-memory key value store (so no persistent)
  - typically used as a fast and best-effort caching solution
  - also used to implement rate limiting
- ZooKeeper
  - strongly consistent, highly available
  - often used to store important config or perform leader election
- Reminder: strongly consistent
  - immediatly consistent once your acid transaction commits
  - so imagine a replicated db, commit goes in, means that change exists everywhere
  - eventually consistent means the change might only take effect 1 place, and rollout to other locations eventually

### Getting into it
structure from relational db's can be useful \
other times its not - then you want a noSQL db \
most popular types of noSQL is key value store \
mappings from keys to values (some come with specfic typing) \
can think of these like hash tables too \
very felxible and simple \
no imposed structure, nothing more conceptual simple \
use when you have no use for strucutre \
caching - storing values (responses to network requests) and access them using some key (hash, username etc) \
so fits here very well \
dynamic config too (covers later) - sometimes you want certain consts in areas in your system \
key values are fast since you don't need to search the entire database \
these means lower latency and more throughput \
lots of diff types - behave differently \
some persist data, some don't (redis) \
some strong consistency, some eventual

interesting point
- if you implement in-memory caching in your server
  - then your server goes down
  - you lose the cache
- but, if you implement redis for example
  - then your server goes down
  - the cache is still there, to be used when the server comes back up

so you get some efficencies by seperating out the system
