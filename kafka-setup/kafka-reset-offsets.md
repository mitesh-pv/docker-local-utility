## Kafka Console Consumer Reset Offsets

If we want to replay some data, or skip some messages which was problematic, we can reset offsets to skip or replay those messages.

### Steps to reset offsets:
1. Start/Stop console consumer
2. Reset Offset
3. Restart console consumer to see the outcome

* First create a topic with 3 partitions
```sh
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic second-topic --partitions 3
```

* Then create a producer for that topic
```sh
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first-topic
```

* Then create a consumer specifying consumer group
```sh
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group
```

* Now stop he consumer so that we can add Lag to the topic
* The lag looks like this

kconsumergroupdesc first-topic

```shell
Consumer group 'my-first-consumer-group' has no active members.

GROUP                   TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
my-first-consumer-group first-topic     0          15              17              2               -               -               -
my-first-consumer-group first-topic     1          15              17              2               -               -               -
my-first-consumer-group first-topic     2          11              13              2               -               -               -
```

* Now to reset offsets to beginning
```sh
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group --reset-offsets --to-earliest --execute
```
Output
```sh
GROUP                          TOPIC                          PARTITION  NEW-OFFSET
my-first-consumer-group        first-topic                    0          0
my-first-consumer-group        first-topic                    1          0
my-first-consumer-group        first-topic                    2          0
```

* Now start a consumer for the same consumer group, it'll start reading from the beginning
```sh
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group
```
This will be reading the messages from kafka from the starting as the offsets has been reset to beginning of the queue. <br>
The offsets cannot be reset when the consumer group is running, so we have to stop the consumer from consuming the messages for resetting the offsets.

* Shift the offsets forward(--shift-by 2)/backward (--shift-by -2)
- To Shift the offset forward, `--shift-by 2`
```sh
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group --reset-offsets --shift-by 2 --execute
```

- To Shift the offset backword, `--shift-by -2`
```sh
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --topic first-topic --group my-first-consumer-group --reset-offsets --shift-by -2 --execute
```

* Now consumer again, it'll start cosuming from 2 positions back in the offset
