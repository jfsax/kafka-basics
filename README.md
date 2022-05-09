# kafka basics
how to setup, run and send/consume messages in Kafka

## download & setup
- https://kafka.apache.org/downloads
- (mac) https://www.tutorialkart.com/apache-kafka/install-apache-kafka-on-mac/
- (windows) https://www.geeksforgeeks.org/how-to-install-and-run-apache-kafka-on-windows/

## running kafka & zookeeper
- commands should be run from kafka's root directory
- zookeeper must be started before kafka

- open a terminal and start zookeeper with the following command:

```shell
(mac) bin/zookeeper-server-start.sh config/zookeeper.properties
(windows) .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
```
- open a second terminal and start kafka:

```shell
(mac) bin/kafka-server-start.sh config/server.properties
(windows) .\bin\windows\kafka-server-start.bat .\config\server.properties
```

## kafka commands:
### creating a topic
- kafka will create topics automatically if the property `auto.create.topics.enable` is added to the file `server.properties`
- to create your topic manually, open a third terminal and run:
```shell
(mac) bin/kafka-topics.sh --create --bootstrap-server=localhost:9092 --replication-factor=1 --partitions=1 --topic="TOPIC_NAME"
(windows) .\bin\windows\kafka-topics.bat --create --bootstrap-server=localhost:9092 --replication-factor=1 --partitions=1 --topic="TOPIC_NAME"
```

### listing topics
```shell
(mac) bin/kafka-topics.sh --list --bootstrap-server=localhost:9092
(windows) .\bin\windows\kafka-topics.bat --list --bootstrap-server=localhost:9092
```

### sending messages (producer)
- a producer can send data with or without a key. if a key is not specified, it will remain `null` by default.
- to send a key-value message, add the properties: `--property "parse.key=true" --property "key.separator=;"` to the command below. messages with the same key will be sent to the same partition.
```shell
(mac) bin/kafka-console-producer.sh --broker-list=localhost:9092 --topic="TOPIC_NAME"
(windows) .\bin\windows\kafka-console-producer.bat --broker-list=localhost:9092 --topic="TOPIC_NAME"
```
- after running the command, type your message and press enter.
- CTRL+C quits the producer.

### reading messages (consumer)
```shell
(mac) bin/kafka-console-consumer.sh --bootstrap-server=localhost:9092 --topic="TOPIC_NAME"
(windows) .\bin\windows\kafka-console-consumer.bat --bootstrap-server=localhost:9092 --topic="TOPIC_NAME"
```

- the command above will only read messages sent <b>after</b> the consumer started running.
- to read messages sent before the consumer started reading, add the property `--from-beginning` to the command above.

### deleting a message
- first create a configuration file in JSON to describe the record(s) you wish to delete:
```
echo '{ "partitions": [ { "topic": "TOPIC_NAME", "partition": 0, "offset": 1 } ],  "version": 1 }' > delete-records.json
```

- then run:
```shell
(mac) bin/kafka-delete-records.sh --bootstrap-server=localhost:9092 --offset-json-file delete-records.json
(windows) .\bin\windows\kafka-delete-records.bat --bootstrap-server=localhost:9092 --offset-json-file delete-records.json
```
