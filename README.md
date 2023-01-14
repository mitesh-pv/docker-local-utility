# Localhost Utility Setup

This repo has basic steps and also docker-compose alternative to bring up common develpment utility softwares in localhost

## Kafka localhost setup

### Starting Kafka with Zookeeper
```shell
$ zookeeper-server-start.sh $KAFKA_HOME/config/zookeeper.properties
$ kafka-server-start.sh $KAFKA_HOME/config/server.properties
```
