# Spring boot microservices sandbox
Playing with DDD, Hexagonal architecture, SAGA, Kafka, Outbox pattern 

To run kafka cluster
- docker-compose -f common.yml -f zookeeper.yml up
- docker-compose -f common.yml -f kafka_cluster.yml up

The init_kafka.yml is to create the kafka topics

- docker-compose -f common.yml -f init_kafka.yml up


mvn clean install -e 