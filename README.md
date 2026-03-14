# Service Discovery

A Spring Boot application providing service discovery using Netflix Eureka Server.

## Overview

This project runs a Eureka Server that acts as a service registry for microservices. Services register themselves with the Eureka Server and can discover other registered services, enabling dynamic service-to-service communication without hardcoded URLs.

## Tech Stack

- Java 25
- Spring Boot 3.5.0
- Spring Cloud 2024.0.0
- Netflix Eureka Server
- Gradle 9.2
- Docker

## Project Structure

```
service-discovery/
├── eureka-server/          # Eureka Server module
│   ├── src/
│   ├── Dockerfile
│   └── build.gradle
├── docker-compose.yml
├── build.gradle            # Root build config
└── settings.gradle
```

## Running Locally

```bash
./gradlew clean build
./gradlew :eureka-server:bootRun
```

Eureka dashboard: http://localhost:8761

## Running with Docker

```bash
./gradlew clean build
docker-compose up --build
```

## Configuration

| Property | Default | Description |
|---|---|---|
| `server.port` | 8761 | Eureka Server port |
| `eureka.client.register-with-eureka` | false | Server does not register with itself |
| `eureka.client.fetch-registry` | false | Server does not fetch its own registry |

## Registering a Client Service

Add the Eureka client dependency to your microservice and configure it to point to this server:

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```