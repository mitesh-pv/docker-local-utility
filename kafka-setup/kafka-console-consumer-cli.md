## Kafka Console Consumer CLI

1. Consumer form the tail of the topic
2. Consumer from the begining of the topic
3. Show both key and value in the output

### Consume from tail

* Consume messages from tail of the topic
```sh
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic 
```

### Consume message from the begining of the topic
```sh
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic  --from-beginning
```

### Display key, value and the timestamp in consumer
```sh
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic  --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.timestamp=true --property print.key=true --property print.value=true
```