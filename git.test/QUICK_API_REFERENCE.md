# Quick API Reference Guide

## 📋 Project Summary
- **Name:** git.test
- **Type:** Spring Boot Application
- **Java:** 17
- **Spring Boot:** 3.4.5
- **Build:** Maven

## 🚀 Quick Start Commands

```bash
# Run application
./mvnw spring-boot:run

# Build JAR
./mvnw clean package

# Run tests
./mvnw test

# Run built JAR
java -jar target/git.test-0.0.1-SNAPSHOT.jar
```

## 📦 Public Classes & Methods

### `git.test.Application`
```java
@SpringBootApplication
public class Application {
    public static void main(String[] args)  // Application entry point
}
```

### `git.test.ApplicationTests`
```java
@SpringBootTest
class ApplicationTests {
    @Test void contextLoads()  // Integration test
}
```

## ⚙️ Configuration

### application.properties
```properties
spring.application.name=git.test    # App name
server.port=8080                    # Server port (optional)
logging.level.git.test=INFO         # Logging level (optional)
```

## 🔧 Maven Dependencies

| Dependency | Purpose |
|------------|---------|
| `spring-boot-starter` | Core Spring Boot |
| `spring-boot-starter-test` | Testing framework |

## 🌐 Default Endpoints

- **Application:** `http://localhost:8080`
- **Health (with actuator):** `http://localhost:8080/actuator/health`

## 📝 Common Extensions

### Add REST Controller
```java
@RestController
public class HelloController {
    @GetMapping("/hello")
    public String hello() { return "Hello World!"; }
}
```

### Add Service
```java
@Service
public class MyService {
    public String doSomething() { return "result"; }
}
```

### Add Configuration
```java
@Configuration
public class AppConfig {
    @Bean
    public String myBean() { return "value"; }
}
```

## 🛠️ Development Commands

```bash
# Development mode with auto-restart
./mvnw spring-boot:run -Dspring.profiles.active=dev

# Custom port
./mvnw spring-boot:run -Dserver.port=8081

# With debug logging
./mvnw spring-boot:run -Ddebug=true

# Skip tests
./mvnw spring-boot:run -DskipTests
```

## 🐳 Docker Quick Setup

```dockerfile
FROM openjdk:17-jre-slim
COPY target/git.test-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

```bash
# Build and run
docker build -t git-test .
docker run -p 8080:8080 git-test
```

## 🧪 Testing Patterns

```java
@SpringBootTest
class MyTests {
    @Autowired
    private ApplicationContext context;
    
    @Test
    void testSomething() {
        assertThat(context).isNotNull();
    }
}
```

## 📊 Monitoring & Health

Add to `pom.xml`:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Endpoints:
- `/actuator/health` - Health status
- `/actuator/info` - Application info
- `/actuator/metrics` - Application metrics

## 🔍 Troubleshooting

| Issue | Solution |
|-------|----------|
| Port 8080 in use | `server.port=8081` in properties |
| Tests fail | `./mvnw clean test` |
| Build fails | Check Java 17 installation |
| Context won't load | Check configuration and dependencies |

## 📚 Key Annotations

| Annotation | Purpose |
|------------|---------|
| `@SpringBootApplication` | Main app class |
| `@RestController` | REST endpoints |
| `@Service` | Business logic |
| `@Repository` | Data access |
| `@Configuration` | Bean configuration |
| `@Component` | Generic component |
| `@Test` | Test method |
| `@SpringBootTest` | Integration test |

## 🔧 Profile Configuration

### application-dev.properties
```properties
spring.application.name=git.test-dev
logging.level.git.test=DEBUG
server.port=8081
```

### application-prod.properties
```properties
spring.application.name=git.test-prod
logging.level.git.test=WARN
server.port=8080
```

### Usage
```bash
# Development
./mvnw spring-boot:run -Dspring.profiles.active=dev

# Production
java -jar app.jar --spring.profiles.active=prod
```

## 📋 Checklist for New Features

- [ ] Add required dependencies to `pom.xml`
- [ ] Create necessary classes with proper annotations
- [ ] Add configuration properties if needed
- [ ] Write unit/integration tests
- [ ] Update documentation
- [ ] Test locally with `./mvnw spring-boot:run`

---

**🚀 Ready to develop!** Use this guide for quick reference while building your Spring Boot application.