Kafka in Docker
===

This repository provides everything you need to run Kafka in Docker.

For convenience also contains a packaged proxy that can be used to get data from
a legacy Kafka 7 cluster into a dockerized Kafka 8.

Based on https://github.com/spotify/docker-kafka

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---

```bash
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` --env ADVERTISED_PORT=9092 mellonedain/kafka
```

```bash
export KAFKA=`docker-machine ip \`docker-machine active\``:9092
kafka-console-producer.sh --broker-list $KAFKA --topic test
```

```bash
export ZOOKEEPER=`docker-machine ip \`docker-machine active\``:2181
kafka-console-consumer.sh --zookeeper $ZOOKEEPER --topic test
```

Optional ENV variables
---

* ADVERTISED_HOST: the external ip for the container, e.g. `docker-machine ip \`docker-machine active\``
* ADVERTISED_PORT: the external port for Kafka, e.g. 9092
* ZK_CHROOT: the zookeeper chroot that's used by Kafka (without / prefix), e.g. "kafka"
* LOG_RETENTION_HOURS: the minimum age of a log file in hours to be eligible for deletion (default is 168, for 1 week)
* LOG_RETENTION_BYTES: configure the size at which segments are pruned from the log, (default is 1073741824, for 1GB)
* NUM_PARTITIONS: configure the default number of log partitions per topic
* AUTO_CREATE_TOPICS: adds auto.create.topics.enable=true to server.properties
* ALLOW_DELETE_TOPICS: adds delete.topic.enable=true to server.properties

Public Builds
---

https://registry.hub.docker.com/u/mellonedain/kafka/

Build from Source
---

    docker build -t mellonedain/kafka kafka/

Todo
---

* Not particularly optimized for startup time.
* Better docs

