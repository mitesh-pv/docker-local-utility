## Kafka Console Producer CLI

1. Producer without keys
<br> Key will be null.
<br> Data will be distributed across all partitions.

2. Produce with keys
<br> Always have same key.
<br> Data will go to the same partition.


### Producer without keys

* Sending data to kafka Topic
```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first-topic
```

* Sending data to kafka Topic with properties
```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first-topic --producer-property acks=all
```

* If we try to produce data to a topic that does not exist, then the kafka cli first creates the topic and then produces the data to the newly created topic. 

This new topic will have 1 partition with 1 replication factor by default
```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic new_topic

kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic new_topic
```

We can edit the `kafka/config/server.properties` file to set default partitions by changing the key `num.partitions=3`

### Produce with Keys
```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic --property parse.key=true --property key.separator=:
> name:mitesh
> example key:example value
> mitesh
org.apache.kafka.common.KafkaException: No key separator found on line number 3: 'mitesh'
	at kafka.tools.ConsoleProducer$LineMessageReader.parse(ConsoleProducer.scala:374)
	at kafka.tools.ConsoleProducer$LineMessageReader.readMessage(ConsoleProducer.scala:349)
	at kafka.tools.ConsoleProducer$.main(ConsoleProducer.scala:50)
	at kafka.tools.ConsoleProducer.main(ConsoleProducer.scala)
```







