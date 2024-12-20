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


## Difference between `@ControllerAdvice` and `@RestControllerAdvice`

<details>
<summary>Answer</summary>

- Both `@ControllerAdvice` and `@RestControllerAdvice` are used for global exception handling in Spring applications. However, they are used in different scenarios based on the type of controller and response format.

Key Differences

| Feature                   | `@ControllerAdvice`                      | `@RestControllerAdvice`                      |
|---------------------------|------------------------------------------|---------------------------------------------|
| **Target**                 | Works with controllers that return views (HTML, JSP, etc.). | Works with REST controllers returning raw data (JSON, XML, etc.). |
| **Response Type**          | Response could be a view (HTML, JSP) or other types. | Response is always written to the response body as JSON or other formats. |
| **`@ResponseBody` Behavior**| Not automatically added; you have to use `@ResponseBody` on methods if needed. | Automatically applies `@ResponseBody` to all handler methods. |
| **Use Case**               | Global exception handling, model attributes, etc., for MVC controllers. | Global exception handling, response customization for REST APIs. |

- When to Use Which?
- **Use `@ControllerAdvice`** if you're building a **traditional Spring MVC application** that returns views (HTML, JSP, etc.) and you want global exception handling, model attributes, etc.
- **Use `@RestControllerAdvice`** if you're building a **RESTful API** where controllers return JSON or XML responses. It simplifies the creation of global exception handlers and ensures responses are automatically formatted in the desired way (usually JSON).


Summary:
- **`@ControllerAdvice`**: Ideal for traditional Spring MVC applications that deal with views, typically used for handling exceptions and adding global model attributes.
- **`@RestControllerAdvice`**: Specifically tailored for REST APIs that return JSON or similar data formats, combining the functionality of `@ControllerAdvice` with `@ResponseBody` automatically applied to all methods.

</details>
 

## Exception handling for only rest api with example.
<details>
<summary>Answer</summary>

- Steps to Implement Exception Handling with @RestControllerAdvice:
  - Create a custom exception class.
  - Define a global exception handler using @RestControllerAdvice.
  - Return a meaningful JSON response when an exception occurs.

1. Custom Exception Class
- Let's first create a custom exception class that will be used to represent errors in your application.

```java
package com.example.demo.exception;

public class ResourceNotFoundException extends RuntimeException {

    private String resourceName;
    private String fieldName;
    private Object fieldValue;

    public ResourceNotFoundException(String resourceName, String fieldName, Object fieldValue) {
        super(String.format("%s not found with %s : '%s'", resourceName, fieldName, fieldValue));
        this.resourceName = resourceName;
        this.fieldName = fieldName;
        this.fieldValue = fieldValue;
    }

    public String getResourceName() {
        return resourceName;
    }

    public String getFieldName() {
        return fieldName;
    }

    public Object getFieldValue() {
        return fieldValue;
    }
}

```
In this example, ResourceNotFoundException is a custom exception that could be used when a resource (such as a user or product) is not found by its identifier.

- 2. Define Global Exception Handler Using @RestControllerAdvice


Now, let's create a global exception handler using @RestControllerAdvice to handle this custom exception, as well as any other exceptions in the application.

```java
package com.example.demo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.HashMap;
import java.util.Map;

// This will handle exceptions globally for all @RestController classes
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<Map<String, Object>> handleResourceNotFoundException(ResourceNotFoundException ex) {
        // Prepare a response map
        Map<String, Object> response = new HashMap<>();
        response.put("message", ex.getMessage());
        response.put("resourceName", ex.getResourceName());
        response.put("fieldName", ex.getFieldName());
        response.put("fieldValue", ex.getFieldValue());

        // Return a JSON response with 404 NOT FOUND status
        return new ResponseEntity<>(response, HttpStatus.NOT_FOUND);
    }

    // Handle any other uncaught exceptions globally
    @ExceptionHandler(Exception.class)
    public ResponseEntity<Map<String, String>> handleGlobalException(Exception ex) {
        Map<String, String> response = new HashMap<>();
        response.put("message", ex.getMessage());
        response.put("details", "An unexpected error occurred.");
        
        // Return a generic error response with 500 INTERNAL SERVER ERROR status
        return new ResponseEntity<>(response, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

```

Where:
- @RestControllerAdvice: This annotation is used to define a global exception handler for all REST controllers. It acts similarly to @ControllerAdvice but is specifically designed for REST APIs.
- @ExceptionHandler: The @ExceptionHandler annotation is used to handle specific exceptions (like ResourceNotFoundException in this case). It catches the exception and sends an appropriate response.
- Response Structure: In the handler, we're returning a Map<String, Object> with the exception message and other details, and Spring Boot automatically converts it to JSON (since @RestControllerAdvice implicitly applies @ResponseBody).


finally Controller Example:
Let's create a simple controller to test this exception handling.

```java
package com.example.demo.controller;

import com.example.demo.exception.ResourceNotFoundException;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

// This is a simple REST controller that will throw an exception when a resource is not found
@RestController
public class ProductController {

  @GetMapping("/products/{id}")
  public String getProduct(@PathVariable("id") Long id) {
    // Simulate a situation where the product is not found
    if (id != 1L) {  // Suppose only the product with ID 1 exists
      throw new ResourceNotFoundException("Product", "id", id);
    }

    return "Product found";
  }
}

```
In this controller, if the id doesn't match 1L, a ResourceNotFoundException is thrown, and it will be handled by the @RestControllerAdvice class we defined earlier.

</details>

## What HTTP status code would you return when a resource is successfully created in a Spring Boot REST API?
<details>
<summary>Answer</summary>

- The appropriate HTTP status code for a successful creation of a resource is 201 Created.
- In Spring Boot, you can use ResponseEntity to return this status along with the created resource. For example:

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
  User createdUser = userService.save(user);
  return new ResponseEntity<>(createdUser, HttpStatus.CREATED);
}

```

or You can use of ResponseStatus do the same. 

```java
@PostMapping("/users")
@ResponseStatus(HttpStatus.CREATED)
public User createUser(@RequestBody User user) {
    return userService.save(user);
}
```

**When to use @ResponseStatus:**
- It's ideal when you have a straightforward operation where only the HTTP status code needs to be controlled, and you don't need any additional customization like headers or other status codes for the response body.

</details>

## What is the difference between HTTP status codes 404 Not Found and 410 Gone? When would you use each in a RESTful API?
<details>
<summary>Answer</summary>

- 404 Not Found: This indicates that the requested resource could not be found, but there is a possibility that it may exist in the future.
- 410 Gone: This indicates that the requested resource was once available but is no longer available and will not be coming back.

</details>

## How should you name the endpoint to retrieve a list of users in a Spring Boot REST API?
<details>
<summary>Answer</summary>

- According to RESTful conventions, the endpoint should be named using a plural noun to represent a collection of resources. The HTTP method GET is used to retrieve resources.
- The recommended endpoint would be GET /users.

Example:

```java
@GetMapping("/users")
public List<User> getAllUsers() {
    return userService.findAll();
}

```
</details>

## What is the correct way to define an endpoint to update a user's information in a Spring Boot REST API?
<details>
<summary>Answer</summary>

- For updating a resource, the HTTP method PUT is used, and the endpoint should include the resource identifier (e.g., user ID) in the URL path.
- The endpoint should be PUT /users/{id} where {id} is the unique identifier of the user being updated.


```java
@PutMapping("/users/{id}")
public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody User user) {
    User updatedUser = userService.update(id, user);
    return new ResponseEntity<>(updatedUser, HttpStatus.OK);
}

```
</details>

## Why should you avoid using verbs in the URL path of a RESTful API, and can you provide an example?
<details>
<summary>Answer</summary>

- The HTTP methods (GET, POST, PUT, DELETE) are the verbs that represent actions in RESTful APIs. Including verbs in the URL path is redundant, as the action is already specified by the HTTP method itself.
- Instead, the URL should describe the resource (the noun), not the action.

**Example of incorrect endpoint:**
- GET /getUsers

**Correct endpoint:**
- GET /users

</details>

## How would you handle an endpoint to delete a user in a Spring Boot REST API?
<details>
<summary>Answer</summary>

- The HTTP method DELETE should be used for deleting resources. The endpoint should specify the resource to be deleted, typically including its identifier in the URL.

- The correct endpoint would be DELETE /users/{id}, where {id} is the unique identifier for the user to be deleted.

Example:
```java
@DeleteMapping("/users/{id}")
public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
    userService.delete(id);
    return new ResponseEntity<>(HttpStatus.NO_CONTENT); // 204 No Content
}

```

OR

```java
@DeleteMapping("/users/{id}")
@ResponseStatus(HttpStatus.NO_CONTENT)
public void deleteUser(@PathVariable Long id) {
    userService.delete(id);
}
```
</details>


## What is the difference between PUT and PATCH methods in a RESTful API, and when would you use each?
<details>
<summary>Answer</summary>

- PUT is used for updating or replacing an entire resource. It is idempotent, meaning repeated requests will always result in the same outcome.
- PATCH is used for partially updating a resource. It is also idempotent, but typically only specific fields are updated, not the entire resource.

For example, for updating a user's profile:
- PUT /users/{id} would replace the entire user information with the provided data.
- PATCH /users/{id} would only update the specific fields provided (e.g., only the user’s email address).

```java
@PutMapping("/users/{id}")
public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody User user) {
    User updatedUser = userService.update(id, user);
    return new ResponseEntity<>(updatedUser, HttpStatus.OK);
}

@PatchMapping("/users/{id}")
public ResponseEntity<User> partialUpdateUser(@PathVariable Long id, @RequestBody Map<String, Object> updates) {
    User updatedUser = userService.partialUpdate(id, updates);
    return new ResponseEntity<>(updatedUser, HttpStatus.OK);
}

```

</details>

## Common http request status code?
<details>
<summary>Answer</summary>



| **Status Code** | **Description** | **Use Case** |
|-----------------|-----------------|--------------|
| **200 OK** | The request was successful and the server has returned the requested data (for `GET`) or the action has been completed (for `POST`, `PUT`, etc.). | Successful `GET` request, resource successfully updated or created. |
| **201 Created** | The request has been fulfilled, and a new resource has been created. | A new resource has been created, like a new user or item in a database. |
| **204 No Content** | The request was successful, but there is no content to return in the response body. | `DELETE` or `PUT` requests where no content is returned. |
| **400 Bad Request** | The server could not understand the request due to invalid syntax or malformed request data. | Invalid input, missing parameters, or incorrect data format in the request body. |
| **401 Unauthorized** | The request lacks valid authentication credentials or the provided credentials are invalid. | The user is not logged in or their credentials are invalid. |
| **403 Forbidden** | The server understands the request but refuses to authorize it. The user is authenticated but does not have permission to access the resource. | A logged-in user trying to access a resource they do not have permissions for (e.g., admin-only page). |
| **404 Not Found** | The server could not find the requested resource. | The client requests a resource (e.g., user profile or article) that doesn't exist. |
| **405 Method Not Allowed** | The method specified in the request (e.g., `POST`, `GET`, `PUT`) is not allowed for the resource identified by the URL. | Trying to use `GET` on a resource that only supports `POST`, or vice versa. |
| **408 Request Timeout** | The server timed out waiting for the request. This happens when the client takes too long to send data. | The client fails to send a request within the time frame allowed by the server. |
| **429 Too Many Requests** | The client has sent too many requests in a given period of time. | The user has exceeded the rate limit set for API requests. |
| **500 Internal Server Error** | The server encountered an unexpected condition that prevented it from fulfilling the request. | The server crashes or encounters an unexpected exception while processing the request. |
| **502 Bad Gateway** | The server, while acting as a gateway or proxy, received an invalid response from the upstream server. | A proxy server or gateway (e.g., a load balancer) could not retrieve data from the actual server. |
| **503 Service Unavailable** | The server is temporarily unable to handle the request due to overloading or maintenance. | The server is temporarily down for maintenance or overloaded with requests. |
| **504 Gateway Timeout** | The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server it needed to access in order to complete the request. | The server times out waiting for a response from another server or service it relies on. |
| **505 HTTP Version Not Supported** | The server does not support the HTTP protocol version that was used in the request. | The client uses an outdated or unsupported HTTP version. |
| **410 Gone** | The resource requested is no longer available and will not be available again. This is a permanent condition. | A resource that used to exist but has been intentionally removed and will not be brought back (e.g., a deprecated API endpoint). |
| **415 Unsupported Media Type** | The server refuses to process the request because the format of the data in the request body is not supported. | The client sends a `POST` or `PUT` request with an unsupported content type (e.g., sending `text/xml` when the server expects `application/json`). |
| **418 I'm a teapot** | This is a joke status code defined in RFC 2324. It is returned by an HTTP teapot when asked to brew coffee. | Not used in real-world applications but mentioned humorously in some contexts. |
| **422 Unprocessable Entity** | The server understands the content type of the request, but the request cannot be processed due to semantic errors (e.g., validation errors). | A form submission where the data is syntactically correct but fails validation (e.g., invalid email format). |
| **426 Upgrade Required** | The client should switch to a different protocol, such as HTTP/2, to proceed with the request. | The server requires the client to upgrade to a more recent protocol version. |
| **301 Moved Permanently** | The requested resource has been permanently moved to a new URL. | Typically used for permanent URL redirection (e.g., when an API endpoint is permanently relocated). |
| **302 Found (Previously "Moved Temporarily")** | The requested resource has been temporarily moved to a different URL. | OAuth 2.0 Authorization Code Flow: A redirect to the authorization server for authentication. |
| **303 See Other** | The server is redirecting the client to a different resource, usually after a `POST` request. | In OAuth 2.0, used after authorization to redirect the client to the token endpoint with a code. |
| **307 Temporary Redirect** | The requested resource resides temporarily under a different URL. | Temporary redirects, commonly used for OAuth 2.0 authentication flows, where a user is redirected back to the client after login. |
| **308 Permanent Redirect** | The requested resource has been permanently moved to a new URL, and future requests should be directed to that URL. | Similar to `301`, but the method and body of the original request are preserved during the redirect. |


</details>