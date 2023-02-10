## Large Mesages in kafka

* Kafka has default of 1 MB per message in a topic, as large messages are inefficient.
* Two approaches to send large messages:
  * Send reference to the large data: HDFS, S3 or other cloud storage
  * Modify kafka parameters: need to change broker, producer and consumer settings in order to achieve this
    * Topic wise, kafka side:
    
    Broker side &rarr; Set `message.max.bytes` <br>
    Topic side &rarr; `max.message.bytes`

    Broker side max replication fetch size: <br>
      `replica.fetch.max.bytes=10485880` (in `server.properties`)

    Consumer side, fetch size should be increased otherwise it'll crash: <br>
    `max.partitoin.fetch.bytes=10485880`