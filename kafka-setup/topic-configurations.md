## Topic Configurations

* Creaet a topic 
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic topic-configuration --replication-factor 1 --partitions 3
```

* Describe the topic to see config
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic topic-configuration
```

* Describe a config for a topic
```sh
kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name topic-configuration --describe
```

* Add some configurations and descrie config
```sh
kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name topic-configuration --alter --add-config min.insync.replicas=2
```
```
$ kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name topic-configuration --describe
Dynamic configs for topic topic-configuration are:
  min.insync.replicas=2 sensitive=false synonyms={DYNAMIC_TOPIC_CONFIG:min.insync.replicas=2, DEFAULT_CONFIG:min.insync.replicas=1}

$ kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic topic-configuration
Topic: topic-configuration	TopicId: 4jHBsWF0QoKzipS7K7f_Pg	PartitionCount: 3	ReplicationFactor: 1	Configs: min.insync.replicas=2,segment.bytes=1073741824
	Topic: topic-configuration	Partition: 0	Leader: 0	Replicas: 0	Isr: 0
	Topic: topic-configuration	Partition: 1	Leader: 0	Replicas: 0	Isr: 0
	Topic: topic-configuration	Partition: 2	Leader: 0	Replicas: 0	Isr: 0
```

* Delete configurations
```sh
kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name topic-configuration --alter --delete-config min.insync.replicas
```