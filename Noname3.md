1. **Question:** How do you handle multiple beans at the same time in Spring Boot?

   **Candidate’s Answer (Brief):**
   “You can use `@Qualifier` to specify which bean by name, or mark one bean as `@Primary` so it gets injected by default.”

   **Correct Answer:**
   When multiple candidate beans exist for injection, you can:

   * Use `@Primary` on one bean so it is chosen by default.
   * Use `@Qualifier("beanName")` alongside `@Autowired` to specify exactly which bean to inject.
   * Alternatively, inject a collection (`List<BeanType>`) to receive all matching beans.

   **Rating:** 4/5
   *Justification:* The candidate correctly identified `@Qualifier` and `@Primary`. They omitted the collection injection approach, which is a third standard method.

2. **Question:** Can you explain creating a custom annotation in Spring Boot with an example?

   **Candidate’s Answer (Brief):**
   “Define an annotation interface with `@interface`, specify `@Target` (e.g., PARAMETER) and `@Retention` (e.g., RUNTIME), then implement a validator class containing the logic, and apply the annotation on the entity field (e.g., `@EmployeeType`) to enforce validation.”

   **Correct Answer:**
   To create a custom annotation:

   1. Define the annotation type:

   ```java
   @Target(ElementType.FIELD)
   @Retention(RetentionPolicy.RUNTIME)
   @Constraint(validatedBy = EmployeeTypeValidator.class)
   public @interface EmployeeType {
       String message() default "Invalid employee type";
       Class<?>[] groups() default {};
       Class<? extends Payload>[] payload() default {};
   }
   ```

   2. Implement the validator:

   ```java
   public class EmployeeTypeValidator implements ConstraintValidator<EmployeeType, String> {
       private static final Set<String> ALLOWED = Set.of("permanent", "contractual");
       public void initialize(EmployeeType constraint) { }
       public boolean isValid(String value, ConstraintValidatorContext context) {
           return value != null && ALLOWED.contains(value.toLowerCase());
       }
   }
   ```

   3. Use it in the entity:

   ```java
   public class Employee {
       private String name;
       @EmployeeType
       private String type;
       // getters/setters
   }
   ```

   **Rating:** 4/5
   *Justification:* The candidate described the high-level steps and retention/target usage but did not show the `@Constraint` metadata or full syntax. The example was implied but not explicit.

3. **Question:** What is caching in Spring Boot?

   **Candidate’s Answer (Brief):**
   “When a frequently run database query is expensive, you annotate methods with `@Cacheable` to store results in providers like Redis, so subsequent calls return data from cache instead of hitting the database. Use `@CachePut` to update cache and `@CacheEvict` to clear it.”

   **Correct Answer:**
   Spring Boot caching lets you store results of expensive method calls in a cache (e.g., Redis, Ehcache). Annotate methods with:

   * `@Cacheable("cacheName")` to cache return values.
   * `@CachePut("cacheName")` to update the cache without skipping method execution.
   * `@CacheEvict("cacheName")` to remove entries when data changes.

   **Rating:** 5/5
   *Justification:* The candidate correctly explained purpose, annotations, and caching providers.

4. **Question:** How does inter-service communication happen between microservices, and what are the various ways?

   **Candidate’s Answer (Brief):**
   “Synchronous via REST (using `RestTemplate`, Feign client, or reactive `WebClient` for nonblocking). Asynchronous via message brokers like RabbitMQ or Kafka, where producers send messages and consumers subscribe. Also event-driven approaches where services publish/subscribe events.”

   **Correct Answer:**
   Inter-service communication can be:

   * **Synchronous (HTTP/REST):**

     * `RestTemplate` (blocking) or `WebClient` (nonblocking) in Spring WebFlux.
     * Feign clients (declarative REST).
   * **Asynchronous (Messaging):**

     * Message brokers (RabbitMQ, Kafka) using publish/subscribe patterns.
     * Event-driven (services emit events, others subscribe).
       Choose based on latency, throughput, and coupling requirements.

   **Rating:** 5/5
   *Justification:* The candidate covered both synchronous and asynchronous mechanisms and mentioned appropriate Spring tools.

5. **Question:** In Spring Boot, how can we customize a specific auto-configuration?

   **Candidate’s Answer (Brief):**
   “You can override defaults in `application.properties`/`application.yml` or define custom beans in a `@Configuration` class. For example, customize the default DataSource there. You can also exclude Tomcat in `pom.xml` and include another server.”

   **Correct Answer:**
   You can customize auto-configuration by:

   * Setting properties in `application.properties`/`application.yml` (e.g., `spring.datasource.url`).
   * Defining your own `@Bean` in a `@Configuration` class to override the auto-configured bean.
   * Excluding specific auto-configurations with `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})`.
   * Adjusting dependencies in `pom.xml` to exclude default servlet containers (e.g., exclude Tomcat to use Jetty).

   **Rating:** 4/5
   *Justification:* The candidate mentioned property overrides and configuration class, and excluding Tomcat. They did not explicitly mention using `exclude` in `@SpringBootApplication`, but the overall approach was correct.

6. **Question:** What are the different bean scopes available in Spring Boot?

   **Candidate’s Answer (Brief):**
   “`singleton` (default): one instance per container. `prototype`: a new instance per request. `request`: bean lives for the duration of an HTTP request. `session`: bean lives for the HTTP session. `websocket`: bean lives for the WebSocket session.”

   **Correct Answer:**
   Standard Spring scopes:

   * `singleton` (one instance per Spring IoC container)
   * `prototype` (new instance every time requested)
   * `request` (one instance per HTTP request)
   * `session` (one instance per HTTP session)
   * `application` (one instance per ServletContext)
   * `websocket` (one instance per WebSocket session)

   **Rating:** 4/5
   *Justification:* The candidate covered `singleton`, `prototype`, `request`, `session`, and `websocket`. They omitted `application`, but covered the main ones.

7. **Question:** Can we implement a custom scope? How?

   **Candidate’s Answer (Brief):**
   “I have no idea.”

   **Correct Answer:**
   To implement a custom scope:

   1. Create a class implementing `org.springframework.beans.factory.config.Scope`, defining `get()`, `remove()`, etc.
   2. Register it with the `ConfigurableBeanFactory` in a `BeanFactoryPostProcessor`:

   ```java
   @Component
   public class CustomScopeConfigurer implements BeanFactoryPostProcessor {
       public void postProcessBeanFactory(ConfigurableListableBeanFactory bf) {
           bf.registerScope("myScope", new MyCustomScope());
       }
   }
   ```

   3. Use `@Scope("myScope")` on beans.

   **Rating:** 1/5
   *Justification:* The candidate did not know how to create a custom scope.

8. **Question:** What is the difference between `@SpringBootApplication` and `@EnableAutoConfiguration`?

   **Candidate’s Answer (Brief):**
   “`@EnableAutoConfiguration` is one of the annotations that `@SpringBootApplication` includes. `@SpringBootApplication` combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.”

   **Correct Answer:**

   * `@EnableAutoConfiguration` triggers Spring Boot’s auto-configuration based on classpath dependencies.
   * `@SpringBootApplication` is a meta-annotation that includes `@EnableAutoConfiguration`, `@ComponentScan`, and `@Configuration`.

   **Rating:** 5/5
   *Justification:* The candidate accurately described the relationship and composition.

9. **Question:** What is the difference between service registry and service discovery, and how do they work with each other?

   **Candidate’s Answer (Brief):**
   “The service registry is a database that stores all microservice instances and their locations (IP/port). Each service registers itself upon startup. Other services query the registry to discover available instances. When a service goes down, it’s removed from the registry.”

   **Correct Answer:**

   * **Service Registry:** A central repository (e.g., Eureka, Consul) where services register their network locations.
   * **Service Discovery:** The process by which a service queries the registry to find other service instances at runtime.
     Together, services register themselves with the registry, and consumers discover available providers via queries to that registry.

   **Rating:** 5/5
   *Justification:* The candidate explained the registry’s role and how discovery queries it, including registration and removal.

10. **Question:** What is the Saga design pattern in microservices?

    **Candidate’s Answer (Brief):**
    “A Saga is a sequence of local transactions across multiple services. If one step fails, a compensating transaction undoes previous steps. There are two types: choreography (each service reacts to events) and orchestration (a central orchestrator manages the saga).”

    **Correct Answer:**
    A Saga manages distributed transactions by breaking them into a series of local transactions. Two approaches:

    * **Choreography:** Each service listens for events and performs its transaction, then publishes the next event.
    * **Orchestration:** A centralized orchestrator service invokes each local transaction in order and triggers compensations on failure.

    **Rating:** 5/5
    *Justification:* The candidate correctly described Saga, compensating transactions, and the two styles.

11. **Question:** What is idempotency in microservices?

    **Candidate’s Answer (Brief):**
    “Idempotent operations (GET, PUT, DELETE) can be repeated without side effects. Repeated POSTs can create duplicates, so they are not idempotent.”

    **Correct Answer:**
    An idempotent operation yields the same result no matter how many times it’s performed. For HTTP:

    * **GET, PUT, DELETE** are idempotent (multiple calls have no additional effect).
    * **POST** is not idempotent (multiple calls may create multiple records).

    **Rating:** 5/5
    *Justification:* The candidate correctly explained idempotency in the context of HTTP methods.

12. **Question:** What is the superclass of all Java classes?

    **Candidate’s Answer (Brief):**
    “`Object` class.”

    **Correct Answer:**
    `java.lang.Object`.

    **Rating:** 5/5
    *Justification:* Correct.

13. **Question:** In which package is `Object` found?

    **Candidate’s Answer (Brief):**
    “`java.lang`.”

    **Correct Answer:**
    `java.lang`.

    **Rating:** 5/5
    *Justification:* Correct.

14. **Question:** Can you name some methods inside `Object`?

    **Candidate’s Answer (Brief):**
    “`equals()`, `hashCode()`, `clone()`, `notify()`, `notifyAll()`, `wait()`, `toString()`.”

    **Correct Answer:**
    Common methods include `equals(Object)`, `hashCode()`, `toString()`, `clone()`, `getClass()`, `notify()`, `notifyAll()`, `wait()`, `finalize()`.

    **Rating:** 5/5
    *Justification:* The candidate listed several major methods; acceptable recall.

15. **Question:** What OOP concepts are you aware of?

    **Candidate’s Answer (Brief):**
    “Encapsulation, inheritance, polymorphism, abstraction.”

    **Correct Answer:**
    The four pillars: encapsulation, inheritance, polymorphism, and abstraction.

    **Rating:** 5/5
    *Justification:* Correct.

16. **Question:** How can you prove that a given class follows inheritance and polymorphism?

    **Candidate’s Answer (Brief):**
    “All classes implicitly extend `Object`, so inheritance exists. Polymorphism is shown via method overriding (e.g., overriding `equals()` or `hashCode()` from `Object`).”

    **Correct Answer:**

    * **Inheritance:** Every class in Java inherits (directly or indirectly) from `Object`. So even if not explicit, `class Employee` inherits all methods from `Object`.
    * **Polymorphism:** You can override `Object` methods (like `equals()`) or overload methods within the class. Any overridden method demonstrates runtime polymorphism by letting a subclass or instance-specific implementation be invoked.

    **Rating:** 4/5
    *Justification:* The candidate correctly pointed out implicit inheritance from `Object` and method overriding. They could also mention method overloading as compile-time polymorphism, but their answer was acceptable.

17. **Question:** In which scenario would you use `ArrayList` vs. `LinkedList`?

    **Candidate’s Answer (Brief):**
    “Use `ArrayList` when you need frequent random access. Use `LinkedList` when you need frequent insertions or deletions in the middle, since it uses a linked structure.”

    **Correct Answer:**

    * **`ArrayList`:** Backed by a dynamic array, O(1) random access, O(n) insertion/deletion (due to shifting). Best if reads far outnumber writes.
    * **`LinkedList`:** Doubly-linked list, O(n) access (no index-based random access), but O(1) insertion/deletion given a node reference. Best if many insertions/deletions.

    **Rating:** 5/5
    *Justification:* The candidate correctly contrasted access vs. modification performance.

18. **Question:** What is the difference between `HashMap` and `ConcurrentHashMap`?

    **Candidate’s Answer (Brief):**
    “`HashMap` is not thread-safe and allows null keys/values. `ConcurrentHashMap` is thread-safe, does not allow null keys or values, and has higher overhead so is slower in single-threaded contexts.”

    **Correct Answer:**

    * **`HashMap`:** Not synchronized (not thread-safe), allows one null key and multiple null values.
    * **`ConcurrentHashMap`:** Thread-safe, internally uses segment/bucket locking (or CAS in Java 8+) for concurrency, does not allow null keys or values. Slightly slower than `HashMap` in single-threaded usage but safe for concurrent access.

    **Rating:** 5/5
    *Justification:* The candidate correctly described thread safety, null allowance, and performance trade-offs.

19. **Question:** How would you remove duplicates from a list while preserving order?

    **Candidate’s Answer (Brief):**
    “Add all list elements to a `LinkedHashSet` (which preserves insertion order), then convert back to an `ArrayList`.”

    **Correct Answer:**
    Use a `LinkedHashSet` (preserves insertion order, eliminates duplicates), e.g.:

    ```java
    List<String> list = …;
    List<String> noDuplicates = new ArrayList<>(new LinkedHashSet<>(list));
    ```

    **Rating:** 5/5
    *Justification:* Correct approach.

20. **Question:** Do you know about `Vector`?

    **Candidate’s Answer (Brief):**
    “`Vector` appeared in early Java (1.2). It’s synchronized (thread-safe) but less efficient than `ArrayList`. It allows null values and one null key.”

    **Correct Answer:**
    `Vector` is a synchronized, thread-safe dynamic array introduced in Java 1.0 (enhanced by Java 1.2 to implement the `List` interface). It grows its capacity as needed but synchronizes every method, leading to overhead. `ArrayList` is preferred in most cases.

    **Rating:** 4/5
    *Justification:* The candidate mentioned synchronization and efficiency. They noted null allowance, though “one null key” is not meaningful for a list; minor inaccuracy but core idea correct.

21. **Question:** What is the `volatile` keyword in Java?

    **Candidate’s Answer (Brief):**
    “`volatile` indicates a variable may be modified by multiple threads. It guarantees visibility of the most recent value across threads but does not guarantee atomicity.”

    **Correct Answer:**
    `volatile` ensures that reads/writes to the variable go directly to main memory (no thread-local caching). It provides visibility guarantees but does not make compound actions atomic.

    **Rating:** 5/5
    *Justification:* Correct description of visibility and lack of atomicity.

22. **Question:** What is the `transient` keyword in Java?

    **Candidate’s Answer (Brief):**
    “`transient` marks a field to be skipped during serialization. For instance, you mark a password field `transient` so it isn’t saved to the serialized form.”

    **Correct Answer:**
    When a field is marked `transient`, the Java serialization mechanism (`Serializable`) ignores that field and does not include it in the serialized byte stream.

    **Rating:** 5/5
    *Justification:* Correct.

23. **Question:** What is the difference between `StringBuilder` and `StringBuffer`?

    **Candidate’s Answer (Brief):**
    “Both are mutable. `StringBuffer` is synchronized (thread-safe); `StringBuilder` is not synchronized (not thread-safe), so it’s faster.”

    **Correct Answer:**

    * `StringBuffer`: Thread-safe (synchronized methods) but slower due to locking.
    * `StringBuilder`: Not thread-safe (no synchronization), faster in single-threaded contexts.

    **Rating:** 5/5
    *Justification:* Correct.

24. **Question:** What is the difference between `==` and `.equals()` in Java?

    **Candidate’s Answer (Brief):**
    “`==` tests if two references point to the same object (same memory). `.equals()` compares object content/values.”

    **Correct Answer:**
    `==` compares reference identity (whether both variables refer to the exact same object). `.equals()` is a method that, when properly overridden, compares logical equality (content) of objects.

    **Rating:** 5/5
    *Justification:* Correct.

25. **Question:** What are indexes in SQL, and how do you create one?

    **Candidate’s Answer (Brief):**
    “Indexes are database objects that speed up record retrieval. You create one by `CREATE INDEX index_name ON table_name(column_name);`.”

    **Correct Answer:**
    An index is a database structure (often a B-tree or other structure) that allows faster lookup by key. You create it with:

    ```sql
    CREATE INDEX idx_column ON table_name(column_name);
    ```

    **Rating:** 5/5
    *Justification:* Correct.

26. **Question:** How does indexing work internally?

    **Candidate’s Answer (Brief):**
    “When you create an index, the database generates an internal structure (e.g., B-tree or hash table). Queries then use that structure to avoid full table scans, jumping directly to matching rows.”

    **Correct Answer:**
    Internally, most relational databases use a B-tree (or B+-tree) for indexes. The index stores key values and pointers to data rows. On a query, the optimizer uses the index to traverse the tree (O(log n)) and directly locate matching rows instead of scanning all rows. Some databases also support hash indexes for equality searches.

    **Rating:** 4/5
    *Justification:* The candidate mentioned underlying structures (“B3 hash table” interpreted as B-tree or hash). They conveyed the idea of avoiding full scans but slightly misnamed the structure. Overall correct concept.

---

**Overall Feedback:**
The candidate demonstrated solid knowledge of Spring Boot features (bean injection, caching, auto-configuration), microservices communication, and core Java (collections, keywords, OOP). Minor gaps include implementing a custom scope, deeper Spring Boot auto-configuration nuances, and precise internal index structures. However, their answers were mostly accurate and well-articulated.
