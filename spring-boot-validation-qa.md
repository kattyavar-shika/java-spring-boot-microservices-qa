# Spring Boot validation Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)

## What is Spring Boot Data Validation, and why is it important?
<details>
<summary>Answer</summary>

- Spring Boot Data Validation is the process of ensuring that the data received by a Spring Boot application (typically through user input in forms, APIs, etc.) is accurate, complete, and conforms to specific rules. 
- It is important because it helps prevent invalid data from entering the system, which could lead to errors, data corruption, or security vulnerabilities. 
- Data validation ensures that applications behave as expected, are secure, and provide a good user experience.

- Spring Boot leverages Java Bean Validation API (JSR 303/JSR 380) via annotations like @NotNull, @Size, @Email, etc., to automatically validate input data.

</details>


## What are some commonly used annotations for validation in Spring Boot?
<details>
<summary>Answer</summary>

**Some of the most commonly used annotations for validation in Spring Boot are:**
- @NotNull: Ensures that a field is not null.
- @NotEmpty: Ensures that a field is not null and not empty (for strings, collections, etc.).
- @Size(min = x, max = y): Specifies that a field’s size should be between min and max.
- @Email: Ensures that a string is a valid email address.
- @Min(value = x): Ensures that a numeric field is greater than or equal to x.
- @Max(value = x): Ensures that a numeric field is less than or equal to x.
- @Pattern(regexp = "regex"): Validates that a field matches a regular expression.
- @Past: Ensures that a date is in the past.
- @Future: Ensures that a date is in the future.

These annotations can be used on fields in Java classes to automatically validate the data.

</details>

## How do you integrate Spring Boot Data Validation into a RESTful API?
<details>
<summary>Answer</summary>

- In a Spring Boot RESTful API, you can integrate data validation by annotating your request DTOs (Data Transfer Objects) with validation annotations and using @Valid or @Validated in the controller method parameters.

Here is an example:

DTO with Validation Annotations:

```java
import javax.validation.constraints.*;

public class UserDTO {
    @NotNull
    @Size(min = 3, max = 50)
    private String name;

    @Email
    private String email;

    @Min(18)
    private int age;

    // Getters and setters
}

```
Controller Method:

```java
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    @PostMapping
    public ResponseEntity<String> createUser(@RequestBody @Valid UserDTO userDTO) {
        // If validation fails, it will throw a MethodArgumentNotValidException
        return ResponseEntity.ok("User created successfully!");
    }
}

```

- Here, when the POST request is sent with a UserDTO, Spring Boot will automatically validate the data based on the annotations in the DTO class.

</details>

## What happens if validation fails in a Spring Boot application?
<details>
<summary>Answer</summary>

-  If validation fails, Spring Boot will throw a MethodArgumentNotValidException (or ConstraintViolationException in some cases) by default. 
- This exception can be caught and handled globally using @ExceptionHandler or a @ControllerAdvice class, where you can customize the error response.

- Here’s an example of how to handle validation exceptions globally:

```java
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.HashMap;
import java.util.Map;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidationExceptions(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getAllErrors().forEach(error -> {
            String fieldName = ((FieldError) error).getField();
            String message = error.getDefaultMessage();
            errors.put(fieldName, message);
        });
        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }
}

```

- This will return a 400 Bad Request with a message that describes the validation errors for the fields.

</details>

## What is the difference between @Valid and @Validated in Spring Boot?
<details>
<summary>Answer</summary>

- @Valid is a standard annotation from the Java Bean Validation API (JSR 303/JSR 380). It triggers validation of the annotated object, ensuring that the constraints are checked when the object is used.

- @Validated is a Spring-specific variant that not only triggers validation but also supports validation groups. It allows you to specify different validation groups for different scenarios.

- In most cases, @Valid will suffice for general validation, but if you need to define specific validation groups, you should use @Validated.

Example:

```java
import javax.validation.constraints.*;

public interface CreateGroup {}

public class UserDTO {
    @NotNull(groups = CreateGroup.class)
    private String name;
}

```

Usage Example:

```java
    @PostMapping("/create")
    public ResponseEntity<String> createUser(@RequestBody @Validated(CreateGroup.class) UserDTO userDTO){} 
```

In this case, validation will occur for the CreateGroup group when @Validated(CreateGroup.class) is used.

</details>

## How can you customize validation messages in Spring Boot?
<details>
<summary>Answer</summary>

- In Spring Boot, you can customize validation error messages by providing custom messages in the annotation itself or by externalizing them to a properties file.

Custom Message in Annotation:

```java
public class UserDTO {
    @NotNull(message = "Name cannot be null")
    private String name;
}

```

Externalizing Validation Messages:

You can define custom messages in the messages.properties file:

```properties
# messages.properties
NotNull.userDTO.name=Name cannot be null

```
Then, in the DTO, you reference the message key:

```java
@NotNull(message = "{NotNull.userDTO.name}")
private String name;

```
Spring Boot will automatically resolve the message from the messages.properties file.


</details>

## What is the purpose of the @Pattern annotation in Spring Boot validation?
<details>
<summary>Answer</summary>

- The @Pattern annotation is used to validate that a string field matches a specified regular expression. 
- This is useful for validating formats like phone numbers, postal codes, or any other custom text patterns.

Example:

```java
public class UserDTO {
    @Pattern(regexp = "^[A-Za-z0-9]{6,12}$", message = "Username must be between 6 and 12 alphanumeric characters.")
    private String username;
}

```

- In this case, the username field must be between 6 and 12 characters long and can only contain alphanumeric characters.

</details>


## Can you perform custom validation in Spring Boot?
<details>
<summary>Answer</summary>

- Yes, you can create custom validation annotations in Spring Boot by implementing a custom validator. 
- This involves creating a new annotation and a corresponding validator class.

**Here’s how to do it:**

Create the Annotation:

```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = MyCustomValidator.class)
@Documented
public @interface ValidPassword {
    String message() default "Password must contain at least one uppercase letter, one number, and be at least 8 characters long";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}

```

Create the Validator:

```java
import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

public class MyCustomValidator implements ConstraintValidator<ValidPassword, String> {

    @Override
    public void initialize(ValidPassword constraintAnnotation) {}

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        if (value == null) {
            return false;
        }
        return value.matches(".*[A-Z].*") && value.matches(".*[0-9].*") && value.length() >= 8;
    }
}

```

Use the Custom Annotation:


```java
public class UserDTO {
    @ValidPassword
    private String password;
}

```
</details>

## How can you handle multiple validation annotations on a single field?
<details>
<summary>Answer</summary>

- In Spring Boot, you can apply multiple validation annotations to a single field. 
- When multiple annotations are used, Spring Boot will check each of them, and if any validation fails, it will trigger the corresponding error.

Example:

```java
public class UserDTO {
    @NotNull(message = "Name cannot be null")
    @Size(min = 3, max = 50, message = "Name must be between 3 and 50 characters")
    private String name;

    @Email(message = "Invalid email format")
    @NotEmpty(message = "Email cannot be empty")
    private String email;

    @Min(value = 18, message = "Age must be at least 18")
    @Max(value = 100, message = "Age must be at most 100")
    private int age;
}

```
Here, Spring Boot will validate that name is both non-null and within the specified size range, email is valid and non-empty, and age is between 18 and 100.

</details>


## What are validation groups, and how do you use them in Spring Boot?
<details>
<summary>Answer</summary>

-  Validation groups allow you to categorize and apply different validation constraints in different scenarios. For example, when updating an entity, you might want to apply different validation rules than when creating it.
- You can define custom groups using interfaces, and then specify which group to validate in different use cases.


- Define Validation Groups:

```java
public interface CreateGroup {}
public interface UpdateGroup {}

```

Annotate DTO with Groups:

```java
public class UserDTO {
    @NotNull(groups = CreateGroup.class, message = "Name is required during creation")
    private String name;

    @Min(value = 18, groups = CreateGroup.class, message = "Age must be at least 18")
    private int age;

    @Size(min = 6, groups = UpdateGroup.class, message = "Password must be at least 6 characters for updates")
    private String password;
}

```

Use Groups in Controller:

```java
@PostMapping("/create")
public ResponseEntity<String> createUser(@RequestBody @Validated(CreateGroup.class) UserDTO userDTO) {
    // Validation for CreateGroup is applied here
    return ResponseEntity.ok("User created successfully!");
}

@PutMapping("/update")
public ResponseEntity<String> updateUser(@RequestBody @Validated(UpdateGroup.class) UserDTO userDTO) {
    // Validation for UpdateGroup is applied here
    return ResponseEntity.ok("User updated successfully!");
}

```

In this example, validation for the UserDTO will be different depending on whether you are creating or updating the user.

</details>


## How would you validate a collection of objects (e.g., a List) in Spring Boot?
<details>
<summary>Answer</summary>

- You can validate a collection of objects by using the @Valid annotation on the collection field. 
- This will trigger validation for each individual object within the collection.

Example:

```java
public class OrderDTO {
    @NotNull
    private String orderId;

    @NotEmpty(message = "Order items cannot be empty")
    @Valid  // Triggers validation for each item in the list
    private List<@Valid ItemDTO> items;
}

public class ItemDTO {
    @NotNull(message = "Item name is required")
    private String name;

    @Min(value = 1, message = "Quantity must be at least 1")
    private int quantity;
}

```
In this case, each item in the items list will be validated individually. If any item fails validation, it will result in a validation error for that particular item.

</details>

## What is the difference between @NotNull and @NotEmpty annotations in Spring Boot?
<details>
<summary>Answer</summary>

- @NotNull: Ensures that the field is not null, but it allows empty values (e.g., empty strings, empty collections). This annotation checks for nullity only.
- @NotEmpty: Ensures that the field is not null and not empty. For strings, it ensures the string is not empty (""), and for collections, it ensures that the collection is not empty.

```java
public class UserDTO {
    @NotNull(message = "Name cannot be null")
    private String name;

    @NotEmpty(message = "Email cannot be empty")
    private String email;
}

```
Here, name can be null, but email cannot be null or empty.

</details>


## How can you validate an object graph in Spring Boot (e.g., validating nested objects)?
<details>
<summary>Answer</summary>

- To validate an object graph (i.e., nested objects), you can use the @Valid annotation on the nested fields. This ensures that the validation rules for the nested objects are also triggered.

Example:

```java
public class UserDTO {
    @NotNull
    private String username;

    @NotNull
    private String password;

    @Valid // Trigger validation for AddressDTO
    private AddressDTO address;
}

public class AddressDTO {
    @NotNull
    private String street;

    @NotNull
    private String city;
}

```
In this example, Spring Boot will validate not only the UserDTO fields but also the AddressDTO fields because of the @Valid annotation on the address field.

</details>













