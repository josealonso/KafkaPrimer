### Event-Driven Microservices Architecture

- Improves flexibility and maintainability.

- Allows high scalability.

- Improves service availability.

                                     ----------> Email Service        
                                     |
Order Service ------> Message Broker ----------> Stock Service
                ^       (Kafka)           ^
		|                         |
		|                         |
		|                         |
	An Order Event                An Order Event 
	is produced                   is consumed


### Kafka Cluster

Kafka is a distributed system.
A Kafka cluster consists of a set of brokers (3 as a minimum).

### Kafka Broker 

It is the Kafka server.
It exchanges messages between **producer** and **consumer**.

### Kafka Topic

It is like a table in a database.
A topic is identified by a name.
We can have any number of topics.

### Kafka Partitions

Kafka topics are divided into a number of partitions.
Every partition contains records in an unchangeable sequence.
A topic messages may be distributed among multiple computers.

### Offsets

Offset is a sequence of ids given to messages as they arrive at a partition.
The first message gets an offset of zero.

### Consumer Groups

A consumer group contains one or more consumers wordking together to 
process the messages.


### Start the Kafka environment


**Kafka with ZooKeeper**


- Start the ZooKeeper service

```
bin/zookeeper-server-start.sh config/zookeeper.properties
```


- Start the Kafka broker service

```
bin/kafka-server-start.sh config/server.properties
```

### Create the microservices

Producer and consumers projects:

```
curl -G https://start.spring.io/starter.zip -d dependencies=web,kafka -d type=maven-build -d groupId=info.josealonso.kafkademo -d artifactId="stock-service" -o stock-service.zip
```

Message Broker project:

```
curl -G https://start.spring.io/starter.zip -d dependencies=lombok -d type=maven-build -d groupId=info.josealonso.kafkademo -d artifactId="base-domains" -o base-domains.zip
```





















