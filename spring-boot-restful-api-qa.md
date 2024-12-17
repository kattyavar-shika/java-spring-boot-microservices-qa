# Spring Boot Restful API Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)

## What is a RESTful API, and what are its key principles?
<details>
<summary>Answer</summary>

- A RESTful API (Representational State Transfer) is an architectural style for building web services that are lightweight, stateless, and can communicate over HTTP. 
- The key principles of RESTful APIs include:
  - Statelessness: Every request from the client to the server must contain all the information needed to understand and process the request. The server should not store anything about the client's state between requests.
  - Client-Server Architecture: The client and server operate independently. The client is responsible for the user interface, while the server manages data storage and logic.
  - Uniform Interface: A consistent and standardized way of interacting with resources, typically through HTTP methods (GET, POST, PUT, DELETE).
  - Representation: Resources (data entities) are represented in a format like JSON or XML.
  - Cacheability: Responses must explicitly define if they are cacheable or not, helping improve performance.
  - Layered System: A system can be composed of multiple layers, each responsible for a different aspect, such as security, load balancing, etc.

</details>

##  How does Spring Boot support the development of RESTful APIs?
<details>
<summary>Answer</summary>

- Spring Boot simplifies the development of RESTful APIs by providing a pre-configured environment with the following features:
  - Embedded Servers: Spring Boot supports embedded web servers like Tomcat, Jetty, and Undertow, so you don't need to configure an external server for running your APIs.
  - Spring Web Dependency: The spring-boot-starter-web dependency includes all the necessary libraries (like Spring MVC, Jackson, etc.) for building RESTful APIs.
  - Simplified Configuration: Spring Boot offers default configurations, reducing boilerplate code and setup.
  - REST Annotations: Annotations such as @RestController, @RequestMapping, @GetMapping, @PostMapping, etc., make it easy to define routes and map HTTP methods to Java methods.
  - Automatic JSON/XML Conversion: With Spring Boot, response objects are automatically converted to JSON (or XML) using libraries like Jackson, eliminating the need for manual serialization.
  - Built-in Error Handling: Spring Boot provides comprehensive error handling and exception handling using @ControllerAdvice or @ExceptionHandler.

</details>

## What is the purpose of @RestController annotation in Spring Boot?
<details>
<summary>Answer</summary>

- @RestController is a convenience annotation in Spring Boot that combines @Controller and @ResponseBody. 
- It indicates that the class is a RESTful web service controller, where methods will return data directly to the client (usually in JSON format) instead of rendering a view.

- @Controller is used to mark a class as a Spring MVC controller that can handle HTTP requests.
- @ResponseBody tells Spring that the return value of methods should be serialized directly into the HTTP response body.


- Using @RestController simplifies the development of REST APIs, as you don't need to manually annotate each method with @ResponseBody.

Example:

```java
@RestController
@RequestMapping("/api/products")
public class ProductController {
    @GetMapping
    public List<Product> getAllProducts() {
        return productService.getAllProducts();
    }
}

```
</details>

## What is the difference between @GetMapping, @PostMapping, @PutMapping, @PatchMapping and @DeleteMapping?
<details>
<summary>Answer</summary>

- These are convenience annotations in Spring Boot that map HTTP requests to Java methods for CRUD (Create, Read, Update, Delete) operations:

- @GetMapping: Used to handle HTTP GET requests. It is typically used for retrieving resources or data.

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userService.getUser(id);
}

```

- @PostMapping: Used to handle HTTP POST requests. It is typically used for creating new resources.

```java
@PostMapping("/users")
public User createUser(@RequestBody User user) {
    return userService.createUser(user);
}

```

- @PutMapping: Used to handle HTTP PUT requests. It is typically used for updating an existing resource.

```java
@PutMapping("/users/{id}")
public User updateUser(@PathVariable Long id, @RequestBody User user) {
    return userService.updateUser(id, user);
}

```

- @DeleteMapping: Used to handle HTTP DELETE requests. It is typically used for deleting resources.

```java
@DeleteMapping("/users/{id}")
public void deleteUser(@PathVariable Long id) {
    userService.deleteUser(id);
}

```

- @PatchMapping is used to handle HTTP PATCH requests, which are used for partial updates to an existing resource. This means you are sending a request with only the data that needs to be modified, not the entire resource.

```java
@PatchMapping("/users/{id}")
public User updateUser(@PathVariable Long id, @RequestBody Map<String, Object> updates) {
    return userService.updateUser(id, updates);  // Only update the fields sent in the request
}

```

</details>

##  Explain the role of @RequestMapping in Spring Boot.
<details>
<summary>Answer</summary>

- @RequestMapping is a versatile annotation used to map HTTP requests to Java methods in a controller. 
- It can be used to specify the HTTP method (GET, POST, PUT, DELETE, etc.), the URL path, and additional parameters such as headers or request parameters.

```java
@RequestMapping(value = "/users", method = RequestMethod.GET)
public List<User> getUsers() {
    return userService.getAllUsers();
}

```

- While @RequestMapping is powerful, Spring 4 introduced more specialized annotations like @GetMapping, @PostMapping, etc., to make code more readable and concise.

</details>

## What is @PathVariable and when do you use it in Spring Boot?
<details>
<summary>Answer</summary>

- @PathVariable is used to extract values from the URI path in a RESTful API request.
- It is commonly used in dynamic URLs to map parts of the URL to method parameters.

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userService.getUser(id);
}

```

- In the above example, id is a path variable, and the value for id will be extracted from the URL.

</details>

## What is @RequestBody in Spring Boot?
<details>
<summary>Answer</summary>

- @RequestBody is used to bind the incoming HTTP request body to a method parameter in a Spring controller. 
- It's typically used for HTTP methods like POST and PUT, where you send data to the server in the request body (e.g., JSON, XML).

```java
@PostMapping("/users")
public User createUser(@RequestBody User user) {
    return userService.createUser(user);
}

```

- In this case, the user object is populated with the data from the request body, usually in JSON format, and passed to the method.

</details>


## How do you handle exceptions globally in a Spring Boot REST API?
<details>
<summary>Answer</summary>

-  In Spring Boot, you can handle exceptions globally using @ControllerAdvice or @ExceptionHandler. 
- This approach allows you to centralize the error-handling logic, making your API more consistent.

Example using @ControllerAdvice:

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleResourceNotFound(ResourceNotFoundException ex) {
        ErrorResponse errorResponse = new ErrorResponse("Resource not found", ex.getMessage());
        return new ResponseEntity<>(errorResponse, HttpStatus.NOT_FOUND);
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGenericException(Exception ex) {
        ErrorResponse errorResponse = new ErrorResponse("Internal server error", ex.getMessage());
        return new ResponseEntity<>(errorResponse, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

```

- In this example, exceptions are handled globally, and an appropriate error response is returned.

</details>


## What is Spring Boot Actuator and how does it help in building RESTful APIs?
<details>
<summary>Answer</summary>

- Spring Boot Actuator is a set of built-in production-ready features that help monitor and manage Spring Boot applications. 
- It provides endpoints that can be used to get details about your application's health, metrics, environment, and other useful information.
- Some commonly used actuator endpoints:
  - /actuator/health: Provides the health status of your application.
  - /actuator/metrics: Provides metrics about the application (e.g., memory usage, active threads).
  - /actuator/env: Shows environment properties.

To enable Actuator, you can add the dependency spring-boot-starter-actuator to your pom.xml or build.gradle.

</details>

## Diff between PATCH And PUT request.
<details>
<summary>Answer</summary>

| **Aspect**           | **PUT** (`@PutMapping`)                               | **PATCH** (`@PatchMapping`)                              |
|----------------------|-------------------------------------------------------|---------------------------------------------------------|
| **Purpose**           | Update the entire resource (complete replacement)      | Update part of the resource (partial update)             |
| **Request Body**      | The client sends the full updated resource (overwrites the existing one) | The client sends only the fields that need to be updated |
| **Idempotency**       | Idempotent (same request gives the same result)        | Not necessarily idempotent (depending on the implementation) |
| **Use Case**          | Use when the entire resource is being updated (e.g., updating all fields of a `User`) | Use when only a part of the resource needs to be updated (e.g., updating a `User`'s `email`) |
| **Example**           | Replacing the whole user object with a new one         | Updating just the `email` field of a user object        |


</details>

## What is the difference between @RequestParam and @PathVariable in Spring Boot?
<details>
<summary>Answer</summary>

- @RequestParam is used to extract query parameters from the URL, typically for optional parameters. It is often used in cases where the parameters are part of the query string (e.g., ?name=John&age=30).

```java
@GetMapping("/users")
public List<User> getUsers(@RequestParam String name, @RequestParam int age) {
    return userService.getUsersByNameAndAge(name, age);
}

```
URL: /users?name=John&age=30

- @PathVariable is used to extract variables from the URI path. It is typically used when the parameter is part of the URL itself, not as a query string.

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userService.getUserById(id);
}

```
URL: /users/1

</details>


## What is the purpose of @ResponseStatus in Spring Boot?
<details>
<summary>Answer</summary>

- The @ResponseStatus annotation is used to set the HTTP status code for a response. 
- It can be applied to a controller method or exception handler to indicate the status code that should be returned with the response.

For controller methods: You can use it to set a default response status for a method.

```java
@ResponseStatus(HttpStatus.CREATED)
@PostMapping("/users")
public User createUser(@RequestBody User user) {
    return userService.createUser(user);
}

```

- For exception handling: It can be used on custom exceptions to indicate the HTTP status code that should be returned when the exception is thrown.

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

```
- In this example, when a ResourceNotFoundException is thrown, Spring will automatically return a 404 Not Found response.

</details>

## How can you handle pagination in a Spring Boot REST API?
<details>
<summary>Answer</summary>

- Spring Data provides a very easy way to implement pagination with the Pageable interface. 
- It allows you to retrieve a subset of results from a potentially large dataset in a RESTful API.

Here’s how you can implement pagination:

- Controller Layer: You can accept Pageable as a parameter in your controller method, which Spring will automatically convert from query parameters (e.g., page, size).

```java
@GetMapping("/users")
public Page<User> getUsers(Pageable pageable) {
    return userService.getUsers(pageable);
}

```

- Service Layer: In the service layer, you can pass the Pageable object to a repository that extends PagingAndSortingRepository.

```java
public Page<User> getUsers(Pageable pageable) {
    return userRepository.findAll(pageable);
}

```

Request: For pagination, clients can make a request with query parameters like ?page=0&size=10 to get the first 10 users.

</details>


## What are @RequestHeader and @CookieValue used for in Spring Boot?
<details>
<summary>Answer</summary>

- @RequestHeader: This annotation is used to bind HTTP request headers to method parameters in a controller. You can use it to access any custom header passed in the HTTP request.

Example:

```java
@GetMapping("/users")
public List<User> getUsers(@RequestHeader("Authorization") String authorizationToken) {
    return userService.getUsers(authorizationToken);
}

```
In this example, the Authorization header is extracted and passed to the method.

- @CookieValue: This annotation is used to bind cookie values to method parameters. It is useful when you need to access cookies sent by the client.

```java
@GetMapping("/dashboard")
public String getDashboard(@CookieValue("user_id") String userId) {
    return dashboardService.getDashboard(userId);
}

```

- In this example, the user_id cookie value is extracted and passed to the method.

</details>

##  What is the difference between @Valid and @Validated in Spring Boot?
<details>
<summary>Answer</summary>

- @Valid: It is a Java Bean validation annotation used to validate the properties of a class. 
- It is provided by the JSR-303 (Bean Validation) specification, and it is typically used on method parameters, fields, or class-level annotations.

Example:
```java
@PostMapping("/users")
public User createUser(@Valid @RequestBody User user) {
    return userService.createUser(user);
}

```

- @Validated: It is a Spring-specific annotation that extends @Valid but allows for the use of validation groups. 
- It can be used to validate different groups of constraints, which is particularly useful in cases where you have different validation requirements for different scenarios.


```java
@PostMapping("/users")
public User createUser(@Validated(Create.class) @RequestBody User user) {
    return userService.createUser(user);
}

```

**In summary:**
- @Valid is part of the JSR-303 specification and is often used for simple validation.
- @Validated allows for more advanced validation capabilities, such as validation groups.

</details>


## What are Validation Groups?
<details>
<summary>Answer</summary>

- Validation Groups are used to validate subsets of constraints on a class. You can define groups like Create, Update, Delete, and apply them to specific validation rules on an entity.
- This is especially useful when you have different requirements for the same object in different scenarios. For example:
- When creating a new user, you may want to ensure the name field is not null.
- When updating a user, you may not need to check the name field, but you might want to validate the email field.

**How does @Validated work with validation groups?**

- To use validation groups, you first define group interfaces, then specify those groups on the relevant constraints. For instance:

```java
public interface Create { }
public interface Update { }

```

- Then, in your entity class (e.g., User), you can apply different validation groups like this:

```java
public class User {

    @NotNull(groups = Create.class)
    private String name;

    @Email(groups = {Create.class, Update.class})
    private String email;

    // other fields, getters, setters...
}

```
In the above example:
- The name field is validated only in the context of Create operations.
- The email field is validated in both Create and Update operations.

Using @Validated with Validation Groups in Controllers
Now, when you use @Validated in your controller, you can specify the validation group to apply:
 
```java
@PostMapping("/users")
public User createUser(@Validated(Create.class) @RequestBody User user) {
    return userService.createUser(user);  // This will validate the user according to the 'Create' group
}

@PutMapping("/users/{id}")
public User updateUser(@Validated(Update.class) @RequestBody User user) {
    return userService.updateUser(user);  // This will validate the user according to the 'Update' group
}

```

In the above example:
- The createUser method triggers validation of the User object according to the Create validation group.
- The updateUser method triggers validation according to the Update validation group.


**Summary **
- @Validated: Provides more advanced validation options, especially when working with validation groups. It allows you to apply different validation rules based on the operation or scenario.
- @Valid: Used for simple validation with no group differentiation. All validation constraints are checked.

```java
@PutMapping("/users/{id}")
public User updateUser(@Validated @RequestBody User user) {
    return userService.updateUser(user);
}

```

- - In this case, @Validated is applied to the user object. Since no specific validation group is passed, it will validate all constraints on the User object (similar to @Valid).

</details>

## What are the different HTTP methods used in RESTful APIs?
<details>
<summary>Answer</summary>

- The most commonly used HTTP methods in RESTful APIs are:
  - GET: Retrieves data from the server (read-only, no side effects).
  - POST: Submits data to the server (used for creating resources).
  - PUT: Updates a resource with the data provided (typically used for full updates).
  - PATCH: Partially updates a resource (only updates the fields provided).
  - DELETE: Removes a resource from the server.
  - HEAD: Similar to GET but only retrieves the headers, not the body.
  - OPTIONS: Describes the communication options for the target resource (like allowed HTTP methods).

</details>


## What are Spring Boot Profiles, and how can they be used to configure different environments (e.g., development, production)?
<details>
<summary>Answer</summary>

- Spring Boot Profiles are used to define different configuration settings for different environments. 
- A profile is a way to isolate configuration properties and beans for different environments, like dev, prod, or test.
- Spring Boot allows you to specify which profile is active using the spring.profiles.active property.

- To specify the active profile, you can either:
```properties
spring.profiles.active=dev

```
Or specify it as a command-line argument:

```shell
java -jar myapp.jar --spring.profiles.active=prod

```
</details>


## What is the difference between @RestController and @Controller in Spring Boot?
<details>
<summary>Answer</summary>

- @Controller: A traditional Spring annotation used for web applications that returns views (HTML, JSP, etc.). It is typically used with @ResponseBody to return JSON or XML, but it is not automatically included.

```java
@Controller
public class UserController {
    @RequestMapping("/users")
    public String getUsers(Model model) {
        model.addAttribute("users", userService.getUsers());
        return "usersView"; // returns a view name (e.g., users.jsp)
    }
}

```

- @RestController: A convenience annotation that combines @Controller and @ResponseBody. It is used in RESTful APIs, and all methods in a @RestController are implicitly annotated with @ResponseBody, meaning that the return values are directly written to the HTTP response body (usually in JSON format).

```java
@RestController
public class UserController {
    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.getUsers();
    }
}

```

**In summary:**
- @Controller is for traditional web applications.
- @RestController is for REST APIs, where the data is directly returned in the response body.

</details>


## What is the use of @CrossOrigin in Spring Boot?
<details>
<summary>Answer</summary>

-  @CrossOrigin is an annotation in Spring Boot that enables Cross-Origin Resource Sharing (CORS) support for your RESTful APIs. 
- CORS is a mechanism that allows web browsers to make requests to domains other than the one that served the original web page.

- By default, web browsers block such cross-origin requests for security reasons. 
- The @CrossOrigin annotation enables you to specify which domains can access your REST API and what HTTP methods are allowed.

```java
@RestController
@CrossOrigin(origins = "http://example.com")
public class UserController {
    
    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.getUsers();
    }
}

```
- In this example, the @CrossOrigin annotation allows requests from http://example.com to access the /users endpoint.

</details>

##  What is the role of @RequestParam in Spring Boot?
<details>
<summary>Answer</summary>

- @RequestParam is used to extract query parameters from the URL of an HTTP request. 
- These parameters are typically sent in the URL after the ? symbol, and can be used to filter or modify the behavior of your API.

```java
@GetMapping("/users")
public List<User> getUsers(@RequestParam(required = false) String name, 
                           @RequestParam(defaultValue = "0") int page) {
    return userService.findUsersByName(name, page);
}

```

Here:
- If the URL is /users?name=John&page=2, the name and page parameters will be extracted and passed to the getUsers method.
- required = false makes the query parameter optional.
- defaultValue specifies a default value if the parameter is not provided in the request.

</details>


## How can you implement versioning in a Spring Boot REST API?
<details>
<summary>Answer</summary>

- Versioning is important when your API evolves, but you want to ensure that clients using older versions are not broken. 
- Spring Boot supports multiple ways to implement versioning for RESTful APIs:

- URI Path Versioning: The most common method of versioning an API is by including the version number in the URL path.

```java
@GetMapping("/v1/users")
public List<User> getUsersV1() {
    return userService.getAllUsers();
}

@GetMapping("/v2/users")
public List<User> getUsersV2() {
    return userService.getAllUsersV2();
}

```

- Request Parameter Versioning: You can pass the version in the query parameters.

```java
@GetMapping("/users")
public List<User> getUsers(@RequestParam(value = "version", defaultValue = "1") int version) {
    if (version == 1) {
        return userService.getAllUsersV1();
    } else {
        return userService.getAllUsersV2();
    }
}

```

- Header Versioning: You can specify the version in the request header.

```java
@GetMapping("/users")
public List<User> getUsers(@RequestHeader(value = "API-Version", defaultValue = "1") int version) {
    if (version == 1) {
        return userService.getAllUsersV1();
    } else {
        return userService.getAllUsersV2();
    }
}

```
</details>

## What is HATEOAS in RESTful APIs, and how does Spring Boot support it?
<details>
<summary>Answer</summary>

- HATEOAS (Hypermedia As The Engine Of Application State) is a constraint of REST that suggests that, along with the data, the API should provide related actions (links) that a client can follow. 
- These links guide the client on what actions can be performed next, creating a more dynamic and discoverable API.
- In Spring Boot, Spring HATEOAS is a library that provides support for adding hypermedia links to RESTful responses. 
- It helps build APIs where each response contains links to related resources, making it easier for clients to navigate through the API.

```java
@GetMapping("/users/{id}")
public Resource<User> getUser(@PathVariable Long id) {
    User user = userService.getUser(id);
    Resource<User> resource = new Resource<>(user);

    resource.add(linkTo(methodOn(UserController.class).getUser(id)).withSelfRel());
    resource.add(linkTo(methodOn(UserController.class).getAllUsers()).withRel("all-users"));
    
    return resource;
}

```
- In the above example:
  - linkTo(methodOn(...)) is used to create hypermedia links.
  - withSelfRel() adds a link to the resource itself.
  - withRel("all-users") adds a link to get all users.

</details>


 









