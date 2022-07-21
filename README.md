# IBM MQ Source Connector
The IBM MQ Source Connector is used to read messages from an IBM MQ cluster and write them to a Kafka topic.

Reference: https://github.com/ibm-messaging/kafka-connect-mq-source

# Building the connector
## Clone git repository:
```
git clone https://github.com/ibm-messaging/kafka-connect-mq-source.git
```

## Change directory into the kafka-connect-mq-source directory:
```
cd kafka-connect-mq-source
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
```
docker-compose up -d
```

## Configure MQ Connector
Replace mq-source.json file
```
mv ../mq-source ./config
```

## Start the MQ Connector
```
curl -X POST -H "Content-Type: application/json" http://localhost:8083/connectors \
  --data "@./config/mq-source.json"
```