## Kafka Console Consumer group CLI

* Create one consule producer and 3 console cosumers, send messages, it spreads out to all the three consumers

```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic

kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group
```

* Create one console producer and 2 console consumers, make the 2 cosole consumers read from different consumer groups. <br>
Sending messages in this scenario both the consumers reads the same messages as both consumers belong to differnt consumer group and the partitions are not distributed among them.

```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic

kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group consumer-group-1
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group consumer-group-2
```

1. List the existing consumer groups
2. Describe a consumer group
3. Delet a cosumer group

### List Consumer groups
```sh
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list
```

### Describe Consumer Group
```sh
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group my-first-consumer-group
```

