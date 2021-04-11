# Publish/Subscribe Pattern

### Some terms before beginning
- Publish/Subscribe Pattern
	- often referred to as Pub/Sub
	- messages model that consists of publishers and subscribers
	- publishers publish messages to special topics (or channels) without caring about or knowing about who reads those messages 
	- subscribers subscribe to topics and read messages coming trough those topics
	- often comes with powerful guarantees like *at least once delivery*, *persistent storage*, *ordering of messages*, and *replayability* of messages
- Idempotent Operation
	- an operation that has the same ultimate outcome regardless of how many times it's performed
	- that is, if an operation can be performed over and over without changing the overall effect, its idempotent
	- operations performed through a Pub/Sub messageing system typically have to be idempotent
	- this is because Pub/Sub systems tend to allow the same message to be consumed multiple times
	- eg +1 to int in db is not idempotent
	- eg setting a value to *complete* is idempotent
- Apache Kafka
	- a distributed messaging system created by LinkedIn
	- very useful when using the streaming paradigm as opposed to polling
- Cloud Pub/Sub
	- hihg scalable Pub/Sub messaging service created by Google
	- guarantees at least once delivery of messages and supports *rewinding* in order to reprocess messages


### Getting into it
Pub/Sub uses streaming, not polling \
there must be a connection that is opened and maintained between Pub and Sub 

think about a stockbroker app \
if you have a network partition, you don't want those client to lose that data during the partition \
so you need some kind of persistent storage to solve for that \
maybe a db? maybe not what you want for any and all applications \
maybe the data is some kind of asyonchronus data - go off and do something and tell the client when its done \
dont want to have storage at the server level \
this is where Pub/Sub comes into play 

four entities involved here
- publisher
	- servers of the chat app etc
	- job is to publish data to topics
	- data pushed from servers to topics
	- dont comm with subscribers
- subscribers
	- clients that are listening for data
	- subscribe to topics
	- dont comm with publishers
- topic
	- kind of like channels of specific info
	- types of messages (probably like classes of data)
- message
	- data or operations that is relavent to subbers that they are listening for
	- this is a conceptual message, its a data block
	- execute a stock trade for example

note that pubbers and subbers don't know about each other \
topics are the intermediate layer to handle that \
topics are effectily like a db \
there is persistent storage at the topic layer \
in pub/sub, you are guaranteed *at least once delivery* \
each message that gets pushed into a topic will keep an index of what subscriber cares about that topic \
once the subscriber gets that message, it'll ACK the message \
then then messages know they have been consumed 

important to note here (with at least once delivery) \
sometimes messages are sent >1 times \
for example, message_1 gets sent to sub_1, but sub_1 loses connection to topic_1 before ACK \
once it gets connected again, message_1 will send again \
this can happen many times \
concept of idempotent operation important here \
this is an operation that has the same outcome, regardless of how often it is performed \
good example here is setting the status of something to "complete" \
increment a counter by 1, this is no idempotent \
important due to *at least once delivery* 

an advantage of pub/sub is that messages within a topic are ordered \
first in, first out \
this means you can replay messages within topics \
rewinding to previous snapshot in time for a topic can be very useful 

why multiple topics? \
you might be storing very diff types of data \
nice to have clear separation of duties and responsibilities 

also nice to add stuff on to pub/sub systems \
so two subs can listen to the same topic, and filter out certain messages depending on business logic \
again, clear spearation of duties 

remember that topics can be sharded 






 

