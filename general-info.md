Event Driven Architecture using Apache Kafka
------------------------------------------------------------------

Each cluster can have multiple brokers
Each broker will have multiple topics
Inside each topic, there are partitions. 

Broker is a server that manages kafka topics, facilitates writes to partitions and handles replication 
for fault tolerance and serves client requests (from both producers and consumers).

New event is stored in new cell / partition. Then replicated to other topics.

Topics store events. Topic is similar to message queue. Except when each event is consumed, it is not deleted from topic.
Producer publishes event. Stored in Kafka topic. Consumer microservices can read from topic. 
Since stored in multiple partitions, allows to scale as more consumers can read from its own partition in parallel.

Kafka provides us with consumer and producer APIs to assist in this.

1. How to create topics.
2. Consumer and Producer Microservices

EVENT-
1. Something has happened.
2. New event for login / new order is placed / any change in state of application
3. EventName should be in simple past tense. 
   4. <Noun><PerformedAction>Event
   5. Eg: ProductShippedEvent
   6. Eg: ProductDeletedEvent

Message vs Event: 
Message is an envelope, while event is content of the envelope.
Event can be String, JSON, Avro or null.  basically -> (Anything that can be serialized to array of bytes)
Event is bytes format evnetually.

default size of event payload is 1MB. (Which is plenty in most cases)
Larger the size of message, slower the system will perform. Event will contain all info required by consumer.
* Event should be as small as possible. For example, for image / video better to use a link rather than serializing the whole image.
* Message Key : String, JSON, Avro or null. i.e. Kafka message is keyValue pair. Both can be of different data types.
* Timestamp : to keep track of when event took place in history
* Headers : List of key value pairs for additional metadata. Eg Auth header. Might or not be used

### Ordering of messages using message key
