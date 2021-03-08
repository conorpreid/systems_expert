# Network Protocols

### Terms before beginning
- Databases
  - programs that record data and query data
  - they are servers themselves
  - interact with an application through network calls, that use the protcols discussed earlier like TCP (or even HTTP)
  - some only keep data in memory, which means on failure / shutdown the data is lost
  - for the most part though, data is stored on disk which means its persistent (even when the server dies etc)
- Disk
  - either HDD or SSD
  - also known as non-volatile storage
  - use HDD for data that rarely accessed or updated, but storaed for a long time
  - use SSD for data thats frequently accessed and updated
- Memory
  - short for RAM
  - data will be lost when the process that has written that data dies
- Persistent Storage
  - any form of storage that persists if the process in charge of managing it dies


### Getting into it
A database is just a server \
Any computer can just become a database - possible, not always reccomended \
Not all databases persist through outages, data stored in memory wont stick around if the server crashes. An example of data stored in memory is an array that gets created in your server code (ie just a datastructure in your code). that data won't persist until you explicity tell it to.

Most of the complexity in the *storage* topic will be handled later in this course.
