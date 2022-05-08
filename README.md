# kafka basics
How to setup, run and send/consume messages in Kafka

# kafka basics

### download && setup
- https://kafka.apache.org/downloads
- (mac)https://www.tutorialkart.com/apache-kafka/install-apache-kafka-on-mac/
- (windows)https://www.geeksforgeeks.org/how-to-install-and-run-apache-kafka-on-windows/

## running kafka & zookeeper
- run the following commands from kafka's root folder
- obs: zookeeper must be started before kafka
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
