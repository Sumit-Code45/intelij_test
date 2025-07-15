# Javadoc API Reference

## Package: git.test

### Class: Application

```java
@SpringBootApplication
public class Application
```

**Inheritance Hierarchy:**
```
java.lang.Object
  └── git.test.Application
```

**Annotations:**
- `@SpringBootApplication`

**Description:**
The main application class for the Spring Boot application. This class serves as the entry point for the application and configures Spring Boot auto-configuration, component scanning, and configuration properties.

**Since:** Version 0.0.1-SNAPSHOT

---

#### Method: main

```java
public static void main(String[] args)
```

**Parameters:**
- `args` - String array containing command-line arguments passed to the application

**Returns:** `void`

**Description:**
The main method that serves as the entry point for the Spring Boot application. This method uses SpringApplication.run() to bootstrap the application, which will:
- Create an appropriate ApplicationContext
- Register appropriate beans
- Start the embedded web server (if applicable)
- Activate configured profiles

**Example Usage:**
```java
Application.main(new String[]{"--server.port=8081"});
```

**Throws:** No declared exceptions, but may throw RuntimeException if application fails to start

**Since:** Version 0.0.1-SNAPSHOT

---

## Package: git.test (Test Classes)

### Class: ApplicationTests

```java
@SpringBootTest
class ApplicationTests
```

**Inheritance Hierarchy:**
```
java.lang.Object
  └── git.test.ApplicationTests
```

**Annotations:**
- `@SpringBootTest`

**Description:**
Integration test class for the Spring Boot application. This class contains tests that verify the application context loads properly and the application can start successfully.

**Test Configuration:**
- Uses Spring Boot test framework
- Loads full application context
- Supports dependency injection in tests

**Since:** Version 0.0.1-SNAPSHOT

---

#### Method: contextLoads

```java
@Test
void contextLoads()
```

**Returns:** `void`

**Annotations:**
- `@Test`

**Description:**
Integration test method that verifies the Spring application context loads without errors. This is a basic smoke test that ensures:
- All auto-configuration works correctly
- All beans can be created successfully
- No circular dependencies exist
- Configuration properties are valid

**Test Behavior:**
- Prints "sumit kushwhaa" to standard output
- Implicitly tests context loading (test fails if context cannot load)

**Assertions:** None explicit (context loading failure would cause test failure)

**Since:** Version 0.0.1-SNAPSHOT

---

## Spring Boot Annotations Reference

### @SpringBootApplication

**Target:** Class  
**Retention:** Runtime  

**Description:**
Meta-annotation that combines three commonly used Spring annotations:
- `@Configuration`: Indicates that the class can be used as a source of bean definitions
- `@EnableAutoConfiguration`: Enables Spring Boot's auto-configuration mechanism
- `@ComponentScan`: Enables component scanning in the package of the annotated class

**Equivalent to:**
```java
@Configuration
@EnableAutoConfiguration
@ComponentScan
```

**Auto-Configuration Features:**
- Automatically configures beans based on classpath dependencies
- Configures embedded web server (Tomcat by default)
- Sets up default logging configuration
- Enables Spring MVC if web dependencies are present

---

### @SpringBootTest

**Target:** Class  
**Retention:** Runtime  

**Description:**
Annotation for Spring Boot integration tests. This annotation:
- Loads the complete Spring application context
- Supports web environment testing
- Enables dependency injection in test classes
- Provides access to ApplicationContext

**Default Configuration:**
- `webEnvironment = SpringBootTest.WebEnvironment.MOCK`
- Loads configuration from `@SpringBootApplication` or `@SpringBootConfiguration`
- Uses random port for web server if needed

---

## Configuration Properties

### Application Properties Schema

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `spring.application.name` | String | `git.test` | Application name used for identification |

### Extended Configuration Options

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `server.port` | Integer | `8080` | Server HTTP port |
| `server.servlet.context-path` | String | `/` | Context path for the application |
| `logging.level.<package>` | String | `INFO` | Logging level for specific packages |
| `spring.profiles.active` | String | `default` | Active Spring profiles |

---

## Maven Dependencies API

### Core Dependencies

#### spring-boot-starter

**Group ID:** `org.springframework.boot`  
**Artifact ID:** `spring-boot-starter`  
**Version:** Inherited from parent (3.4.5)  

**Includes:**
- Spring Core
- Spring Context
- Spring Beans
- Auto-configuration
- Logging (Logback)
- YAML support

#### spring-boot-starter-test

**Group ID:** `org.springframework.boot`  
**Artifact ID:** `spring-boot-starter-test`  
**Scope:** `test`  
**Version:** Inherited from parent (3.4.5)  

**Includes:**
- JUnit 5 (Jupiter)
- Mockito
- AssertJ
- Hamcrest
- Spring Test
- Spring Boot Test

---

## Build Lifecycle

### Maven Phases

| Phase | Description | Commands |
|-------|-------------|----------|
| `validate` | Validate project structure | `./mvnw validate` |
| `compile` | Compile source code | `./mvnw compile` |
| `test` | Run unit tests | `./mvnw test` |
| `package` | Create JAR/WAR | `./mvnw package` |
| `verify` | Run integration tests | `./mvnw verify` |
| `install` | Install to local repository | `./mvnw install` |

### Spring Boot Goals

| Goal | Description | Command |
|------|-------------|---------|
| `spring-boot:run` | Run application in place | `./mvnw spring-boot:run` |
| `spring-boot:repackage` | Create executable JAR | `./mvnw spring-boot:repackage` |
| `spring-boot:build-info` | Generate build information | `./mvnw spring-boot:build-info` |

---

## Application Lifecycle

### Startup Sequence

1. **JVM Initialization**
   - Load Application class
   - Execute main() method

2. **Spring Boot Bootstrap**
   - Create SpringApplication instance
   - Configure application properties
   - Determine web application type

3. **Context Creation**
   - Create ApplicationContext
   - Load configuration classes
   - Register auto-configuration

4. **Bean Creation**
   - Instantiate beans
   - Resolve dependencies
   - Apply post-processors

5. **Server Startup** (if web application)
   - Start embedded server
   - Deploy application
   - Begin accepting requests

### Shutdown Sequence

1. **Graceful Shutdown Signal**
2. **Stop Accepting New Requests**
3. **Complete Ongoing Requests**
4. **Destroy Beans**
5. **Close ApplicationContext**
6. **Stop JVM**

---

## Error Handling

### Common Exception Types

| Exception | Cause | Solution |
|-----------|-------|----------|
| `BindException` | Port already in use | Change server.port or stop conflicting process |
| `ClassNotFoundException` | Missing dependency | Add required dependency to pom.xml |
| `BeanCreationException` | Bean configuration error | Check configuration and dependencies |
| `ApplicationContextException` | Context loading failure | Review auto-configuration and properties |

### Debug Configuration

```properties
# Enable debug logging
logging.level.org.springframework=DEBUG
logging.level.org.springframework.boot=DEBUG

# Show auto-configuration report
debug=true

# Show web server details
logging.level.org.springframework.boot.web.embedded=DEBUG
```

---

**Documentation Generated:** December 2024  
**Spring Boot Version:** 3.4.5  
**Java Version:** 17  
**Maven Version:** 3.9+