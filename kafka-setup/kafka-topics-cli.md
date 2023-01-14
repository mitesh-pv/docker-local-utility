## Kafka topics CLI

### CLI commands to
1. Create a Kafka topic
2. List a Kafka topic
3. Describe a Kafka topic
4. Increase the partitions in a Kafka topic
5. Deletea Kafka topic


### List kafka topics 

```sh
kafka-topics.sh --bootstrap-server localhost:9092 --list
```

### Create kafka topics 

* Create topic with default 1 partition
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic first-topic
```

* Create topic with specific number of partitions
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic second-topic --partitions 3
```

* Default replication factor is 1, create a topic with specific replication factor
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic third-topic --partitions 3 --replication-factor 2
```

### Describe topic
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic second-topic
```

### Delete topics
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic first-topic
```




