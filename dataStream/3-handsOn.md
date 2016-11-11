---
title: DataStream API Connectors - Hands-On
layout: page
permalink: /dataStream/3-handsOn.html
---

In this hands-on session, you will learn how to use Flink's connectors to write and read streams from and to external storage systems. The session features of two tasks from which you can choose. The first task is to setup a local Kafka instance and to connect two streaming programs through a Kafka topic (one program writes to the topic and the other one reads from it). The second task is to setup a local Elasticsearch instance, write the output of a streaming program into an Elasticsearch index and finally to visualize this data with Kibana.

### Connecting streaming programs through Kafka

[Apache Kafka](http://kafka.apache.org) is a central component in many data stream infrastructures. Kafka is a distributed publish-subscribe system for data streams based on the concept of durable logs. A stream is called *topic* and can be populated by multiple producers and read by multiple consumers. Topics are persisted to harddisks and can be replayed.

#### Setup a local Apache Kafka instance

The following instructions show how to setup a local Kafka instance in a few steps.

* Download Apache Kafka 0.9.0.1 for Scala 2.10 [here](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.9.0.1/kafka_2.10-0.9.0.1.tgz).

* Extract the archive file and enter the extracted folder:

~~~bash
tar xvfz kafka_2.10-0.9.0.1.tgz 
cd kafka_2.10-0.9.0.1
~~~

* Start an Apache Zookeeper instance (Kafka uses ZooKeeper for distributed coordination) on `localhost:2181`:

~~~bash
./bin/zookeeper-server-start.sh config/zookeeper.properties &
~~~

* Start a Kafka instance on `localhost:9092`:

~~~bash
./bin/kafka-server-start.sh config/server.properties &
~~~

**Note:** Kafka persists topics (i.e., data streams) to `/tmp/kafka_logs` by default. Topics can be removed (or cleared) by shutting Kafka down and deleting this directory. You can stop Kafka and ZooKeeper by calling the `./bin/kafka-server-stop.sh` and `./bin/zookeeper-server-stop.sh` scripts (in that order!).

#### Write cleansed TaxiRides to a Kafka topic and read them back

Next, we modify your solutions for the previous two exercises and connect them through a Kafka topic.

1. The [TaxiRide Cleansing program]({{ site.baseurl }}/exercises/rideCleansing.html) shall write its result stream into a Kafka topic.
2. The [Popular Places program]( {{ site.baseurl }}/exercises/popularPlaces.html) shall read its input data (cleansed TaxiRides) from the Kafka topic.

The following [exercise instructions]({{ site.baseurl }}/exercises/toFromKafka.html) contain instructions and hints to adapt your programs.

