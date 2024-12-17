# Spring boot caching Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)


## What is Spring Boot Caching?
<details>
<summary>Answer</summary>

- Spring Boot Caching is a mechanism provided by Spring Framework to improve application performance by storing frequently used data in an in-memory data store or external caching system. 
- It uses annotations like @Cacheable, @CachePut, and @CacheEvict to manage caching behavior.

</details>


##  What are the annotations used in Spring Boot Caching?
<details>
<summary>Answer</summary>

- **@EnableCaching:** Enables caching support in a Spring Boot application.
- **@Cacheable:** Marks a method’s return value as cacheable.
- **@CachePut:** Updates the cache with a new value.
- **@CacheEvict:** Removes entries from the cache.
- **@Caching:** Allows combining multiple caching annotations.

</details>

## How do you enable caching in a Spring Boot application?
<details>
<summary>Answer</summary>

- To enable caching, follow these steps:
  - Add the dependency for a cache provider (e.g., EhCache, Redis, etc.).
  - Annotate the Spring Boot application class with @EnableCaching.
  - Use caching annotations (@Cacheable, @CacheEvict, etc.) on methods where caching is required.

```java
@SpringBootApplication
@EnableCaching  // This is required. if you don't do this caching will not be enabled.
public class CachingApplication {
    public static void main(String[] args) {
        SpringApplication.run(CachingApplication.class, args);
    }
}

```
</details>

## What is @Cacheable in Spring Boot?
<details>
<summary>Answer</summary>

- @Cacheable is an annotation that indicates a method's return value should be stored in the cache. 
- If the same method is called with the same parameters, the cached result is returned instead of executing the method again.

Example:

```java
@Cacheable(value = "products", key = "#id")
public Product getProductById(Long id) {
    // Method logic
}

```

</details>

## What is @CacheEvict in Spring Boot?
<details>
<summary>Answer</summary>

- @CacheEvict is used to remove entries from the cache. 
- It can be used when you need to clear specific cache entries or an entire cache.

```java
@CacheEvict(value = "products", key = "#id")
public void deleteProductById(Long id) {
    // Delete logic
}

```
</details>

## What is @CachePut in Spring Boot?
<details>
<summary>Answer</summary>

- @CachePut is used to update the cache without skipping method execution.
- It ensures the method is executed and the return value is updated in the cache.

```java
@CachePut(value = "products", key = "#product.id")
public Product updateProduct(Product product) {
    // Update product logic
    return product;
}

```

</details>

## What happens when @Cacheable is applied to a method that returns null?
<details>
<summary>Answer</summary>

- By default, if a method annotated with @Cacheable returns null, no entry is added to the cache. 
- However, you can configure the cache provider to handle null values explicitly.

</details>


## What are the key generation strategies in Spring Boot caching?
<details>
<summary>Answer</summary>

- Spring uses a SimpleKeyGenerator by default to generate cache keys. You can customize the key generation by:
  - Using the key attribute in caching annotations (e.g., key = "#id").
  - Implementing a custom KeyGenerator bean.

```java
@Bean
public KeyGenerator customKeyGenerator() {
    return (target, method, params) -> Arrays.toString(params);
}

```
</details>

## What is the difference between @Cacheable and @CachePut?
<details>
<summary>Answer</summary>

| Aspect       | @Cacheable                                    | @CachePut                         |
|--------------|-----------------------------------------------|------------------------------------|
| **Behavior** | Caches the result only if it is not present in the cache. | Always updates the cache.         |
| **Execution**| Skips method execution if cache exists.       | Always executes the method.       |
| **Use Case** | For read-only operations.                    | For operations that modify data.  |

</details>

## How do you clear all entries from a cache?
<details>
<summary>Answer</summary>

- To clear all entries, use @CacheEvict with the allEntries = true attribute.

Example:
```java
@CacheEvict(value = "products", allEntries = true)
public void clearAllProductsCache() {
    // Logic to clear cache
}

```

</details>

## How do you implement caching with Redis in Spring Boot?
<details>
<summary>Answer</summary>

- Add Redis dependencies:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>

```
- Configure Redis properties in application.properties:

```properties
spring.redis.host=localhost
spring.redis.port=6379

```

- Enable caching and use caching annotations:

```java
@Cacheable(value = "users", key = "#id")
public User getUserById(Long id) {
    // Business logic
}

```
</details>

## How do you customize cache configuration in Spring Boot?
<details>
<summary>Answer</summary>

- You can configure cache properties using CacheManager. For example, configuring Redis:

```java
import org.springframework.cache.CacheManager;
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.serializer.RedisSerializationContext;
import org.springframework.data.redis.serializer.StringRedisSerializer;

import java.time.Duration;

@Configuration
@EnableCaching
public class RedisCacheConfig {

    @Bean
    public CacheManager cacheManager(RedisConnectionFactory redisConnectionFactory) {
        // Custom cache configuration
        RedisCacheConfiguration cacheConfiguration = RedisCacheConfiguration.defaultCacheConfig()
                .entryTtl(Duration.ofMinutes(60)) // Time to live for cache entries
                .disableCachingNullValues() // Disable caching null values
                .serializeKeysWith(
                        RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()))
                .serializeValuesWith(
                        RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()));

        // Create and return RedisCacheManager
        return RedisCacheManager.builder(redisConnectionFactory)
                .cacheDefaults(cacheConfiguration)
                .build();
    }
}

```
</details>


## What is the difference between CacheManager and CacheResolver?
<details>
<summary>Answer</summary>

- CacheManager: Manages the cache and is used to retrieve cache instances.
- CacheResolver: Used to resolve the caches dynamically at runtime based on method parameters or other factors.

</details>

## What are common caching providers supported by Spring Boot?
<details>
<summary>Answer</summary>

- Spring Boot supports various caching providers like:
  - EhCache
  -  Hazelcast
  -  Redis
  -  Caffeine
  -  Guava
  -  JCache (JSR-107 compliant)

</details>

## How can you test caching in a Spring Boot application?
<details>
<summary>Answer</summary>

- You can test caching behavior using:
  - Mocking: Verify if the service method is called only once when caching is applied.
  - Spring Boot Testing: Use @SpringBootTest and verify cache entries.
  - CacheManager Inspection: Check if values are added to or evicted from the cache.

```java
@Autowired
private CacheManager cacheManager;

@Test
public void testCaching() {
    productService.getProductById(1L);
    Cache cache = cacheManager.getCache("products");
    assertNotNull(cache.get(1L).get());
}

```
</details>

## How do you specify the cache key in @Cacheable
<details>
<summary>Answer</summary>

- The cache key is specified using the key attribute in the @Cacheable annotation. Spring EL (Expression Language) is used to define the key.
  - Default key (method arguments):

```java
@Cacheable("products")
public Product getProductById(Long id) {
    return productRepository.findById(id).orElse(null);
}

```

- Custom key:
```java
@Cacheable(value = "products", key = "#id")
public Product getProductById(Long id) {
    return productRepository.findById(id).orElse(null);
}

```
- Multiple parameters:

```java
@Cacheable(value = "products", key = "#name + '_' + #category")
public List<Product> getProducts(String name, String category) {
    return productRepository.findByNameAndCategory(name, category);
}

```
</details>

## What is the purpose of the @Caching annotation?
<details>
<summary>Answer</summary>

- The @Caching annotation is used when multiple cache annotations (e.g., @Cacheable, @CachePut, @CacheEvict) are needed for a single method.

```java
@Caching(
    cacheable = @Cacheable(value = "products", key = "#id"),
    evict = @CacheEvict(value = "products", key = "#oldId")
)
public Product replaceProduct(Long oldId, Long id, Product newProduct) {
    productRepository.deleteById(oldId);
    return productRepository.save(newProduct);
}

```
</details>

## What is the difference between @Cacheable and @CacheConfig?
<details>
<summary>Answer</summary>

- @Cacheable: Used at the method level to define caching behavior for individual methods.
- @CacheConfig: Used at the class level to define common caching properties (e.g., cache names) for all methods in the class.

```java
@CacheConfig(cacheNames = {"products"})
public class ProductService {

    @Cacheable(key = "#id")
    public Product getProductById(Long id) {
        return productRepository.findById(id).orElse(null);
    }

    @CacheEvict(allEntries = true)
    public void clearCache() {
        // Clears the "products" cache
    }
}

```

</details>

## How to Specify Which CacheManager to Use?
<details>
<summary>Answer</summary>

- Use @Primary for the Default Cache Manager: The @Primary annotation marks one of the CacheManager beans as the default. 
- If no specific cache manager is specified in the @Cacheable, @CacheEvict, etc., Spring will use this primary cache manager.

```java
@Bean
@Primary
public CacheManager caffeineCacheManager() {
    return new CaffeineCacheManager("defaultCache");
}

@Bean
public CacheManager redisCacheManager(RedisConnectionFactory factory) {
    return RedisCacheManager.builder(factory).build();
}

```

- In this case:
  - The caffeineCacheManager will be used by default because of the @Primary annotation.
  - The redisCacheManager can still be explicitly referenced.


- Specify Cache Manager at Annotation Level: You can explicitly define which cache manager to use by setting the cacheManager property in the caching annotations.

```java
@Cacheable(value = "users", cacheManager = "redisCacheManager")
public User getUserById(Long id) {
    return userRepository.findById(id).orElse(null);
}

```
- Here, the redisCacheManager is used regardless of which cache manager is marked as @Primary.

</details>

## Can Spring Boot prevent caching of null values dynamically without configuration?
<details>
<summary>Answer</summary>
 
- Yes, Spring Boot can dynamically prevent caching of null values by using conditional caching with the unless attribute in @Cacheable.

```java
@Cacheable(value = "products", key = "#id", unless = "#result == null")
public Product getProductById(Long id) {
    return productRepository.findById(id).orElse(null);
}

```

- The unless attribute prevents caching if the method returns null.

</details>


## What happens if an exception occurs while evicting the cache or executing the method annotated with @CacheEvict?
<details>
<summary>Answer</summary>

-  By default, if an exception occurs during the method execution (whether the method annotated with @CacheEvict or a @Cacheable method), the cache eviction process will be skipped. If the exception occurs after the eviction but within the same transaction (or method), the cache will still be removed, but you may end up in an inconsistent state depending on the nature of the exception.
- Flow with CacheEvict:
  - Method Execution: The method annotated with @CacheEvict is invoked.
  - Cache Eviction: If beforeInvocation = true, the cache eviction occurs before the method execution. If beforeInvocation = false (default), the cache eviction occurs after the method execution.
  - Exception Handling: If an exception is thrown during the method execution, the cache eviction may still occur if beforeInvocation was set to false. Otherwise, if the method fails before the eviction process, the cache will not be evicted.

```java
@CacheEvict(value = "products", key = "#id", beforeInvocation = true)
public void evictProductCache(Long id) {
    // Simulate cache eviction before method execution
    System.out.println("Evicting product cache for id: " + id);
    if (id == null) {
        throw new IllegalArgumentException("Invalid product ID");
    }
}

```
- beforeInvocation = true in @CacheEvict
- By setting beforeInvocation = true, the cache eviction will occur before the method is executed, meaning that even if an exception occurs during the method execution, the cache will still be evicted.

</details>

## Can you please describe Caching Strategies?
<details>
<summary>Answer</summary>


1. **Cache Aside**: Application code manages the cache; data is loaded on demand.
2. **Read-Through**: Cache sits between the application and data source, fetching data automatically.
3. **Write-Through**: Data is written to the cache and the underlying data store simultaneously.
4. **Write-Behind**: Data is written to the cache first, with asynchronous updates to the data store.
5. **Time-Based Expiration**: Cached data expires after a set time.
6. **Event-Driven Expiration**: Cache is invalidated based on specific events or changes in the data source.
7. **Size-Based Eviction**: Cache limits size and evicts the least recently used or least frequently used items.
8. **Distributed Caching**: Caches are spread across multiple nodes for scalability.
9. **Hierarchical Caching**: Multiple levels of cache, such as local and distributed caches.
10. **In-Memory Caching**: Data is stored in memory for fast access, often using tools like Redis or Memcached.
11. **Read Ahead**: Anticipates future data requests by pre-loading data into the cache based on access patterns.
12. **Cache-Around**: The cache stores results of expensive computations or database queries, reducing repeated calculations.


</details>

