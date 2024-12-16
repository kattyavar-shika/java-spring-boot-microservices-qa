# Spring Data Rest Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)

## What is Spring Data REST?
<details>
<summary>Answer</summary>

- Spring Data REST is part of the Spring Data project, which automatically exposes your Spring Data repositories as RESTful web services.
- It allows you to quickly build RESTful APIs without writing controller logic, simply by defining repositories and leveraging annotations like @RepositoryRestResource. 
- Spring Data REST also supports CRUD operations on entities and allows customization of endpoints and exposed resources.

</details>

##  How do you expose a Spring Data repository as a REST endpoint?
<details>
<summary>Answer</summary>

- To expose a Spring Data repository as a REST endpoint, you simply need to create a repository interface that extends one of Spring Data’s repository interfaces (e.g., JpaRepository, CrudRepository, etc.). 
- Then, by using the @RepositoryRestResource annotation, you can customize the endpoint path if needed. 
- By default, Spring Data REST will expose the repository as a RESTful API.

Example:

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.rest.core.annotation.RepositoryRestResource;

@RepositoryRestResource
public interface BookRepository extends JpaRepository<Book, Long> {
}

```

This will expose the Book entity as a REST resource with standard CRUD operations (GET, POST, PUT, DELETE) at /books.

</details>

## How can you customize the endpoint URL in Spring Data REST?
<details>
<summary>Answer</summary>

- You can customize the endpoint URL using the @RepositoryRestResource annotation's path attribute.

```java
@RepositoryRestResource(path = "custom-books")
public interface BookRepository extends JpaRepository<Book, Long> {
}

```
This would expose the resource at the endpoint /custom-books instead of /books.

</details>

## What is the purpose of the @RepositoryRestResource annotation?
<details>
<summary>Answer</summary>

- The @RepositoryRestResource annotation is used to customize the Spring Data REST repository endpoints. 
- You can use it to configure things like the resource path, the collection resource rel, and whether the repository should be exposed as a REST resource or not. 
- Some key properties include:
  - path: Customizes the URL path for the repository.
  - collectionResourceRel: Defines the name of the collection resource.
  - excerptProjection: Defines a projection for the resource.

</details>

## What is the @RestResource annotation, and how is it different from @RepositoryRestResource?
<details>
<summary>Answer</summary>

- The @RestResource annotation is used to customize specific methods in a repository. It is more granular than @RepositoryRestResource, which customizes the repository as a whole.
- The @RestResource annotation can be applied to individual repository methods to control their behavior, including setting the path or enabling/disabling the method in the REST API.

```java
public interface BookRepository extends JpaRepository<Book, Long> {

    @RestResource(path = "by-title", rel = "by-title")
    List<Book> findByTitle(String title);
}

```
This exposes a custom method with the path /books/search/by-title.

</details>

## How do you add custom query methods in Spring Data REST?
<details>
<summary>Answer</summary>
 
- You can add custom query methods to a Spring Data repository interface by simply defining method signatures based on the naming conventions or by using @Query annotations. 
- These methods will automatically be exposed as part of the REST API.

```java
public interface BookRepository extends JpaRepository<Book, Long> {
    List<Book> findByTitle(String title);

    @Query("SELECT b FROM Book b WHERE b.author.name = :authorName")
    List<Book> findBooksByAuthorName(@Param("authorName") String authorName);
}

```

These methods would be available at the respective endpoints, such as /books/search/findByTitle and /books/search/findBooksByAuthorName.

</details>

## How can you disable a repository from being exposed as a REST resource?
<details>
<summary>Answer</summary>

- You can disable a repository from being exposed as a REST resource by using the @RepositoryRestResource(exported = false) annotation.

```java
@RepositoryRestResource(exported = false)
public interface AuthorRepository extends JpaRepository<Author, Long> {
}

```
This will prevent the Author repository from being exposed as a REST resource.

</details>

## What are event listeners in Spring Data REST?
<details>
<summary>Answer</summary>

- Spring Data REST provides event listeners that allow you to hook into the lifecycle of RESTful interactions with your entities. 
- You can use these event listeners to perform actions before or after certain events, such as creation, update, or deletion.

```java
import org.springframework.data.rest.core.annotation.HandleBeforeCreate;
import org.springframework.data.rest.core.annotation.HandleBeforeSave;
import org.springframework.data.rest.core.annotation.RepositoryEventHandler;

@RepositoryEventHandler
public class BookEventHandler {

    @HandleBeforeCreate
    public void handleBeforeCreate(Book book) {
        book.setCreatedDate(LocalDateTime.now());
    }

    @HandleBeforeSave
    public void handleBeforeSave(Book book) {
        // Do something before saving
    }
}

```
</details>

## How can you handle CORS in Spring Data REST?
<details>
<summary>Answer</summary>

- You can handle CORS (Cross-Origin Resource Sharing) by configuring it globally or at the controller level. In Spring Data REST, it can be done using @CrossOrigin or by configuring a WebMvcConfigurer.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**").allowedOrigins("http://example.com");
    }
}

```
</details>


## Disabling HTTP Methods (DELETE and PUT) at the Repository Level Using Spring Data REST:
<details>
<summary>Answer</summary>

- If you prefer a simpler and more declarative approach without writing custom controllers or configuring security, you can directly disable DELETE and PUT by making use of Spring Data REST's support for disabling repository methods. This will work for basic Spring Data JPA repositories.

```java
@RepositoryRestResource
public interface CustomerRepository extends JpaRepository<Customer, Long> {

    // Disable DELETE method at the repository level
    @RestResource(exported = false)
    void deleteById(Long id);

    // Disable PUT (or save) method at the repository level
    @RestResource(exported = false)
    <S extends Customer> S save(S entity);
}

```

- By disabling the save() method, you effectively prevent the PUT method from being called. Similarly, disabling the deleteById() method prevents the DELETE method from being called.

</details>