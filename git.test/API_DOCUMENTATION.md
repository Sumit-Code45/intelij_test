# Git Test Application - API Documentation

## Table of Contents
- [Project Overview](#project-overview)
- [Getting Started](#getting-started)
- [API Reference](#api-reference)
- [Configuration](#configuration)
- [Testing](#testing)
- [Build and Deployment](#build-and-deployment)
- [Examples and Usage](#examples-and-usage)

## Project Overview

**Project Name:** git.test  
**Version:** 0.0.1-SNAPSHOT  
**Java Version:** 17  
**Spring Boot Version:** 3.4.5  
**Build Tool:** Maven  

This is a minimal Spring Boot application designed as a demo project. It provides a foundational structure for building Java-based web applications using the Spring framework.

## Getting Started

### Prerequisites
- Java 17 or higher
- Maven 3.6+ (or use the included Maven wrapper)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd git.test
   ```

2. **Build the application**
   ```bash
   ./mvnw clean compile
   ```

3. **Run the application**
   ```bash
   ./mvnw spring-boot:run
   ```

4. **Run tests**
   ```bash
   ./mvnw test
   ```

The application will start on the default port (8080) unless configured otherwise.

## API Reference

### Application Class

**Package:** `git.test`  
**Class:** `Application`  
**Type:** Main Application Class  

#### Public Methods

##### `main(String[] args)`

**Description:** The entry point of the Spring Boot application. Bootstraps and launches the Spring application context.

**Parameters:**
- `args` (String[]): Command-line arguments passed to the application

**Return Type:** `void`

**Usage Example:**
```java
public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
}
```

**Annotations:**
- `@SpringBootApplication`: Combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`

#### Class Features

- **Auto-configuration**: Automatically configures Spring Boot based on classpath dependencies
- **Component scanning**: Scans for Spring components in the `git.test` package and sub-packages
- **Embedded server**: Includes embedded Tomcat server for standalone deployment

#### Usage Examples

**Basic Application Startup:**
```java
package git.test;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

**Custom Application Startup with Properties:**
```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(Application.class);
    app.setDefaultProperties(Collections.singletonMap("server.port", "8081"));
    app.run(args);
}
```

## Configuration

### Application Properties

**File:** `src/main/resources/application.properties`

#### Available Properties

| Property | Value | Description |
|----------|-------|-------------|
| `spring.application.name` | `git.test` | The name of the Spring Boot application |

#### Configuration Examples

**Basic Configuration:**
```properties
# Application identification
spring.application.name=git.test

# Server configuration (optional)
server.port=8080
server.servlet.context-path=/api

# Logging configuration (optional)
logging.level.git.test=DEBUG
logging.level.org.springframework=INFO
```

**Database Configuration (when adding database support):**
```properties
# Database configuration
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=create-drop
```

**Actuator Configuration (when adding actuator dependency):**
```properties
# Management endpoints
management.endpoints.web.exposure.include=health,info,metrics
management.endpoint.health.show-details=always
```

## Testing

### ApplicationTests Class

**Package:** `git.test`  
**Class:** `ApplicationTests`  
**Type:** Integration Test Class  

#### Test Methods

##### `contextLoads()`

**Description:** Verifies that the Spring application context loads successfully without any errors.

**Test Type:** Integration test  
**Annotations:** `@Test`, `@SpringBootTest`  

**Implementation:**
```java
@Test
void contextLoads() {
    System.out.println("sumit kushwhaa");
}
```

#### Testing Examples

**Running Tests:**
```bash
# Run all tests
./mvnw test

# Run tests with coverage
./mvnw test jacoco:report

# Run specific test class
./mvnw test -Dtest=ApplicationTests
```

**Adding Additional Tests:**
```java
@SpringBootTest
class ApplicationTests {
    
    @Test
    void contextLoads() {
        // Test passes if application context loads successfully
    }
    
    @Test
    void applicationStartsSuccessfully() {
        // Additional test for application startup
        assertThat(true).isTrue();
    }
    
    @Test
    @DisplayName("Should load application properties")
    void shouldLoadApplicationProperties() {
        assertThat(System.getProperty("spring.application.name"))
            .isEqualTo("git.test");
    }
}
```

## Build and Deployment

### Maven Configuration

**File:** `pom.xml`

#### Key Dependencies

| Dependency | Purpose |
|------------|---------|
| `spring-boot-starter` | Core Spring Boot functionality |
| `spring-boot-starter-test` | Testing framework including JUnit 5, Mockito, AssertJ |

#### Build Commands

```bash
# Clean and compile
./mvnw clean compile

# Package as JAR
./mvnw clean package

# Run without packaging
./mvnw spring-boot:run

# Generate project reports
./mvnw site
```

#### Deployment Options

**JAR Deployment:**
```bash
# Build executable JAR
./mvnw clean package

# Run the JAR
java -jar target/git.test-0.0.1-SNAPSHOT.jar
```

**Docker Deployment:**
```dockerfile
FROM openjdk:17-jre-slim
COPY target/git.test-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

## Examples and Usage

### Adding REST Controllers

To extend this application with REST APIs:

```java
package git.test.controller;

import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class HelloController {
    
    @GetMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }
    
    @GetMapping("/hello/{name}")
    public String helloName(@PathVariable String name) {
        return "Hello, " + name + "!";
    }
}
```

### Adding Services

```java
package git.test.service;

import org.springframework.stereotype.Service;

@Service
public class HelloService {
    
    public String generateGreeting(String name) {
        return "Hello, " + name + "!";
    }
}
```

### Adding Configuration Classes

```java
package git.test.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {
    
    @Bean
    public String applicationVersion() {
        return "1.0.0";
    }
}
```

### Environment-Specific Configuration

**application-dev.properties:**
```properties
spring.application.name=git.test-dev
logging.level.git.test=DEBUG
server.port=8081
```

**application-prod.properties:**
```properties
spring.application.name=git.test-prod
logging.level.git.test=WARN
server.port=8080
```

**Running with profiles:**
```bash
# Development profile
./mvnw spring-boot:run -Dspring.profiles.active=dev

# Production profile
java -jar target/git.test-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

## Error Handling and Troubleshooting

### Common Issues

1. **Port Already in Use:**
   ```
   Error: Port 8080 already in use
   Solution: Change port in application.properties or stop the conflicting process
   ```

2. **Java Version Mismatch:**
   ```
   Error: Unsupported class file major version
   Solution: Ensure Java 17+ is installed and JAVA_HOME is set correctly
   ```

3. **Maven Wrapper Permissions:**
   ```bash
   chmod +x mvnw
   ```

### Health Checks

Add actuator dependency for health monitoring:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Access health endpoint: `http://localhost:8080/actuator/health`

## Contributing

1. Follow Java coding standards
2. Write unit tests for new functionality
3. Update documentation for API changes
4. Use meaningful commit messages

## License

This project is a demo application. Check with your organization for specific licensing requirements.

---

**Generated Documentation Version:** 1.0  
**Last Updated:** December 2024  
**Spring Boot Version:** 3.4.5