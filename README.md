# Gateway Service

A reactive API gateway providing a single entry point for restaurant microservices with service discovery, rate limiting, retries, and circuit breakers.

Part of: https://github.com/topics/korjick-java-microservice-restaurant

## Tech Stack

- **Language & Framework:** Java 25, Spring Boot 4 (Spring WebFlux, Project Reactor)
- **API Gateway:** Spring Cloud Gateway (Load-Balanced Routing, Retry & Backoff)
- **Service Discovery & Configuration:** Netflix Eureka Client, Spring Cloud Config Client
- **Resilience:** Resilience4j (Circuit Breakers, Time Limiters)
- **Rate Limiting:** Spring Data Redis Reactive, Redis
- **Observability:** Spring Boot Actuator, Micrometer Tracing, Brave, Zipkin
- **Testing:** JUnit 5, Spring Boot Test
- **Containerization:** Cloud Native Buildpacks

## API Endpoints

Requests are routed through the gateway on port `9099` to services registered in Eureka.

- `/v1/menu-items/**` - Route requests to `menu-service`.
- `/v1/menu-orders/**` - Route requests to `orders-service`.
- `/v1/reviews/**` - Route requests to `review-service`.
- `/v1/menu-aggregate/**` - Route requests to `menu-aggregate-service`.

## Build and Run

Requires Java 25. Redis defaults to `localhost:6379`, and Eureka defaults to `http://localhost:8761/eureka/`. Start Redis, Eureka, and the target services to route requests.

The optional Config Server defaults to `http://localhost:9095` and can be configured with `CONFIG_SERVER_URL`. Zipkin defaults to `http://localhost:9411`.

```bash
# Run tests
./gradlew test

# Run application
./gradlew bootRun

# Build container image (requires Docker)
./gradlew bootBuildImage
```
