
## Features

- Used Spring Boot as a backend framework
- Databased used - MongoDb and MySql
- Asyncronous Processing by Message Queue Kafka
- Managed Different Service Discovery by Netflix Eureka Server



## Installation

- Install JAVA (17+)
- Install IntellJ
- Install MongoDB
- Intsall Mongo Compass
- Install MySql 
- Install DBreaver

#### Install Kafka on Docker by Docker Compose

```bash
services:
  kafka:
    ports:
      - 29094:29092
    image: confluentinc/cp-kafka:latest
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_LISTENERS: PLAINTEXT://:9092,PLAINTEXT_HOST://:29092
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,PLAINTEXT_HOST://127.0.0.1:29094
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    depends_on:
      - zookeeper
    networks: 
      - kafka_network
  zookeeper:
    ports:
      - 32181:2181
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    image: confluentinc/cp-zookeeper:latest
    networks: 
      - kafka_network
networks:
  kafka_network:
    name: kafka_docker_example_net
```

#### Start Service : 
```
docker-compose up
```

#### Connect with Network : 
```
docker network connect kafka_docker_example_net spark-up-spark-master-1
```
## API Reference of QnA Service

#### Get posts of a user

```http
  GET /userspost/getPost/{id}
```

| Route-value | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `string` | **Required**. User id of Quora User|

#### Get all posts

```http
  GET /userspost/getAllPost
```


#### Add new Post by a user

```http
  POST /userspost/addPost
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `string` | **Required**.  id of Quora Post
| `title` | `string` | **Required**. Title of post
| `userid` | `long` | **Required**. User id of Quora User
| `body` | `string` | **Required**. Body of post


#### Update a posts of a user

```http
  POST /userspost/updatePost/{id}
```

| Request Value | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `string` | **Required**. User id of Quora User

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `string` | **Required**.  id of Quora Post
| `title` | `string` | **Required**. Title of post
| `userid` | `long` | **Required**. User id of Quora User
| `body` | `string` | **Required**. Body of post




