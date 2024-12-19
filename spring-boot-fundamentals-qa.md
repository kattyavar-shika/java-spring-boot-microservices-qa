# Spring boot fundamentals Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)


## What is Spring Boot?
<details>
<summary>Answer</summary>

- Spring Boot is a framework built on top of the Spring Framework, aimed at simplifying the setup and development of Spring-based applications. 
- It provides production-ready features like embedded servers (Tomcat, Jetty, etc.), automatic configuration, and sensible defaults. 
- It minimizes the need for configuration and speeds up development by using annotations and conventions over configuration.

</details>

## Spring Boot Vs Spring Framework
<details>
<summary>Answer</summary>

 Comparison of Spring Boot and Spring Framework


| Feature/Aspect         | Spring Framework                      | Spring Boot                          |
|------------------------|---------------------------------------|--------------------------------------|
| **Configuration**      | Requires extensive XML or Java-based configuration. | Simplifies configuration with auto-configuration and annotations. |
| **Setup Time**         | More time-consuming setup due to manual configurations. | Quick setup with Spring Initializr and embedded server options. |
| **Project Structure**  | Flexible structure; can be complex based on project requirements. | Opinionated project structure with a standard convention. |
| **Dependency Management** | Manual management of dependencies; may require additional configuration. | Dependency management handled automatically with a starter dependency system. |
| **Embedded Server**    | Requires separate configuration to run on an embedded server. | Comes with embedded servers (Tomcat, Jetty, etc.) out of the box. |
| **Microservices Support** | Supports microservices but requires more configuration. | Designed for microservices with features like Spring Cloud integration. |
| **Development Speed**  | Slower development due to extensive boilerplate code. | Faster development with less boilerplate and rapid prototyping. |
| **Testing Support**    | Requires configuration for testing components. | Provides built-in support for testing with annotations like `@SpringBootTest`. |
| **Community & Ecosystem** | Large community, but Spring Boot has become the preferred choice. | Rapidly growing community; increasingly preferred for new applications. |
| **Learning Curve**     | Steeper learning curve due to complexity. | Easier to learn due to simplified features and clear documentation. |


</details>

## What are the key features of Spring Boot?
<details>
<summary>Answer</summary>

**Some key features of Spring Boot are:**
- Auto Configuration: Automatically configures the application based on the dependencies in the classpath.
- Embedded Web Server: Includes embedded servers like Tomcat, Jetty, or Undertow, eliminating the need to deploy to a separate application server.
- Standalone Application: Allows creating standalone applications that can be run from the command line using java -jar.
- Spring Boot Starters: Pre-configured templates (starters) to easily add functionality, such as spring-boot-starter-web, spring-boot-starter-data-jpa, etc.
- Spring Boot Actuator: Provides monitoring and management endpoints like health checks, metrics, etc.
- Spring Boot CLI: A command-line tool that allows rapid application development.

</details>


## Explain the role of @SpringBootApplication annotation.
<details>
<summary>Answer</summary>

- @SpringBootApplication is a convenience annotation that combines three annotations:
  - @Configuration: Marks the class as a configuration class (equivalent to @Bean definitions).
  - @EnableAutoConfiguration: Tells Spring Boot to start applying auto-configurations based on the classpath and other conditions.
  - @ComponentScan: Scans for Spring components (such as @Service, @Controller) within the same package and its sub-packages.

It is typically used on the main class to bootstrap the Spring Boot application.

</details>

## What is the difference between @Component, @Service, @Repository, and @Controller annotations in Spring Boot?
<details>
<summary>Answer</summary>

- @Component: A generic stereotype annotation for any Spring-managed bean.
- @Service: A specialized form of @Component, typically used for service layer classes that hold business logic.
- @Repository: A specialized @Component used to indicate a DAO (Data Access Object) that interacts with the database. It also has additional behavior, such as exception translation for database-related exceptions. It also enables exception translation, which converts database-related exceptions into Spring’s unchecked exceptions (e.g., DataAccessException).
- @Controller: A specialized @Component used in the web layer, typically for handling HTTP requests and returning views (used in Spring MVC).

</details>

## What is Auto-Configuration in Spring Boot?
<details>
<summary>Answer</summary>

- Auto-Configuration in Spring Boot attempts to automatically configure your Spring application based on the libraries you have on the classpath. For example, if Spring Boot detects that the spring-boot-starter-web dependency is in the classpath, it will automatically configure components such as an embedded Tomcat server, DispatcherServlet, etc., without requiring explicit configuration from the developer.

</details>

##  What is Spring Boot Actuator?
<details>
<summary>Answer</summary>

- Spring Boot Actuator is a set of tools built into Spring Boot to help monitor and manage Spring Boot applications in production. It provides features like:
  - Health checks
  - Metrics (JVM, database, etc.)
  - Auditing
  - Logging
  - Application environment information
  - Custom endpoints for managing and monitoring application performance

</details>

##  What is the role of application.properties or application.yml file in Spring Boot?
<details>
<summary>Answer</summary>

- The application.properties (or application.yml) file is used to configure various aspects of the Spring Boot application, such as:
  - Server configuration (port, context path)
  - Database connections (JDBC URL, username, password)
  - Logging levels
  - External properties (e.g., third-party API keys, credentials)

Spring Boot uses this file to externalize configuration, making it easier to manage across different environments.

</details>

## How can you create a RESTful API in Spring Boot?
<details>
<summary>Answer</summary>

- To create a RESTful API in Spring Boot:
  - Use @RestController for the controller class.
  - Define request mappings using @GetMapping, @PostMapping, @PutMapping, etc.
  - Use @RequestMapping for general request mappings.

```java
@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/greet")
    public String greet() {
        return "Hello, World!";
    }
}

```
This defines an API endpoint at /api/greet that responds to GET requests with "Hello, World!".

</details>

## What are Spring Boot Starters?
<details>
<summary>Answer</summary>

- Spring Boot Starters are pre-configured, ready-to-use dependencies that provide functionalities for common tasks such as web development, data access, messaging, etc.
- By including these starters, you can avoid manually adding individual dependencies.

**For example:**
- spring-boot-starter-web includes dependencies for building web applications (e.g., Spring MVC, embedded Tomcat).
- spring-boot-starter-data-jpa includes dependencies for working with JPA (Java Persistence API).

</details>


## What is @Value annotation in Spring Boot?
<details>
<summary>Answer</summary>

- The @Value annotation is used to inject values from properties files, environment variables, or system properties into Spring beans.

```java
@Value("${server.port}")
private int port;

```
- This will inject the value of server.port from the application.properties file into the port field.

</details>

## How to run a Spring Boot application?
<details>
<summary>Answer</summary>

- A Spring Boot application can be run in several ways:

- Using the main class: Run the main class with @SpringBootApplication using java -jar or directly from the IDE.
- Command line: Use the Spring Boot CLI to run the application using spring run.
- Maven or Gradle: You can build and run a Spring Boot application using Maven or Gradle commands, like:
  - mvn spring-boot:run
  - gradle bootRun

</details>

## What is the difference between @SpringBootApplication and @EnableAutoConfiguration?
<details>
<summary>Answer</summary>

- @SpringBootApplication: A convenience annotation that includes @Configuration, @EnableAutoConfiguration, and @ComponentScan. It is used to mark the main class that starts the Spring Boot application.
- @EnableAutoConfiguration: Tells Spring Boot to automatically configure beans based on the project's dependencies. This is one of the key annotations used in the @SpringBootApplication annotation.

</details>

##  What is the significance of @PostConstruct and @PreDestroy annotations in Spring Boot?
<details>
<summary>Answer</summary>

- @PostConstruct: Marks a method to be executed after the bean is initialized and all dependencies have been injected.
- @PreDestroy: Marks a method to be executed just before the bean is destroyed, typically for cleanup tasks.

</details>

##  What is the difference between @RestController and @Controller in Spring Boot?
<details>
<summary>Answer</summary>

- @RestController: It is a specialized version of @Controller. It is used to define REST APIs, and it automatically serializes the return object to JSON or XML, eliminating the need for @ResponseBody.

- @Controller: This is used for defining Spring MVC controllers for rendering views (like JSP or Thymeleaf). It does not automatically convert the return object to JSON or XML. For that, you need to use @ResponseBody.

</details>

## What is the purpose of the spring-boot-starter-web dependency?
<details>
<summary>Answer</summary>

-  The spring-boot-starter-web is a Spring Boot starter dependency that includes everything required to build a web application, including:
  - Spring MVC for building web applications
  - Embedded Tomcat server (by default) for serving the application
  - JSON converters for RESTful APIs
  - Spring's @RestController, @RequestMapping, and related annotations for request mapping

By including this dependency, Spring Boot will automatically configure all the necessary components to build and run a web application.

</details>

## What is the role of @ConfigurationProperties in Spring Boot?
<details>
<summary>Answer</summary>

-  @ConfigurationProperties is used in Spring Boot to bind external configuration properties (like those in application.properties or application.yml) to a Java bean. 
- It allows you to group related properties and access them in a strongly-typed manner.

Example:
```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
    private String version;

    // Getters and setters
}

```

In application.properties:

```properties
app.name=MyApp
app.version=1.0.0

```

The AppConfig class will be automatically populated with the values from application.properties.

</details>

## What is Spring Boot DevTools and what are its benefits?
<details>
<summary>Answer</summary>

- Spring Boot DevTools is a set of tools that can improve the development experience. Some key features of DevTools are:
  - Automatic restart: Automatically restarts the application when changes are detected in the source code (without requiring a manual restart).
  - LiveReload: Provides automatic browser refresh when the application code is updated.
  - Enhanced logging: DevTools provides more detailed logging to help developers identify issues more easily.
  - Cache disabling: Disables template caching, making it easier to work with templates during development.

To use DevTools, simply add the dependency in your pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>

```

</details>

## What is the difference between @Bean and @Component in Spring?
<details>
<summary>Answer</summary>

- @Bean: It is used to declare beans in a Java configuration class (typically in a class annotated with **@Configuration**). 
- The @Bean annotated method returns the bean instance and allows you to configure the bean before it is registered in the Spring container.

Example:

```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}

```

- @Component: It is a class-level annotation that marks a class as a Spring-managed bean. Spring automatically detects and registers the class as a bean during classpath scanning.

Example:

```java
@Component
public class MyServiceImpl implements MyService {
    // Class implementation
}

```
- @Bean gives more fine-grained control, while @Component relies on component scanning and automatic registration.

</details>

## What is the difference between @Autowired and @Inject?
<details>
<summary>Answer</summary>

- @Autowired: It is the Spring-specific annotation used to inject beans into a class. It can be used on fields, constructors, or setter methods.
- @Inject: This is a standard Java annotation (part of the JSR-330) that works similarly to @Autowired but is not Spring-specific. Spring supports @Inject as an alternative to @Autowired.

The key difference is that @Autowired has some additional features specific to Spring, like required (to indicate whether the dependency is mandatory), which @Inject lacks.

</details>

## What are Spring Profiles?
<details>
<summary>Answer</summary>

- Spring Profiles allow you to define different configurations for different environments (e.g., development, testing, production).
- Profiles can be activated using the application.properties or application.yml file, and you can specify beans or configurations that should be loaded based on the active profile.

For example, to define different properties for development and production:

```properties
# application.properties
spring.profiles.active=dev

```

In application-dev.properties:

```properties
database.url=jdbc:mysql://localhost/devdb

```

In application-prod.properties:

```properties
database.url=jdbc:mysql://localhost/proddb

```
</details>

## What are Spring Boot’s main building blocks?
<details>
<summary>Answer</summary>

The main building blocks of a Spring Boot application include:
- Spring Boot Starter: Pre-configured templates for common tasks.
- Auto-configuration: Automatically configures beans based on dependencies.
- Embedded Web Server: Web servers like Tomcat are included for standalone applications.
- Spring Boot CLI: Command-line tool for rapid application development.
- Spring Boot Actuator: Monitoring and management endpoints.

</details>

## What is the purpose of the @ComponentScan annotation in Spring Boot?
<details>
<summary>Answer</summary>

- he @ComponentScan annotation is used to tell Spring where to search for annotated components (like @Component, @Service, @Repository, and @Controller). 
- It automatically detects and registers beans in the Spring container. 
- By default, @SpringBootApplication includes @ComponentScan, which scans the package of the main application class and its sub-packages.

- You can customize the base package to scan using @ComponentScan(basePackages = "com.example").
 
</details>

## Can you explain how to switch from the default Tomcat server to another embedded server like Jetty or Undertow?
<details>
<summary>Answer</summary>

**How to Switch from Tomcat to Jetty or Undertow:**
- To switch from the default Tomcat server to Jetty or Undertow in a Spring Boot application, you need to make changes to the project's dependencies.
-  Switching to Jetty:
  - Exclude the default Tomcat starter from the spring-boot-starter-web dependency.
  - Include the Jetty starter as a dependency.

```xml
<!-- Exclude the default Tomcat starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>

<!-- Include the Jetty starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>

```   

**Switching to Undertow:**
- Similarly, for Undertow, you would exclude Tomcat and include Undertow's starter:

```xml
<!-- Exclude the default Tomcat starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>

<!-- Include the Undertow starter -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-undertow</artifactId>
</dependency>

```
After adding the respective dependencies, the application will use Jetty or Undertow instead of the default Tomcat server when run.


**Programmatically Setting the Embedded Web Server:(Alternate way ...)**
You can programmatically switch to Jetty, although this is rarely necessary since modifying the pom.xml is the more common approach. Here's an example of how to configure Jetty programmatically:

```java
import org.springframework.boot.web.embedded.jetty.JettyServletWebServerFactory;
import org.springframework.boot.web.servlet.server.ServletWebServerFactory;
import org.springframework.boot.web.servlet.server.WebServerFactoryCustomizer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class WebServerConfig {

    @Bean
    public WebServerFactoryCustomizer<ServletWebServerFactory> containerCustomizer() {
        return factory -> {
            // Switch to Jetty
            if (factory instanceof JettyServletWebServerFactory) {
                JettyServletWebServerFactory jettyFactory = (JettyServletWebServerFactory) factory;
                jettyFactory.setPort(8083); // Set port for Jetty server
            }
        };
    }
}

```
- In general, switching the embedded server programmatically is less common than using the pom.xml or application.properties.

**Using Spring Boot Starters in a Custom Configuration:(alternate way..)**

Instead of modifying the pom.xml to switch to Jetty or Undertow, you can use Spring Boot's auto-configuration mechanism to exclude Tomcat and include your chosen web server in the configuration classes.

- For example, you can configure the embedded server using conditional annotations:

```java
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.web.embedded.tomcat.TomcatServletWebServerFactory;
import org.springframework.context.annotation.Configuration;

@Configuration
@EnableAutoConfiguration(exclude = { TomcatServletWebServerFactory.class })
public class CustomWebServerConfig {
    // Custom web server configuration
}

```
- This approach allows you to exclude specific configurations for Tomcat and include the server you want by adding appropriate dependencies in the pom.xml and using the @EnableAutoConfiguration annotation.

</details>


## How do you configure a Spring Boot application to use an external database?
<details>
<summary>Answer</summary>

- To configure an external database in Spring Boot, you need to specify the database connection properties in application.properties or application.yml.

Example for MySQL:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect

```
Ensure you have the necessary database driver dependency in your pom.xml:

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

```

</details>

## What is Spring Boot's @SpringBootTest annotation used for?
<details>
<summary>Answer</summary>

- @SpringBootTest is used in integration testing to load the full application context, including all beans, so you can test the behavior of the Spring Boot application in a real environment. 
- This annotation is typically used in tests that require the application context to be loaded.

Example:
```java
@SpringBootTest
public class MyApplicationTests {

    @Autowired
    private MyService myService;

    @Test
    void testServiceMethod() {
        assertThat(myService.someMethod()).isEqualTo("expected value");
    }
}

```
It can also be customized to specify a web environment (e.g., mock or real servlet container).

</details>

## What is the purpose of the @Conditional annotation in Spring Boot?
<details>
<summary>Answer</summary>

- @Conditional is used in Spring to conditionally enable or disable bean definitions based on the outcome of a particular condition at runtime. 
- This can be useful when you want to create beans only under specific conditions, such as when certain properties are set, or when a class is present on the classpath.

- It allows Spring to evaluate certain conditions before registering beans, enabling more flexible and configurable applications.

Example:

```java
@ConditionalOnProperty(name = "feature.enabled", havingValue = "true")
@Bean
public SomeFeature someFeature() {
    return new SomeFeature();
}

```
- In this example, the SomeFeature bean is only registered if the property feature.enabled=true is set in the application's configuration.

- Spring Boot has several pre-defined conditions like @ConditionalOnClass, @ConditionalOnMissingBean, @ConditionalOnProperty, etc.

</details>

## How do you disable auto-configuration for a specific class in Spring Boot?
<details>
<summary>Answer</summary>

- You can disable auto-configuration in Spring Boot by using the @EnableAutoConfiguration annotation's exclude attribute, or by using the spring.autoconfigure.exclude property in the application.
- properties or application.yml file.

Using exclude in @EnableAutoConfiguration:

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude = {DataSourceAutoConfiguration.class})
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}

```

Using application.properties:

```java
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration

```

-  This allows you to prevent certain auto-configurations from being applied. It’s particularly useful when you want to customize the application and prevent Spring Boot from automatically configuring certain beans, such as data sources or web-related components.

</details>

##  How does Spring Boot handle profile-specific configurations?
<details>
<summary>Answer</summary>

- Spring Boot supports profiles to handle environment-specific configurations, such as different properties for development, testing, and production environments.
- Profiles are defined using the @Profile annotation or via the spring.profiles.active property.

Defining profiles in @Configuration:

```java
@Configuration
@Profile("dev")
public class DevConfig {
    // Dev-specific beans
}

@Configuration
@Profile("prod")
public class ProdConfig {
    // Prod-specific beans
}

```

Setting the active profile: You can set the active profile in several ways:
- Via application.properties or application.yml:

```properties
spring.profiles.active=dev

```

- Via the command line:
```shell
java -jar myapp.jar --spring.profiles.active=dev

```

- Via environment variables:
```shell
export SPRING_PROFILES_ACTIVE=dev

```
</details>

## What is the role of @ConfigurationProperties in Spring Boot, and how is it different from @Value?
<details>
<summary>Answer</summary>

- @ConfigurationProperties is used to bind external configuration properties (e.g., from application.properties or application.yml) to a Spring bean. 
- It helps to group related properties together and makes it easier to inject complex configurations. 
- It's particularly useful for cases where you have a large set of configuration properties for a service or component.

**@ConfigurationProperties:**
- Binds a prefix of properties to a Java bean.
- It works well for grouping related properties, and Spring Boot automatically performs validation for the configuration properties.
- It is particularly useful for hierarchical property structures.

Example:
```java
@ConfigurationProperties(prefix = "server")
public class ServerConfig {
    private String host;
    private int port;
    // getters and setters
}

```

in application.yml

```yaml
server:
  host: "localhost"
  port: 8080

```

**@Value**
- Injects individual values from properties or expressions.
- Can be used to inject simple values directly into fields or method parameters.
- It's less suitable for grouping large sets of properties compared to @ConfigurationProperties.

Example:

```java
@Value("${server.host}")
private String host;

```

**Difference**
- @ConfigurationProperties is better for grouping related configuration properties and is often used for complex property structures.
- @Value is useful for injecting single values or expressions.

</details>

## What are the different scopes of beans in Spring, and how do they affect the application behavior?
<details>
<summary>Answer</summary>

- In Spring, the scope of a bean defines its lifecycle and visibility within the Spring container.
- There are several types of bean scopes in Spring, and understanding them helps in managing resources effectively, particularly when dealing with different types of objects (singleton, prototype, etc.).
- Here are the most commonly used bean scopes in Spring:

- **Singleton (Default Scope):**
  - Scope: One instance of the bean is created and shared across the entire Spring container (application context).
  - Usage: This is the default scope for beans in Spring. It’s useful when the same instance of the bean can be reused throughout the application.
  Example:
    
```java
@Component
public class MyService {
    // Singleton bean (default scope)
}

```
Behavior: The Spring container creates only one instance of the MyService bean, and this instance is injected into all other components that depend on it.

- **Prototype**
  - Scope: A new instance of the bean is created each time it is requested from the Spring container.
  - Usage: Useful for beans that maintain state and you need separate instances of the bean (e.g., for handling user-specific requests).

Example:
```java
@Scope("prototype")
@Component
public class MyPrototypeService {
    // Prototype-scoped bean
}

```
- Behavior: Spring creates a new instance of MyPrototypeService each time it is requested, so every injection of MyPrototypeService will have its own instance.

- **Request**
  - Scope: A new instance of the bean is created for each HTTP request. This scope is only valid in the context of a web application.
  - Usage: Useful for web-based applications where you need beans that should only exist for the duration of an HTTP request.

Example:
```java
@Scope("request")
@Component
public class RequestScopedService {
    // Request-scoped bean (valid only in web apps)
}

```
Behavior: A new instance of RequestScopedService will be created for each HTTP request and discarded once the request is completed.

- **Session**
  - Scope: A new instance of the bean is created for each HTTP session. This is also valid only in a web application context.
  - Usage: Useful when you need to maintain a session-specific state for a user.
Example:
```java
@Scope("session")
@Component
public class SessionScopedService {
    // Session-scoped bean (valid in web apps)
}

```
- Behavior: A new instance of SessionScopedService is created for each HTTP session, ensuring that each user has a unique instance throughout their session.

- **Application**
  - Scope: Similar to singleton but limited to the lifecycle of the web application context (in the case of web applications).
  - Usage: It is used to maintain a single instance of the bean for the entire web application lifecycle.

Example:
```java
@Scope("application")
@Component
public class ApplicationScopedService {
    // Application-scoped bean (valid in web apps)
}

```

</details>

## What is a circular dependency in Spring Boot?
<details>
<summary>Answer</summary>

-  A circular dependency in Spring occurs when two or more beans depend on each other, creating a cycle. 
- In other words, Bean A depends on Bean B, and Bean B depends on Bean A (directly or indirectly).

For example:
-  Bean A depends on Bean B
-  Bean B depends on Bean A

Spring uses Dependency Injection (DI) to manage beans, but when there is a circular reference, Spring cannot resolve which bean to instantiate first, leading to an error.

Example:

```java
@Component
public class A {
  @Autowired
  private B b; // Bean A depends on Bean B
}

@Component
public class B {
  @Autowired
  private A a; // Bean B depends on Bean A
}

```
- This will lead to a BeanCurrentlyInCreationException in Spring Boot due to the circular dependency.

</details>

## How does Spring handle circular dependencies?
<details>
<summary>Answer</summary>

- Spring handles circular dependencies using setter injection and lazy initialization.
  - By default, constructor injection cannot be used to resolve circular dependencies because Spring can't instantiate one of the beans before resolving the other.
  - However, setter injection can resolve circular dependencies because Spring can first create the beans and then inject the dependencies afterward using setters.
  - Spring can also use @Lazy injection, which delays the initialization of the dependent bean, avoiding the circular reference issue during bean creation.

</details>


## Can you give an example of a circular dependency in Spring Boot and how to fix it?
<details>
<summary>Answer</summary>

-  Sure! Here's an example of circular dependency:

**Circular Dependency Example:**

Example:

```java
@Component
public class A {
    @Autowired
    private B b;
}

@Component
public class B {
    @Autowired
    private A a;
}

```

In this case, Spring Boot cannot instantiate either A or B because each one depends on the other.

**Solution 1: Use Setter Injection:**

```java
@Component
public class A {
    private B b;

    @Autowired
    public void setB(B b) {
        this.b = b;
    }
}

@Component
public class B {
    private A a;

    @Autowired
    public void setA(A a) {
        this.a = a;
    }
}

```

Here, Spring can first create both beans and then inject the dependencies through the setters.

**Solution 2: Use @Lazy Injection:**
Example:
```java
@Component
public class A {
    @Autowired
    @Lazy
    private B b;
}

@Component
public class B {
    @Autowired
    @Lazy
    private A a;
}

```

- Using @Lazy ensures that Spring only initializes the dependent bean when it is actually needed, avoiding the circular dependency problem during bean creation.

</details>

## What types of dependencies can cause circular dependencies in Spring?
<details>
<summary>Answer</summary>

- Circular dependencies can occur in any of the following scenarios:
  - Constructor Injection: When two beans are injected into each other via constructors.
  - Field Injection: When two beans reference each other via fields annotated with @Autowired.
  - Setter Injection: Although setter injection can resolve circular dependencies, if not properly handled, it could still create a circular dependency issue.

For example, when using constructor injection:


```java
@Component
public class A {
    private B b;

    @Autowired
    public A(B b) {
        this.b = b;
    }
}

@Component
public class B {
    private A a;

    @Autowired
    public B(A a) {
        this.a = a;
    }
}

```
In this case, Spring will not be able to resolve the dependencies because it needs to create A and B simultaneously, causing a circular reference.

</details>

## What happens if you don't resolve a circular dependency in Spring Boot?
<details>
<summary>Answer</summary>

- If a circular dependency is not resolved, Spring will throw an exception when trying to create the application context. Specifically, you'll encounter the following exception:
 
```text
org.springframework.beans.factory.BeanCreationException: 
Error creating bean with name 'beanName': 
Requested bean is currently in creation: Is there an unresolvable circular reference?
```

This means Spring could not resolve the dependency chain, as both beans are waiting for each other to be created, leading to an infinite loop during bean instantiation.

</details>

## What is the @Lookup annotation in Spring Boot?
<details>
<summary>Answer</summary>

- The @Lookup annotation in Spring is used to inject a prototype-scoped bean into a singleton-scoped bean. 
- It allows the Spring container to inject a new instance of the prototype bean each time the lookup method is called, even when the containing bean is a singleton.

- In simple terms, @Lookup helps you break the limitation that a singleton bean can only inject other singleton beans (i.e., it resolves the issue of injecting prototype beans into singleton beans).
- Spring uses @Lookup to create a dynamic method that calls the prototype bean lookup at runtime.

Example:
```java
@Component
public class SingletonBean {

    @Lookup
    public PrototypeBean getPrototypeBean() {
        return null; // Spring will override this method to return the actual prototype bean.
    }
}

```
- In the above example, SingletonBean is a singleton bean, and PrototypeBean is a prototype-scoped bean. Each time the getPrototypeBean() method is called, Spring will provide a new instance of PrototypeBean.

</details>

## When should you use @Lookup in Spring Boot?
<details>
<summary>Answer</summary>

- @Lookup is primarily used when you need to inject a prototype bean into a singleton bean and you want a new instance of the prototype bean every time the lookup method is called.

- This is typically needed in scenarios where you:
  - Need to create multiple instances of a prototype bean within a singleton-scoped bean.
  - Want to avoid explicitly handling the prototype bean creation via ObjectFactory or ApplicationContext.
  - Don't want to directly manage the lifecycle of the prototype bean but need a fresh instance each time.

- For example, if you're building a scenario where a singleton service needs to fetch new instances of a prototype service or object, @Lookup can be a simple and effective way to handle it.

</details>


## Can @Lookup be used with other types of beans besides prototype-scoped beans?
<details>
<summary>Answer</summary>

-  **No**, the primary use of @Lookup is to inject prototype-scoped beans into singleton-scoped beans. 
- This is because @Lookup is designed to retrieve a new instance of the prototype bean each time it’s invoked. 
- For other bean scopes (such as singleton or request), Spring's standard injection mechanisms (like @Autowired) suffice, and @Lookup is unnecessary.

- However, @Lookup can technically work with any bean type, but it is typically only useful with prototype beans to handle their dynamic creation inside singleton beans.

</details>

## Can you demonstrate the behavior of @PostConstruct with a prototype-scoped bean?
<details>
<summary>Answer</summary>

- Here's an example that demonstrates how @PostConstruct behaves with prototype-scoped beans.

Example:
```java
@Component
@Scope("prototype")
public class PrototypeBean {

    @PostConstruct
    public void init() {
        System.out.println("PrototypeBean initialized");
    }
}

@Component
public class SingletonBean {

    @Autowired
    private ApplicationContext context;

    public void createPrototypeBean() {
        PrototypeBean prototypeBean1 = context.getBean(PrototypeBean.class);
        PrototypeBean prototypeBean2 = context.getBean(PrototypeBean.class);
    }
}

```

In this example:
- PrototypeBean has the @PostConstruct annotation, and its init() method is called only once when the first instance of PrototypeBean is created.
- Even though SingletonBean calls context.getBean(PrototypeBean.class) twice, the init() method of PrototypeBean will only print "PrototypeBean initialized" once.

Output:

```text
PrototypeBean initialized

```

- This is because Spring only invokes @PostConstruct once for the first instance of the prototype bean.

</details>

## Can you explain the different types of Dependency Injection in Spring Boot and how they work, especially focusing on @Autowired, constructor injection, and method-level injection? What is the order of execution for these injections in Spring Boot?
<details>
<summary>Answer</summary>

**Dependency Injection in Spring Boot**
- Spring Boot uses Dependency Injection (DI) to manage beans, promoting loose coupling between components and making the system more maintainable and testable. Spring provides several ways to inject dependencies into beans:
  - Constructor Injection
  - Setter (Method) Injection
  - Field Injection (@Autowired)

**Let’s explore each type in detail:**

**1. Constructor Injection**

Constructor injection is the most recommended approach in Spring. In this type, the required dependencies are provided via the constructor of the class.

How it works:
- Spring automatically calls the constructor of the class and injects the required dependencies into it.
- The constructor is called when the bean is created, and the dependencies are passed at the time of instantiation.

Example:
```text
@Service
public class MyService {
    private final MyRepository myRepository;

    // Constructor Injection
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }

    public void performAction() {
        myRepository.doSomething();
    }
}

```

**2. Setter (Method) Injection**

In setter injection, Spring calls the setter method of the class after the bean has been instantiated to inject the dependencies.

**How it works:**
- Spring creates the bean first, then injects the dependency by calling the setter method.
- The setter method must be annotated with @Autowired.

Example:
```java
@Service
public class MyService {
    private MyRepository myRepository;

    // Setter Injection
    @Autowired
    public void setMyRepository(MyRepository myRepository) {
        this.myRepository = myRepository;
    }

    public void performAction() {
        myRepository.doSomething();
    }
}

```

**3. Field Injection (@Autowired)**

Field injection is the simplest form of DI. With this type, Spring automatically injects dependencies directly into the fields using @Autowired.

How it works:
- Spring uses reflection to inject dependencies into private fields. No setter or constructor is required.
- It is the least explicit approach but can be convenient for quick development.

Example:
```java
@Service
public class MyService {
    @Autowired
    private MyRepository myRepository;  // Field Injection

    public void performAction() {
        myRepository.doSomething();
    }
}


```

**Order of Execution:**

When Spring Boot initializes a bean, the order of dependency injection depends on how the injection is performed:

**Constructor Injection:**
  - Constructor injection is the first to execute. When Spring creates the bean, it will resolve all dependencies by calling the constructor, and all required dependencies will be passed in immediately when the bean is created.
  - Order of execution: During the instantiation phase of the bean lifecycle.

**Setter Injection (Method-level Injection):**
  - Setter injection is executed after the bean is instantiated. After Spring creates the bean, it then looks for @Autowired annotations on setter methods and injects the dependencies at this stage.
  - Order of execution: After the bean instantiation and before the bean is ready for use.

**Field Injection (@Autowired):**
  - Field injection happens last. Spring will inject dependencies after the bean is created and the setter methods are executed, by directly setting the fields using reflection.
  - Order of execution: After the constructor and setter injections.

</details>


## What is the purpose of the @Primary annotation in Spring?
<details>
<summary>Answer</summary>

- The @Primary annotation is used in Spring to resolve conflicts when there are multiple beans of the same type. 
- It is used to indicate which bean should be injected by default when there are multiple candidates of the same type in the Spring container.

- When multiple beans of the same type are available, Spring will choose the bean marked with @Primary for injection unless a specific bean is specified using @Qualifier.

Example:

```java
@Bean
@Primary
public Car teslaCar() {
    return new Tesla();
}

@Bean
public Car bmwCar() {
    return new BMW();
}

```
- In the above example, @Primary ensures that the teslaCar bean is injected by default, unless explicitly specified.

</details>

## How does Spring decide which bean to inject when multiple beans of the same type are present, and @Primary is not used?
<details>
<summary>Answer</summary>

- If there are multiple beans of the same type and @Primary is not used, Spring will throw an exception (NoUniqueBeanDefinitionException) because it won't be able to decide which bean to inject.
- To resolve this, you can use the @Qualifier annotation to specify which bean to inject.

Example:
```java
@Autowired
@Qualifier("bmwCar")
private Car car;

```

- In this case, @Qualifier tells Spring explicitly which bean to inject, and @Primary is not necessary.

</details>

## Can @Primary be used with @Qualifier annotations?
<details>
<summary>Answer</summary>

- Yes, @Primary and @Qualifier can be used together. 
- The @Qualifier annotation can be used to resolve conflicts when you want to inject a specific bean, even if a @Primary bean is available.

- For example, you can have multiple beans of the same type, and the @Primary bean will be injected by default unless you specify a particular one using @Qualifier.

```java
@Bean
@Primary
public Car teslaCar() {
    return new Tesla();
}

@Bean
@Qualifier("bmwCar")
public Car bmwCar() {
    return new BMW();
}

@Autowired
@Qualifier("bmwCar")
private Car car;  // Will inject the BMW car even though Tesla is marked as @Primary

```
</details>


## What is the difference between @Primary and @Qualifier annotations?
<details>
<summary>Answer</summary>

- @Primary is used to define the default bean when there are multiple candidates for injection. It helps Spring decide which bean to inject when no specific bean is mentioned.
- @Qualifier is used to specify which bean to inject when there are multiple candidates of the same type and you need to be explicit about which one to choose.

In simple terms:
- Use @Primary when you want one of the beans to be the default.
- Use @Qualifier when you want to override the default and specify a particular bean.

</details>

## Can you use @Qualifier without using @Primary?
<details>
<summary>Answer</summary>

-  Yes, @Qualifier can be used independently of @Primary. 
- @Qualifier is used to explicitly specify which bean to inject when there are multiple candidates of the same type, even if none of the beans is annotated with @Primary.

Example:
```java
@Bean
public Car teslaCar() {
    return new Tesla();
}

@Bean
public Car bmwCar() {
    return new BMW();
}

@Autowired
@Qualifier("bmwCar")
private Car car;  // Using @Qualifier to specify the bean to inject

```
- In this case, no bean is annotated with @Primary, but @Qualifier ensures that the bmwCar bean is injected.

</details>

## What happens if two beans are annotated with @Primary?
<details>
<summary>Answer</summary>

-  If two beans are annotated with @Primary, Spring will throw an exception (NoUniqueBeanDefinitionException) when trying to inject one of those beans. 
- This happens because Spring cannot decide which bean to inject, as both beans are marked as @Primary.

- To resolve this issue, you should ensure that only one bean is marked as @Primary, or use @Qualifier to explicitly specify which bean should be injected.

</details>

## How does @Primary and @Qualifier work together in a Spring Boot application?
<details>
<summary>Answer</summary>

- When both @Primary and @Qualifier are used together, @Primary marks one of the beans as the default choice, while @Qualifier is used to explicitly select a specific bean when needed.

Example:
```java
@Bean
@Primary
public Car teslaCar() {
    return new Tesla();
}

@Bean
@Qualifier("bmwCar")
public Car bmwCar() {
    return new BMW();
}

@Autowired
private Car car;  // Tesla car will be injected due to @Primary

@Autowired
@Qualifier("bmwCar")
private Car bmwCar;  // BMW car will be injected using @Qualifier

```

- In the first case, the teslaCar will be injected because it is marked with @Primary. In the second case, the bmwCar is injected because @Qualifier is explicitly used.

</details>

##  Can @Qualifier be used on constructor injection?
<details>
<summary>Answer</summary>

- Yes, @Qualifier can be used on constructor injection as well. 
- It works the same way as field injection or setter injection to specify which bean to inject when multiple beans of the same type are available.

Example:
```java
@Autowired
public CarService(@Qualifier("bmwCar") Car car) {
    this.car = car;  // The BMW car will be injected using @Qualifier
}

```
</details>


## Can I use @Qualifier with @Service or @Component annotations in Spring.
<details>
<summary>Answer</summary>

- Yes, you can use @Qualifier with @Service or @Component annotations in Spring. 
- The @Qualifier annotation is used to specify which bean to inject when there are multiple candidates of the same type, regardless of whether the beans are marked with @Component, @Service, @Repository, or @Controller.

Example 1: Using @Qualifier with @Service
```java
@Service
@Qualifier("teslaCarService")
public class TeslaCarService implements CarService {
    @Override
    public void drive() {
        System.out.println("Driving Tesla...");
    }
}

@Service
@Qualifier("bmwCarService")
public class BmwCarService implements CarService {
    @Override
    public void drive() {
        System.out.println("Driving BMW...");
    }
}

```
Now, you can use @Qualifier to specify which bean you want to inject into a class:
```java
@Component
public class CarController {

    private final CarService carService;

    @Autowired
    public CarController(@Qualifier("bmwCarService") CarService carService) {
        this.carService = carService; // BMW car service will be injected
    }

    public void driveCar() {
        carService.drive(); // Will call drive method of BMW car service
    }
}

```

Using @Qualifier with @Component

```java
@Component
@Qualifier("teslaCar")
public class TeslaCar implements Car {
    @Override
    public void drive() {
        System.out.println("Driving Tesla...");
    }
}

@Component
@Qualifier("bmwCar")
public class BmwCar implements Car {
    @Override
    public void drive() {
        System.out.println("Driving BMW...");
    }
}

```
In this example, you can inject the Car bean into another class using @Qualifier:

```java
@Component
public class CarOwner {

    private final Car car;

    @Autowired
    public CarOwner(@Qualifier("bmwCar") Car car) {
        this.car = car; // BMW car will be injected
    }

    public void driveCar() {
        car.drive(); // Will drive the BMW car
    }
}

```
</details>

## How we can customize tomcat server for total number thread, connection time out, max connection?
<details>
<summary>Answer</summary>

- In Spring Boot, you can configure the embedded Tomcat server to optimize performance, manage resources, and control request handling. 
- Spring Boot's default embedded web server is Tomcat, and it can be customized via application.properties or application.yml

```yaml
# --- Server Configuration ---
server:
  # Port where the application listens.
  port: 8080
  

 
  # Session timeout duration.
  # The session timeout configuration defines how long an HTTP session is valid before the server considers it expired.
  servlet:
    session:
      timeout: 30m

# --- SSL Configuration ---
  ssl:
    enabled: true
    key-store: classpath:keystore.jks
    key-store-password: password
    key-alias: mykey

# --- Additional Configurations ---
  tomcat:
    # Max number of connections that the server will accept.
    max-connections: 20000

    # Max number of threads for request processing.
    # This will increase the maximum number of threads from the default 200 to 400, enabling the server to handle more concurrent requests.
    max-threads: 400

    # Min number of threads to maintain.
    # This setting defines the minimum number of threads that should be maintained in the Tomcat server’s thread pool. 
    min-threads: 10

    # Connection timeout (in milliseconds).
    # The connection-timeout property sets the amount of time the server will wait for a request before closing the connection.
    connection-timeout: 20000
  
    # The queue size for incoming requests when the max connections limit is reached.
    # This setting defines how many requests will be queued before the server rejects additional incoming requests. If the max-connections limit is reached, the server will queue requests up to this accept-count value.
    accept-count: 100
  
    # Maximum size of HTTP request header (in bytes).
    # Tomcat has a default limit on the size of HTTP headers. If you need to support larger headers (for example, for OAuth tokens), you can increase this limit.
    max-http-header-size: 8192


# Disable embedded web server if needed.
web-server:
  enabled: true

```

</details>

## What is ConversionService in Spring?
<details>
<summary>Answer</summary>

- The ConversionService is a core Spring framework interface that provides the ability to convert objects from one type to another. 
- It’s a part of Spring's data binding and type conversion mechanism. 
- The service is typically used to convert request parameters to Java object types, or to convert between Java types (e.g., converting a String to a Date or Integer).

Example:

```java
import org.springframework.core.convert.converter.Converter;

public class StringToCustomObjectConverter implements Converter<String, CustomObject> {
    @Override
    public CustomObject convert(String source) {
        CustomObject customObject = new CustomObject();
        customObject.setValue(source);
        return customObject;
    }
}

```


How can we use? 

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.convert.ConversionService;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    @Autowired
    private ConversionService conversionService;

    @GetMapping("/convert")
    public String convert(@RequestParam("value") String value) {
        // Convert string to custom object using the registered converter
        CustomObject customObject = conversionService.convert(value, CustomObject.class);
        return "Converted value: " + customObject.getValue();
    }
}

```

</details>

 
## Can ConversionService be used with Spring Data JPA for entity conversion?
<details>
<summary>Answer</summary>

- Yes, ConversionService can be used with Spring Data JPA, although it's not commonly used for entity-to-entity conversion. 
- You can use it to convert DTOs (Data Transfer Objects) to JPA entities or vice versa, especially when you need to map custom fields or perform complex data transformations.

Example:
```java
import org.springframework.core.convert.ConversionService;
import org.springframework.beans.factory.annotation.Autowired;

public class MyService {

    @Autowired
    private ConversionService conversionService;

    public MyDto convertToDto(MyEntity entity) {
        return conversionService.convert(entity, MyDto.class);
    }
}

```
</details>