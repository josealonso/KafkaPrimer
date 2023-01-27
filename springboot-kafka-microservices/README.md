### Event-Driven Microservices Architecture

- Improves flexibility and maintainability.

- Allows high scalability.

- Improves service availability.

                                     ----------> Email Service ----> Consumer Group 2       
                                     |
Order Service ------> Message Broker ----------> Stock Service ----> Consumer Group 1
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

A consumer group contains one or more consumers working together to 
process the messages.


### Start the Kafka environment


**Run Kafka with ZooKeeper**


- Start the ZooKeeper service

```
bin/zookeeper-server-start.sh config/zookeeper.properties
```

- Start the Kafka broker service

```
bin/kafka-server-start.sh config/server.properties
```

**Run Kafka inside a Docker container**

TODO 


### Create the microservices

Producer and consumers projects:

```
curl -G https://start.spring.io/starter.zip -d dependencies=web,kafka -d type=maven-build -d groupId=info.josealonso.kafkademo -d artifactId="stock-service" -o stock-service.zip
```

Message Broker project:

```
curl -G https://start.spring.io/starter.zip -d dependencies=lombok -d type=maven-build -d groupId=info.josealonso.kafkademo -d artifactId="base-domains" -o base-domains.zip
```

### Test the application

1.- Run the **Kafka** message broker (explained above)

2.- Start the product service (**order-service**)

3.- Start the consumer services (**stock-service** and **email-service**)

4.- Make a POST request.

Using **HTTPie** instead of Postman:

```
htttp post localhost:8080/api/v1/orders name="book order" qty:=5 price:=10000
```

Response:

```
HTTP/1.1 200
Connection: keep-alive
Content-Length: 29
Content-Type: application/json
Date: Thu, 26 Jan 2023 23:59:31 GMT
Keep-Alive: timeout=60

Order placed successfully ...
```



















