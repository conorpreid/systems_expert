# Relational Databases

### Terms before beginning
- Relational Database
  - structured database
  - data is stored following a tabular format
  - suports querying through SQL
- Non-relational Database
  - free of imposed, tabular-like structure
  - NoSQL (not only SQL)
- SQL
  - Strucutured Query Language
- SQL Database
  - a database that supports SQL
  - often used to equal relational database
- NoSQL Database
  - database that is not SQL compatible
  - *this isn't true, NoSQL is also referred to as Not Only SQL*
- ACID transaction
  - a type of database transaction that has four important properties
    - atomicity:
      - the operations within the transaction either succeed or fail
    - consistency:
      - the transaction cannot bring the system into an invalid state.
      - after the transaction is commited or rolled back, the rules for each record will still apply
      - and future transactions will see the effect of the transaction
    - isolation:
      - the execution of multple transactions concurrently will have the same effect as if they had been executed sequentially
    - durability:
      - any commited transaction is written to non-volitile storage
      - it will not be undone by a crash, power loss, or network partition
- Database index
  - an auxilliary data structure that allows the db to perform certain queries much faster
  - you place an index on a column in your structured data, and reads are much quicker using that column
  - note that writes are more expensive, due to having to write the index too.
- Strong Consistency
  - refers to the consistency of ACID transactions
- Eventual Consistency
  - reads might return a view of the system that is stale
  - a datastore that is eventually consistent will give guarantees that the state of the db will eventually reflect writes within a time period
- Postgres
  - a relational database that uses a dialet of SQL called PostgreSQL
  - provides ACID transactions


### Getting into it
The structure that you impose on the data gives you a delineation between DB types \
Relational vs non-relational databases \
Interesting note
- You could write some Python (etc) to do complex operations on your data
- But to do so, you'd have to read it into memory. could be TB's of data
- SQL runs in the database itself, getting around this problem

A note on efficency
- At first glance, finding something in a table is O(n)
- where n is the number of rows
- thats kinda tough
- this is where indexes come into play

Indexs are very complex, high level here \
Just need to be aware of - there are tonnes of types \
Imagine *amounts* table \
Index is like a table of contents - it would store the amounts in order, making them easier to search through \
they then point to where the main data is stored \
things like "max" / "min" much quicker \
jump from linear time to log time makes a massive difference \
