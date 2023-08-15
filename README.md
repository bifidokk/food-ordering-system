# Spring boot microservices sandbox
Playing with DDD, Hexagonal architecture, SAGA, Kafka, Outbox pattern 

To run kafka cluster:
```
docker-compose -f common.yml -f zookeeper.yml up
docker-compose -f common.yml -f kafka_cluster.yml up
```


The init_kafka.yml is to create the kafka topics:

```
docker-compose -f common.yml -f init_kafka.yml up
```

```
mvn clean install -e 
```

To create an order:
```
POST http://localhost:8181/orders
```

```json
{
  "customerId": "d215b5f8-0249-4dc5-89a3-51fd148cfb41",
  "restaurantId": "d215b5f8-0249-4dc5-89a3-51fd148cfb45",
  "address": {
    "street": "street_1",
    "postalCode": "1000AB",
    "city": "Amsterdam"
  },
  "price": 200.00,
  "items": [
    {
      "productId": "d215b5f8-0249-4dc5-89a3-51fd148cfb48",
      "quantity": 1,
      "price": 50.00,
      "subTotal": 50.00
    },
    {
      "productId": "d215b5f8-0249-4dc5-89a3-51fd148cfb48",
      "quantity": 3,
      "price": 50.00,
      "subTotal": 150.00
    }
  ]
}
```

Response

```json
{
    "orderTrackingId": "b39f4dd4-fca6-4f6b-b707-6a364c8f6338",
    "orderStatus": "PENDING",
    "message": "Order created successfully"
}
```

To check order status:
```
GET http://localhost:8181/orders/b39f4dd4-fca6-4f6b-b707-6a364c8f6338
```

Response
```json
{
    "orderTrackingId": "b39f4dd4-fca6-4f6b-b707-6a364c8f6338",
    "orderStatus": "APPROVED",
    "failureMessages": []
}
```