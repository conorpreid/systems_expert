# Replication and Sharding

### Terms before beginning
- Replication
  - duplicating the data from one database server to others
  - often used to increase redundancy in the system to tolerate regional failures
  - can also be used to move data closer to clients, helping latecny
- Sharding
  - Also called data partitioning
  - splitting a database into two or more pieces called shards
  - helps with throughput of the db
  - strategies include
    - sharding based on a clients region
    - sharding based on the type of data being stored (user, payments eg)
    - sharding based on the hash of a column (structured data only)
- Hot spot
  - describes the uneven spread of workload across servers
  - can happen when the sharding key or hashing function are suboptimal
  - or if the workload is naturally skewed
  - bascially, some servers get more traffic than others


### Gettting into it
db is often very critical \
performacne of system == performance of db \
must make sure db is performant \
this is where replication and sharding comes in \
replication - you have a standby database to switch to when the main one goes down \
writes happen to both \
replica always needs to be up to date for this to work \
writes have to happen in a syncronous way \
if write fails to replica - main write should not happen \
writes take longer thus \
replication can also help latency - think regional replication \
US users vs India users - diff db's \
writes happen to "local" db, needs to be replicated to the other one \
these cross db writes can be asyconronous \
they can happen every couple mins maybe - some systems this can be fine \
think pushing new deployments out across servers across the world - gradual rollout

maybe the db is getting overloaded \
you can vertical scale, but horizontal scaling is better \
you replicate to try and help throughput \
but - what if you have loads and loads of data? \
probably don't want to do that \
instead - split the data up \
store some in one server, some in another \
this is sharding (data partitioning) \
you avoid duplicating data this way \
how to split?
- shard the tables, rows in some shards others in other shards

note that hotspotting can happen here, depending on how you shard. \
maybe the workload is uneveningly distributed, due to poor sharding strategy \
use a hashing function to get uniformity \
consistent hashing useful here \
you might have replicas of each shard \
