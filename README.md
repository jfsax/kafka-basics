# kafka basics
How to setup, run and send/consume messages in Kafka

# kafka basics

## download & setup
- https://kafka.apache.org/downloads
- (mac)https://www.tutorialkart.com/apache-kafka/install-apache-kafka-on-mac/
- (windows)https://www.geeksforgeeks.org/how-to-install-and-run-apache-kafka-on-windows/

## running kafka & zookeeper
- run the following commands from kafka's root folder
- zookeeper must be started before kafka
- open a terminal and start zookeeper with the following command:

```shell
(mac) bin/kafka-server-start.sh config/server.properties
(windows) .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
```
- open a second terminal and start kafka:

```shell
(mac) bin/zookeeper-server-start.sh config/zookeeper.properties
(windows) .\bin\windows\kafka-server-start.bat .\config\server.properties
```

## kafka commands:
### creating a topic
- kafka will create topics automatically if `auto.create.topics.enable` is added to the file `config/server.properties`
- to create your topic manually, run:
```shell
(mac) bin/kafka-topics.sh --create --bootstrap-server=localhost:9092 --replication-factor=1 --partitions=1 --topic="TOPIC_NAME"
(windows) .\bin\windows\kafka-topics.bat --create --bootstrap-server=localhost:9092 --replication-factor=1 --partitions=1 --topic="TOPIC_NAME"
```

### listing topics
```shell
(mac) bin/kafka-topics.sh --list --bootstrap-server=localhost:9092
(windows) .\bin\windows\kafka-topics.bat --list --bootstrap-server=localhost:9092
```
