# Spring Boot JPA Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)

## What is Spring Boot and how does it differ from Spring Framework?
<details>
<summary>Answer</summary>

- Spring Boot is a framework built on top of the Spring Framework that simplifies the development of Spring-based applications. 
- It eliminates the need for complex XML configuration and simplifies project setup by providing default configurations, embedded web servers (like Tomcat, Jetty), and various production-ready features such as health checks, metrics, and application monitoring.

**Key differences from Spring Framework:**
- Spring Boot eliminates boilerplate code and reduces configuration with automatic configurations and starter templates.
- It embeds web servers (like Tomcat, Jetty), removing the need for external server configuration.
- Spring Boot applications can be run as standalone applications (with embedded containers), unlike Spring Framework, which requires external server deployment.

</details>

## What is Spring Data JPA and why is it used?
<details>
<summary>Answer</summary>

-  Spring Data JPA is part of the larger Spring Data project that provides easy integration of Java Persistence API (JPA) in Spring applications. 
- It reduces boilerplate code and simplifies data access layers, providing convenient features like repositories, automatic query generation, pagination, and auditing.

- It abstracts the underlying JPA implementation (e.g., Hibernate) and allows developers to focus on defining entities and repositories rather than dealing with complex SQL queries and boilerplate code for data operations.
</details>

## What are the advantages of using Spring Data JPA?
<details>
<summary>Answer</summary>

- **Reduced boilerplate code:** Spring Data JPA automatically implements repository interfaces, reducing the need to write custom DAO (Data Access Object) classes and queries.
- **Automatic query generation:** Queries can be defined through method names, and Spring Data JPA automatically generates SQL based on the method signature.
- **Easy pagination and sorting:** Spring Data JPA provides built-in support for pagination and sorting without requiring custom implementation.
- **Integration with JPA providers:** It integrates seamlessly with JPA providers like Hibernate, making it easy to use a wide range of database operations.
- **Custom queries with @Query:** It allows for custom queries using JPQL or SQL directly in repository methods.

</details>

## What are the common annotations used in Spring Data JPA?
<details>
<summary>Answer</summary>

- @Entity: Marks a class as a JPA entity.
- @Id: Specifies the primary key of the entity.
- @GeneratedValue: Automatically generates the primary key value.
- @OneToMany, @ManyToOne, @OneToOne, @ManyToMany: Define relationships between entities.
- @JoinColumn: Specifies the column for joining two entities in a relationship.
- @Query: Defines a custom JPQL (Java Persistence Query Language) or SQL query.
- @Transactional: Marks methods for transaction management in JPA.
- @Repository: Marks a class as a Spring Data JPA repository, though it is optional for interfaces.

</details>

## What is the use of @Query annotation in Spring Data JPA?
<details>
<summary>Answer</summary>

- The @Query annotation allows the developer to define custom JPQL (Java Persistence Query Language) or native SQL queries for the repository methods. 
- It provides flexibility when the auto-generated queries do not meet the specific requirements.

Example:
```java
public interface UserRepository extends JpaRepository<User, Long> {

    @Query("SELECT u FROM User u WHERE u.email = ?1")
    User findByEmail(String email);

    @Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
    User findByEmailNative(String email);
}

```

- nativeQuery = true tells Spring Data JPA that the query is a native SQL query instead of JPQL.

</details>

## What is the purpose of @Modifying annotation in Spring Data JPA?
<details>
<summary>Answer</summary>

- The @Modifying annotation is used in conjunction with the @Query annotation when you want to execute a modifying query (e.g., INSERT, UPDATE, DELETE) rather than a SELECT query.

Example:
```java
public interface UserRepository extends JpaRepository<User, Long> {

    @Modifying
    @Query("UPDATE User u SET u.status = ?1 WHERE u.id = ?2")
    int updateUserStatus(String status, Long id);
}

```
- In this example, the @Modifying annotation is required because the query modifies the data in the database (update).

</details>

## What is the difference between JpaRepository and CrudRepository?
<details>
<summary>Answer</summary>

- Both JpaRepository and CrudRepository are Spring Data interfaces used to interact with the database, but they offer different levels of functionality:
  - CrudRepository: Provides basic CRUD operations (Create, Read, Update, Delete). It defines methods like save(), findById(), findAll(), delete(), etc.
  - JpaRepository: Extends CrudRepository and adds JPA-specific operations like batch operations (flush()), pagination (findAll(Pageable pageable)), and sorting (findAll(Sort sort)).


In general, if you're using JPA and need more advanced features like pagination and sorting, JpaRepository is preferred.

</details>

## Explain how pagination works in Spring Data JPA.
<details>
<summary>Answer</summary>

- Pagination in Spring Data JPA is handled by the Pageable interface. You can use Pageable to define the page size, page number, and sorting order.

Example:

```java
public interface UserRepository extends JpaRepository<User, Long> {

    Page<User> findByStatus(String status, Pageable pageable);
}

```

To use pagination:

```java
Pageable pageable = PageRequest.of(0, 10, Sort.by("name").ascending());
Page<User> usersPage = userRepository.findByStatus("active", pageable);

List<User> users = usersPage.getContent();  // This gets the list of users for the current page
long totalElements = usersPage.getTotalElements();  // Total number of users in the database

```

Where:
- PageRequest.of(0, 10) creates a page request for the first page with 10 elements per page.
- Page provides additional information like the total number of pages, total elements, and whether it is the first/last page.

</details>

## What are the common strategies for handling transactions in Spring Data JPA?
<details>
<summary>Answer</summary>

-  Spring Data JPA uses @Transactional to manage transactions. 
- By default, transactions are handled at the service layer, and Spring manages the transaction boundaries (commit or rollback) automatically.

- @Transactional: This annotation can be placed on service methods to ensure that the database operations within the method are part of a single transaction. If an exception occurs, the transaction will be rolled back automatically.

```java
@Service
public class UserService {

    @Transactional
    public void updateUser(Long userId, String newStatus) {
        User user = userRepository.findById(userId).orElseThrow();
        user.setStatus(newStatus);
        userRepository.save(user);
    }
}

```
</details>

## What are some performance optimizations in Spring Data JPA?
<details>
<summary>Answer</summary>

- Some common performance optimizations in Spring Data JPA include:
  - Lazy Loading: Use @OneToMany or @ManyToMany with fetch = FetchType.LAZY to avoid unnecessary database queries.
  - Eager Loading: Use @OneToMany or @ManyToMany with fetch = FetchType.EAGER when necessary to avoid multiple round trips to the database (though use cautiously, as it can lead to performance degradation if misused).
  - Batch Processing: Use JpaRepository.saveAll() for batch saving of entities rather than calling save() in a loop.
  - Indexes: Make sure that frequently queried fields are indexed in the database.
  - Pagination and Sorting: Use Pageable and Sort to limit the number of records retrieved from the database.

</details>

##  What are the differences between EntityManager and JpaRepository?
<details>
<summary>Answer</summary>

- JpaRepository: It is a Spring Data JPA interface that provides high-level CRUD and query methods. It is typically used for typical data access operations.
- EntityManager: It is a JPA interface that provides lower-level control over JPA entities. It allows operations like persist(), merge(), remove(), and direct interaction with the persistence context.

While JpaRepository is convenient and abstracts the EntityManager, you can use EntityManager when you need more fine-grained control or want to work with more complex queries directly.

</details>

##  What is the difference between @Entity and @Table annotations in Spring Data JPA?
<details>
<summary>Answer</summary>

- @Entity: This annotation is used to mark a Java class as a JPA entity. The class is mapped to a table in the database.
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;
}

```

- @Table: This annotation is used to specify the name of the table in the database to which the entity will be mapped. It is optional; if not provided, JPA assumes the table name is the same as the entity class name.

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    private Long id;
    private String name;
}

```
</details>

## What is a @ManyToOne relationship in Spring Data JPA?
<details>
<summary>Answer</summary>

- The @ManyToOne annotation represents a many-to-one relationship between two entities.
- It means that many instances of one entity can be associated with a single instance of another entity.

```java
@Entity
public class Order {

    @Id
    private Long id;

    @ManyToOne
    @JoinColumn(name = "customer_id")
    private Customer customer;
}

```
- Here, multiple Order entities can be associated with a single Customer entity, and the foreign key is customer_id.

</details>

## What is the difference between @OneToMany and @ManyToOne annotations in JPA?
<details>
<summary>Answer</summary>

- @OneToMany: Represents a one-to-many relationship where one entity (the parent) can have multiple associated child entities. 
- For example, a Customer can have many Orders.

```java
@Entity
public class Customer {
    @Id
    private Long id;

    @OneToMany(mappedBy = "customer")
    private List<Order> orders;
}

```

- @ManyToOne: Represents the inverse side of the @OneToMany relationship, where many child entities are associated with one parent entity. 
- For example, many Orders belong to a single Customer.

Example:
```java
@Entity
public class Order {
    @Id
    private Long id;

    @ManyToOne
    @JoinColumn(name = "customer_id")
    private Customer customer;
}

```

</details>

## What is the purpose of @GeneratedValue annotation in JPA?
<details>
<summary>Answer</summary>

- The @GeneratedValue annotation is used to define how the primary key value is generated. It is typically used with @Id to automatically generate unique IDs for entities.

Example:

```java
@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // Auto-increment strategy
    private Long id;

    private String name;
}

```

**Generation Types:**:
- GenerationType.AUTO: The persistence provider (e.g., Hibernate) will choose the generation strategy (typically auto or identity).
- GenerationType.IDENTITY: The database auto-generates the primary key (auto-increment for databases like MySQL).
- GenerationType.SEQUENCE: A sequence is used for generating primary key values (for databases like Oracle).
- GenerationType.TABLE: Uses a special table to generate primary key values (less common).

</details>


## What is the difference between @Transactional at the class level and the method level in Spring?
<details>
<summary>Answer</summary>

- At the class level: @Transactional applied at the class level means that all methods in the class are transactionally managed unless overridden by a method-level @Transactional.
```java
@Service
@Transactional
public class UserService {
    // All methods will be transactional by default
    public void saveUser(User user) { ... }
}

```

- At the method level: @Transactional can also be applied to individual methods to override the class-level behavior and customize the transaction management for specific methods.

```java
@Service
@Transactional
public class UserService {
    
    @Transactional(readOnly = true)
    public User findUser(Long userId) { ... }  // Read-only transaction

    @Transactional
    public void saveUser(User user) { ... }
}

```
</details>


## How does Spring Boot handle database migrations?
<details>
<summary>Answer</summary>

- Spring Boot does not handle database migrations out-of-the-box, but it integrates easily with popular tools like Flyway and Liquibase.
  - Flyway: Flyway is a database migration tool that works with Spring Boot to automatically apply migrations at startup. It uses SQL scripts or Java classes to apply database changes.
```xml
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
</dependency>

```
    - Place migration scripts in src/main/resources/db/migration.
    - Flyway will automatically run all migrations (e.g., V1__Create_table_user.sql, V2__Add_column_status.sql) when the application starts.

- Liquibase: Similar to Flyway but more flexible with XML-based changelogs.

</details>

## How does Spring Boot automatically configure a DataSource for JPA?
<details>
<summary>Answer</summary>

- Spring Boot automatically configures a DataSource for JPA based on the properties defined in the application.properties or application.yml file. 
- If Spring Boot detects that HikariCP (the default connection pool) or another connection pool library is present, it will use it to configure the DataSource.

**Key properties include:**
- spring.datasource.url: The JDBC URL for connecting to the database.
- spring.datasource.username: The username to connect to the database.
- spring.datasource.password: The password for the database connection.
- spring.datasource.driver-class-name: The database driver class (e.g., com.mysql.cj.jdbc.Driver).

Spring Boot will also set sensible defaults for connection pooling, such as HikariCP as the default connection pool and automatic database connection validation.


```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=secret
spring.jpa.hibernate.ddl-auto=update

```
If you have a database driver (like MySQL, PostgreSQL) in your classpath, Spring Boot will configure the DataSource and related connection pool automatically.

</details>

##  What are the properties in application.properties that control JPA configuration in Spring Boot?
<details>
<summary>Answer</summary>

- Here are some common application.properties settings for JPA and Hibernate in Spring Boot
  - spring.datasource.url: The JDBC URL of the database.
  - spring.datasource.username: The database username.
  - spring.datasource.password: The database password.
  - spring.datasource.driver-class-name: The database driver class name (e.g., com.mysql.cj.jdbc.Driver).
  - spring.jpa.hibernate.ddl-auto: Controls the schema generation process. Possible values are:
    - none: No schema generation.
    - update: Updates the schema automatically (commonly used in development).
    - create: Drops and creates the schema on application startup.
    - create-drop: Drops and creates the schema on application startup and shutdown.
  - spring.jpa.show-sql: Set to true to log the SQL queries executed by Hibernate.
  - spring.jpa.properties.hibernate.dialect: Specifies the Hibernate dialect for the database (e.g., org.hibernate.dialect.MySQLDialect).
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=secret
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

```

These settings allow Spring Boot to automatically configure a JPA DataSource, manage the Hibernate session, and adjust other relevant configurations.

</details>


## How can you disable JPA autoconfiguration in Spring Boot?
<details>
<summary>Answer</summary>

- Answer: If you don't want Spring Boot to auto-configure JPA, you can disable the JPA autoconfiguration by excluding the relevant autoconfiguration classes in your @SpringBootApplication or @EnableAutoConfiguration annotations.

Example

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class, HibernateJpaAutoConfiguration.class})
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}

```

- This excludes the DataSourceAutoConfiguration and HibernateJpaAutoConfiguration classes, effectively preventing Spring Boot from setting up any JPA-related beans.

</details>

## How does Spring Boot handle Hibernate as the default JPA provider?
<details>
<summary>Answer</summary>

- By default, Spring Boot uses Hibernate as the JPA provider when the spring-boot-starter-data-jpa dependency is added. 
- It automatically configures Hibernate's EntityManagerFactory and JpaTransactionManager. 
- You don’t need to manually configure these beans unless you have a specific requirement.

- Spring Boot will also configure the Hibernate SessionFactory, transaction management, and connection pooling using defaults or properties defined in application.properties.

Example: If you don't explicitly set the JPA provider, Hibernate will be chosen by default:

```properties
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

```

</details>

## What happens if there are multiple DataSource beans in a Spring Boot application?
<details>
<summary>Answer</summary>

- If there are multiple DataSource beans defined in the application, Spring Boot will throw an exception during startup because it doesn't know which one to use by default. In such cases, you need to explicitly define which DataSource should be used for JPA by marking the primary one with @Primary or using the @Qualifier annotation to distinguish between them.

```java
@Configuration
public class DataSourceConfig {

    @Bean
    @Primary
    public DataSource dataSource() {
        return new HikariDataSource();
    }

    @Bean
    @Qualifier("secondaryDataSource")
    public DataSource secondaryDataSource() {
        return new HikariDataSource();
    }
}

```
</details>


##  What are custom query methods in Spring Data JPA?
<details>
<summary>Answer</summary>

- Custom query methods in Spring Data JPA allow you to define more complex database queries that go beyond the basic CRUD operations provided by JpaRepository or CrudRepository.
- You can write custom queries using:
  - Query Method Derivation: Spring Data JPA automatically generates queries based on method names.
  - JPQL (Java Persistence Query Language): You can use the @Query annotation to write your own JPQL queries.
  - Native SQL: If necessary, you can use the @Query annotation to execute native SQL queries directly against the database.

**Example of a Custom Query Method:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    // Custom query method derived from the method name
    List<User> findByLastName(String lastName);

    // Custom JPQL query using @Query
    @Query("SELECT u FROM User u WHERE u.firstName = :firstName")
    List<User> findUsersByFirstName(@Param("firstName") String firstName);
}

```
</details>

## What is the difference between derived query methods and custom queries in Spring Data JPA?
<details>
<summary>Answer</summary>

- Derived Query Methods: These methods allow you to define queries based on the method name following a certain naming convention. 
- Spring Data JPA will automatically generate the necessary query for you.

```java
List<User> findByFirstNameAndAge(String firstName, int age);

```

This method will automatically generate a query like:

```sql
SELECT u FROM User u WHERE u.firstName = ?1 AND u.age = ?2

```

- Custom Queries: These are queries written explicitly using the @Query annotation with either JPQL (Java Persistence Query Language) or native SQL. 
- Custom queries provide more flexibility, especially when dealing with complex queries that cannot be represented by the method name conventions.

Example JPQL: 

```java
@Query("SELECT u FROM User u WHERE u.firstName = :firstName AND u.age > :age")
List<User> findUsersByFirstNameAndAge(@Param("firstName") String firstName, @Param("age") int age);

```

Example with Native SQL : 

```java
@Query(value = "SELECT * FROM users WHERE first_name = ?1 AND age > ?2", nativeQuery = true)
List<User> findUsersByFirstNameAndAgeNative(String firstName, int age);

```
</details>


## How do you use the @Query annotation in Spring Data JPA?
<details>
<summary>Answer</summary>
 
- The @Query annotation in Spring Data JPA allows you to define custom JPQL or SQL queries. 
- The query can be a simple select query or a more complex one with joins, group by, etc. 
- It is commonly used when the derived query methods do not provide sufficient flexibility.


  You can also use the @Param annotation to bind method parameters to the query parameters.


Example 

```java
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);

```

Example: Native SQL Query

```java
@Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
User findByEmailNative(String email);

```

In the above examples, the @Query annotation defines a custom query, and the @Param annotation is used to bind the method argument to the query parameter.

</details>


## What is the purpose of nativeQuery in the @Query annotation?
<details>
<summary>Answer</summary>

- The nativeQuery attribute in the @Query annotation allows you to specify whether the query should be treated as a native SQL query rather than a JPQL (Java Persistence Query Language) query.
  - nativeQuery = true: The query is a native SQL query, which is executed directly against the underlying database using the specific SQL dialect of that database.
  - nativeQuery = false (default): The query is written in JPQL, which is database-independent and works with entity mappings rather than table names.

```java
// Native SQL query
@Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
User findByEmailNative(String email);

// JPQL query (default)
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmailJPQL(@Param("email") String email);

```
In the first example, nativeQuery = true means that the query will be executed as a SQL query, while in the second example, the query will be executed using JPQL.

</details>

##  What is the default connection pool in Spring Boot? How can you configure it?
<details>
<summary>Answer</summary>

- The default connection pool in Spring Boot is HikariCP. 
- HikariCP is known for its high performance and low overhead, making it the default choice for connection pooling in Spring Boot applications.
  - spring.datasource.url: The JDBC URL of the database.
  - spring.datasource.username: The username for the database.
  - spring.datasource.password: The password for the database.
  - spring.datasource.hikari.*: HikariCP-specific configuration properties.

Example:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# HikariCP specific settings
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.idle-timeout=30000
spring.datasource.hikari.max-lifetime=600000

```

You can also configure additional properties like:
- maximum-pool-size: The maximum number of connections in the pool.
- minimum-idle: The minimum number of idle connections to maintain in the pool.
- idle-timeout: The maximum time a connection can be idle before being closed.
- max-lifetime: The maximum lifetime of a connection in the pool.

</details>












