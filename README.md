# IBM MQ Source Connector
The IBM MQ Source Connector is used to read messages from an IBM MQ cluster and write them to a Kafka topic.

Reference: https://github.com/ibm-messaging/kafka-connect-mq-source

# Building the connector
## Clone this repository:
```
$ git clone https://github.com/augustoximenes/kafka-connect-mq-source
$ cd kafka-connect-mq-source
```
## Clone IBM git repository into this:
```
$ git clone https://github.com/ibm-messaging/kafka-connect-mq-source.git
$ cd kafka-connect-mq-source
```

## Build the connector using Maven:
```
mvn clean package
```

# Running in distributed mode
## Build image:
```
docker build -t kafkaconnect-with-mq-source:1.3.1 .
```

## Run:
Go back to the parent folder (kafka-connect-mq-source) and up the containers:
```
$ cd ..
$ docker-compose up -d
```
# Configure IBM MQ and Kafka
## Create Queue:
Access MQ Console (https://localhost:9443/ibmmq/console/) and create the queue.
```
- user: user
- password: passw0rd

- queue: QL_INPUT
```

## Create Topic:
```
docker exec broker kafka-topics --bootstrap-server broker:9092  --create --topic TP_OUTPUT
```

# Configure MQ Connector
## Start the MQ Connector
```
curl -X POST -H "Content-Type: application/json" http://localhost:8083/connectors \
  --data "@mq-source.json"
```

# Go to the test:
## Consume the messages from topic:
```
docker exec --interactive --tty broker kafka-console-consumer --bootstrap-server broker:9092 --topic TP_OUTPUT --from-beginning
```

## Produce message to queue:
Access MQ Console (https://localhost:9443/ibmmq/console/) and create the message to QL_INPUT queue.