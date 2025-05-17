# Example Voting App - Student Project

This is a simple distributed application running across multiple Docker containers. Your task will be to build the Docker Compose file to make the application work.

## Application Overview

This application provides a voting system where users can vote between two options, with results displayed in real-time:

![Architecture diagram](architecture.excalidraw.png)

The application consists of:
* A front-end web app in [Python](/vote) that lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) queue which collects new votes
* A [.NET](/worker/) worker which consumes votes and stores them in the database
* A [Postgres](https://hub.docker.com/_/postgres/) database backed by a Docker volume
* A [Node.js](/result) web app which shows the results of the voting in real time

## Prerequisites

* Install [Docker Desktop](https://www.docker.com/products/docker-desktop) for Mac or Windows
* On Linux, make sure you have the latest version of [Docker and Docker Compose](https://docs.docker.com/compose/install/)

## Your Task

Your task is to build a working `docker-compose.yml` file that:

1. Sets up all five services (vote, redis, worker, db, result)
2. Configures the necessary networks
3. Sets up proper volume mapping for persistent data
4. Ensures services start in the correct order (using dependencies)
5. Exposes the necessary ports for the web interfaces

### Service Requirements

* **vote**: Python web app that needs to be accessible on port 8080
* **redis**: Queue service that the vote app writes to and the worker reads from
* **worker**: .NET service that processes votes from Redis and stores in Postgres
* **db**: Postgres database that stores vote data
* **result**: Node.js web app that displays results and needs to be accessible on port 8081

## Checking Your Work

Once you have created your docker-compose.yml file, run:

```shell
docker compose up
```

The application should be accessible at:
* Vote application: [http://localhost:8080](http://localhost:8080)
* Results application: [http://localhost:8081](http://localhost:8081)

## Tips

* Examine each service's Dockerfile to understand its requirements
* Consider how services depend on each other
* Think about which services need to communicate with each other and set up networks accordingly
* Remember to set up health checks for critical services
* The voting application only accepts one vote per client browser

Good luck!
