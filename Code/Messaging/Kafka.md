# Kafka
Apache Kafka is a framework implementation of a software bus using stream-processing. It is an open-source software platform developed by the Apache Software Foundation written in Scala and Java. The project aims to provide a unified, high-throughput, low-latency platform for handling real-time data feeds. Kafka can connect to external systems (for data import/export) via Kafka Connect and provides Kafka Streams, a Java stream processing library. Kafka uses a binary TCP-based protocol that is optimized for efficiency and relies on a "message set" abstraction that naturally groups messages together to reduce the overhead of the network round trip. This "leads to larger network packets, larger sequential disk operations, contiguous memory blocks which allows Kafka to turn a bursty stream of random message writes into linear writes."

Kafka combines three key capabilities, so you can implement your use cases for event streaming end-to-end with
a single battle-tested solution:

To publish (write) and subscribe to (read) streams of events, including continuous import/export of your data from other systems.
To store streams of events durably and reliably for as long as you want.
To process streams of events as they occur or retrospectively.

Kafka provides all this functionality in a distributed, highly scalable, elastic, fault-tolerant, and secure manner.
Kafka can be deployed on bare-metal hardware, virtual machines, and containers, and on-premises as well as in the cloud.
You can choose between self-managing your Kafka environments and using fully managed services offered by a variety of vendors.

[Download links](https://kafka.apache.org/downloads)

*WARNING: Make sure to download the binary, and not the source.*


## Installing Kafka
Start by extracting Kafka to your C-drive, or wherever you please.

*Do note that in this repository commands will be documented for an installation on the 'c:\' path.*

In the kafka directory create 2 additional folders:
- kafka-logs
- zookeeper-data

In the config folder edit (and uncomment) these lines:
- In server.properties

        advertised.listeners=PLAINTEXT://localhost:9092
        ...
        log.dirs=C:/kafka/kafka-logs

- In zookeeper.properties

        dataDir=C:/kafka/zookeeper-data

*Make sure to change the kafka directory to whichever directory kafka was extracted.
It might contain some extra version information.*


## Running Kafka
Kafka comes with a map of batch scripts for windows within the map containing shell scripts for a Unix/Linux shell.
The commands shown in this repository will be those for a Windows system and normalized to the '~/kafka/bin/windows' folder.
For examples of commands in a shell terminal you can go [here](https://github.com/dilipsundarraj1/TeachApacheKafka/blob/master/Kafka_Commands.md).

Open a terminal and change directory to the Windows folder:

> cd kafka/bin/windows

### Start Zookeeper Server
In Powershell we run batch files starting with './', while if we use command prompt we don't.

- Powershell:
> ./zookeeper-server-start.bat ../../config/zookeeper.properties

- Command prompt:
> zookeeper-server-start.bat ../../config/zookeeper.properties

*We will be using Powershell, for more info on installing, using and configuring Powershell and Windows Terminal go
[here](https://github.com/H3AR7B3A7/WindowsTerminalAndPowershell).*

### Start Kafka Server / Broker
> ./kafka-server-start.bat ../../config/server.properties

*We can run multiple brokers by creating multiple server properties files containing different ports and log directories.*


## Architecture
### Kafka In Software Architecture
*A simple representation of Kafka in software architecture:*

![Producer - Kafka - Consumer](producer-kafka-consumer.png)

*A more detailed example of Kafka in software architecture (with multiple producers and consumers):*

![Producer - Kafka - Consumer - Details](producer-kafka-consumer-details.png)

### Topics
*A consumer group reading multiple partitions (at different offsets) from a topic:*
![Kafka Topic](kafka-topic.png)

### Consumer Group
The load on consumers will automatically re-balance when the number of consumers within the same consumer group changes.


## Kafka Through Console
### Create Topic
> ./kafka-topics --create --topic MyTopic -zookeeper localhost:2181 --replication-factor 1 --partitions 1

### Check Topics
> ./kafka-topics --describe --zookeeper localhost:2181

### Create a Console Producer
> ./kafka-console-producer --broker-list localhost:9092 --topic MyTopic

### Create a Console Consumer
> ./kafka-console-consumer --bootstrap-server localhost:9092 --topic MyTopic --from-beginning

### Alter a Topic
> ./kafka-topics --zookeeper localhost:2181 --alter --topic MyTopic --partitions 4

### Delete a Topic
> ./kafka-topics --zookeeper localhost:2181 --delete --topic MyTopic


## Kafka Core API
### Admin API
An API to manage and inspect topics, brokers, and other Kafka objects.

### Producer API
An API which allows us to publish (write) a stream of data to one or more of the named/categorized
Kafka topics in the cluster.

### Consumer API
An API to subscribe to (read) one or more topics and to process the stream of events produced to them.

### Streams API
An API to implement stream processing applications and microservices.
It provides higher-level functions to process event streams, including transformations,
stateful operations like aggregations and joins, windowing, processing based on event-time, and more.
It reads input from one or more topics in order to generate output to one or more topics,
effectively transforming the input streams to output streams.

### Connect API
An API to build and run reusable data import/export connectors that consume (read) or produce (write) streams of events
from and to external systems and applications, so they can integrate with Kafka.
For example, a connector to a relational database like PostgreSQL might capture every change to a set of tables.
However, in practice, you typically don't need to implement your own connectors because the Kafka community already
provides hundreds of ready-to-use connectors.

## Kafka Configurations
### Acks
- **acks=0**:
  - No response requested from broker to producer
  - Data will be lost if broker goes offline
  - Good for performance
- *acks=1*:
  - Default
  - Leader response requested, but replication not a guarantee
  - The producer will retry if ack not received
  - Data will be lost if leader goes down and replicas didn't replicate data
- *acks=all*:
  - Leader and replica response requested
  - No data loss, with enough replicas
  - Added latency
  - Must be used in conjunction with min.insync.replicas

### Producer Retries
- Default = 0
- In case of retries, by default order is not guaranteed
- The max.in.flight.requests.per.connection setting:
  - Default = 5
  - Set to 1 this will guarantee order
  - Kafka versions higher than 1.0.0 have a better solution

### IdemPotent Producer
- Set by producerProps.put("enable.idempotence", true)
- Prevents duplicate messages due to network errors
- Defaults:
  - retries = Integer.MAX_VALUE
  - max.in.flight.requests = 5 (in >= v1.1), 1 (in < v1.1)
  - acks = all
  
### Producer Compression
- Messages usually exist of JSON (text-based), applying compression is important
- The compression.type setting
  - none (default)
  - gzip
  - lz4
  - snappy
- Smaller requests
- Faster to transfer over network
- Better throughput
- Better disk utilization
- Compression is more effective the bigger the batch of message sent (more compression & throughput)
  - Tweak the settings linger.ms and batch.size to have bigger batches

### More
*For more examples visit these GitHub repositories:*
- [MichaelHeinecke](https://github.com/MichaelHeinecke/ApacheKafkaForBeginners)
- [dilipsundarraj1](https://github.com/dilipsundarraj1/TeachApacheKafka)

## Kafka & Docker

### Bitnami
```console
docker run --name zookeeper -e ALLOW_ANONYMOUS_LOGIN=yes -p 2181:2181 -d bitnami/zookeeper:latest
```

```console
docker run --name kafka1 -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181 -e ALLOW_PLAINTEXT_LISTENER=yes -p :9092 -d bitnami/kafka:latest
```

### Wurstmeister
docker-compose.yml:
```yaml
version: '1'  
  
services:   
  zookeeper:  
    image: wurstmeister/zookeeper:latest  
    container_name: zookeeper  
    ports:  
      - "2181:2181"  
 kafka:  
    image: wurstmeister/kafka:latest  
    container_name: kafka  
    ports:  
      - "9092:9092"  
 environment:  
      KAFKA_ADVERTISED_HOST_NAME: localhost  
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
```

Run docker-compose:
> docker-compose -f docker-compose.yml up

Create a topic:
> kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 100 --topic myTopic

---
#Kafka