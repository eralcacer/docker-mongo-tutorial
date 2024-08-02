# Docker Practice Tutorial

This tutorial demonstrates how to create a simple server that connects to a MongoDB container running in Docker. The tutorial covers creating a Docker Compose file to manage the server and the MongoDB container.

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- Docker
- Docker Compose

## Project Structure

├── Dockerfile

├── docker-compose.yml

├── docker-compose-dev.yml

├── index.js

├── package.json

└── README.md

## Dockerfile alternative:

The Dockerfile defines the image for the server application:

First I created the application server that connects to the database. Then, I downloaded and created a container with the Mongo image in Docker. After that, I created a network to keep my app and database within the same network so they could reach each other. Next, I created an image for my app. Finally, I created a container on ports 27017 for my database, and 3000 for my app. I run both containers using

```
docker build -t myapp:1.0.0 . #builds the image for my app
docker create -p27017:27017 --name monguito --network mynetwork -e MONGO_INITDB_ROOT_USERNAME=enrique -e MONGO_INITDB_ROOT_PASSWORD=password mongo
docker create -p3000:3000 --name chanchito --network mynetwork myapp:1.0.0
docker start monguito
docker start chanchito
```

## Docker Compose Alternative

The docker-compose.yml file defines the services for the application and MongoDB:

### Production environment

```
docker compose up
```

### Using nodemon and continuous development:

```
docker compose -f docker-compose-dev.yml up
```

## Running the Application

### Using Docker CLI

1. Build the image for your app:

```
docker build -t myapp:1.0.0 .
```

2. Create and start the MongoDB container:

```
docker create -p27017:27017 --name monguito --network mynetwork -e MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo
docker start monguito
```

3. Create and start the application container:

```
docker create -p3000:3000 --name chanchito --network mynetwork myapp:1.0.0
docker start chanchito
```

### Using Docker Compose

1. Start both containers using Docker Compose:

```
docker compose up
```

2. For continuous development with nodemon, use the development Docker Compose file:

```
docker compose -f docker-compose-dev.yml up
```

## Application Endpoints

- `GET /`: Lists all animals.
- `GET /crear`: Creates a new animal.

# Acknowledgments

Thanks to the @nschurmann for providing valuable resources and tools.
