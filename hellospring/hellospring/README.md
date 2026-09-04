# Hello Spring

A minimal Spring Boot web application used as a learning sandbox for Spring MVC and Actuator.

## Tech Stack

- Java 21
- Spring Boot 4.1.1 (`spring-boot-starter-webmvc`, `spring-boot-starter-actuator`)
- Maven (via included `mvnw` / `mvnw.cmd` wrapper)

## Prerequisites

- JDK 21+
- No local Maven install required — use the wrapper scripts below.

## Getting Started

Run the application:

```bash
./mvnw spring-boot:run        # macOS/Linux
./mvnw.cmd spring-boot:run    # Windows
```

The app starts on `http://localhost:8080` by default.

Run the tests:

```bash
./mvnw test
```

## Endpoints

| Method | Path               | Description                          |
|--------|--------------------|---------------------------------------|
| GET    | `/hello`           | Returns a plain-text greeting         |
| GET    | `/actuator/health` | Health check (liveness/readiness)     |

## Project Structure

```
src/main/java/org/com/aboubakr/hellospring/
├── HellospringApplication.java   # Application entry point (@SpringBootApplication)
└── HelloController.java          # REST controller — add new controllers here

src/main/resources/
└── application.properties        # App configuration

src/test/java/...                 # Tests mirror the main package structure
```

## Adding a New Endpoint

1. Create a new class under `src/main/java/org/com/aboubakr/hellospring/`, annotated `@RestController`.
2. Map methods with `@GetMapping`, `@PostMapping`, etc.
3. Spring's component scan (via `@SpringBootApplication`) picks it up automatically — no manual registration needed.

## Configuration

App settings live in `src/main/resources/application.properties`. Common additions as the app grows:

```properties
server.port=8080
management.endpoints.web.exposure.include=health,info
```

## Running with Docker

The Dockerfile expects a pre-built jar — it does not compile the application itself. Build it first:

```bash
./mvnw package -DskipTests
```

Then build the image:

```bash
docker build -t hellospring .
```

Run the container:

```bash
docker run -p 8080:8080 hellospring
```

The app is then reachable at `http://localhost:8080`, same as running it locally.

## Roadmap

- [ ] Add a persistence layer (e.g. Spring Data JPA)
- [ ] Add request validation and error handling
- [ ] Add API documentation (e.g. springdoc-openapi)
- [ ] Containerize with a Dockerfile
