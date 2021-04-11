# MapReduce

### Some terms before beginning
- MapReduce
	- framework for processing very large datasets in a distributed setting
	- efficent, quick and fault tolerant
	- three main steps
		- Map: map function on the various chunks of the dataset, transforms into intermediate key-value pairs
		- Shuffle: reorganizes the intermediate key-value pairs such that pairs of the same key are routed to the same machine
		- Reduce: runs a reduce function on the newly shuffled key-value pairs and transforms them into more meaningful data
	- canonical example of a MapReduce use case is counting the number of occurrences of words in a large text file
	- you only need to worry about the Map and Reduce functions (and input and output)
	- everything else is abstracted away (like parallelization of tasks, fault tolerance etc)
- Distributed File System
	- an abstraction over a large cluster of machines that allows them to act like one large file system
	- most populalar are GFS (Google File System) and HDFS (Hadoop Distributed File System)
	- typically, DFS takes care of availability and replication
	- files are split into chunks of a certain size, and those chunks are sharded across a large cluster of machines
	- a central control plane is in charge of deciding where each chunk resides, routing reads to the right nodes and handling comms between machines
	- different DFS have different API's and semantics, but they achieve the same common goal
		- extremely large-scale persistent storage
- Hadoop
	- popular and open source framework that supports MApReduce jobs
	- also supports many other kinds of data-processing pipelines
	- central component is HDFS, on top of ehich other technologies have been developed


### Getting into it
complex topic, but for interviews you just need the basics \
developed in Google - very large datasets \
only so much vertical scaling you can do when you have loads of data \
so, process datasets that are stored across thousands of machines \
mapreduce lets you do this \
TB's of data across thousands of machines == easy to process \

data is stored across machines \
first, apply a map function to transform the data into key value pairs \
these are intermediate key:value pairs \
second, shuffle them to make them make sense depending on what you want to do \
then reduce them into some meaningful output or result 

important
- 1. assume you have a DFS, when you talk about MapReduce
	- DFS has some kind of central control plane that knows whats going on (where the data is, how to comm with storage, machines doing map and reduce etc)
- 2. we dont want to move the large dataset, becuase its very big. 
	- we let data live where it does, move the map functions to the data itself
- 3. key:value pairs are important
	- when reduce data that comes from the same dataset, you are looking for some kind of commonality across that data
	- intermediate step is very important then
	- you have some keys that are common (like PK's) that you want to aggregate across
- 4. trys to handle faults
	- in order to do this, it reperforms a map operation when it fails
	- this means map function is idempotent, has to be
	- reduce function too
- finally
	- main thing is the map reduce functions, and the input output
	- thats all you care about
	- you care about the detail of processing data in a distributed env

