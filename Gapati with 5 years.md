1. **Question:** “So please tell me about yourself.”
   **Candidate’s Answer (Brief):**
   Introduced themselves as Gapati with five-plus years of experience as a Java/Python developer. Mentioned working primarily with Java, Spring Boot (referred to as “Springwood”), microservices, MySQL, JUnit for testing, Jenkins for CD, version control (Git), and Hibernate/JPA.
   **Correct Answer:**
   A concise summary covering: total years of experience; primary roles/responsibilities; key technologies (e.g., Java 17, Spring Boot, Hibernate/JPA, MySQL/PostgreSQL, Docker/Kubernetes, messaging such as Kafka/RabbitMQ); tools used (e.g., Git, Jenkins, Maven/Gradle); and a high-level note on recent projects (e.g., microservices design, REST API development).
   **Rating:** 3/5
   *Justification:* The candidate covered most relevant technologies and years of experience but mixed in minor inaccuracies (“Springwood” instead of “Spring Boot”) and did not highlight recent project details or cloud/container experience explicitly.

2. **Question:** “Which Java version are you using right now?”
   **Candidate’s Answer (Brief):**
   “Currently I’m working with Java 17.”
   **Correct Answer:**
   Answering “Java 17” is correct; if pressed, they could add that Java 17 is a Long Term Support (LTS) release with features like records, sealed classes, pattern matching, etc.
   **Rating:** 5/5
   *Justification:* The candidate answered correctly and concisely.

3. **Question:** “What is the difference between Java 8 and Java 17?”
   **Candidate’s Answer (Brief):**
   Mentioned “CD classes” (intending sealed classes) to control subclassing, improved “switch statement” (cleaner and safer expressions), “model data classes” (referring to records), in addition to Java 8 features (functional interfaces, lambda expressions, stream operations, Optional).
   **Correct Answer:**
   Major differences include:

   * **Java 8 (2014)** introduced lambdas, default/static methods in interfaces, Stream API, `java.time` API, `Optional`, Nashorn JS engine, and method references.
   * **Java 17 (2021, LTS)** adds: sealed classes (restricts which classes can extend/implement), records (compact syntax for data classes), pattern matching for `instanceof` and switch, text blocks (multiline strings), enhanced switch expressions, `Nullable` types inference improvements, improved garbage collectors (e.g., G1, ZGC), and new APIs (e.g., `java.nio.file.Files` enhancements), plus deprecations/removals (e.g., Nashorn).
     **Rating:** 3/5
     *Justification:* The candidate identified sealed classes, switch improvements, and records but phrased them unclearly (“CD classes,” “model data classes”). They recalled Java 8 features but omitted text blocks, pattern matching, or GC improvements.

4. **Question:** “What is the difference between a normal interface and a functional interface?”
   **Candidate’s Answer (Brief):**
   “A functional interface holds one abstract method and any number of default/static methods for lambda expressions, whereas a normal interface can have multiple abstract methods and cannot be used directly with lambdas.”
   **Correct Answer:**

   * A **Functional Interface** (annotated `@FunctionalInterface` or meeting its criteria) has exactly one abstract method (the “functional method”) and may include any number of default or static methods. It can serve as the target for lambda expressions or method references.
   * A **Normal Interface** can declare multiple abstract methods (and default or static methods) and is not intended as a lambda target. It may have no `@FunctionalInterface` annotation.
     **Rating:** 4/5
     *Justification:* The candidate’s distinction is correct, though they said “holds some static method and any number of default and static methods” (redundant phrasing). They understood the single-abstract-method rule and lambda applicability.

5. **Question:** “What is the use of static and default methods in interfaces?”
   **Candidate’s Answer (Brief):**
   “Static methods are for helper/utility logic. Default methods provide a method body inside interfaces for backward compatibility so existing implementations need not change.”
   **Correct Answer:**

   * **Static methods** in interfaces act as helper or utility methods callable on the interface itself (e.g., `InterfaceName.helperMethod()`). They do not belong to the implementing classes.
   * **Default methods** allow interfaces to provide a concrete implementation, enabling interface evolution without breaking existing implementations. Classes implementing the interface inherit default implementations unless overridden.
     **Rating:** 5/5
     *Justification:* The candidate captured both roles accurately and concisely.

6. **Question:** “What is the importance of lambda expressions?”
   **Candidate’s Answer (Brief):**
   “Lambdas provide functional programming support—anonymous functions can be passed around as objects.”
   **Correct Answer:**
   Lambda expressions enable concise expression of single-method interfaces, facilitating functional-style operations such as passing behavior (functions) as parameters. They reduce boilerplate code (no need for anonymous inner classes), ease parallel collection processing via Streams, and improve code readability.
   **Rating:** 4/5
   *Justification:* The candidate identified that lambdas represent anonymous functions and support functional programming. They could have added that lambdas reduce verbosity compared to inner classes.

7. **Question:** “How many types of predefined functional interfaces are there? Can you name some?”
   **Candidate’s Answer (Brief):**
   Named `Predicate`, `Function`, `Consumer`, `Supplier`, and `BiFunction`.
   **Correct Answer:**
   Common predefined functional interfaces (in `java.util.function`) include:

   * `Predicate<T>` (method `boolean test(T t)`)
   * `Function<T,R>` (method `R apply(T t)`)
   * `Supplier<T>` (method `T get()`)
   * `Consumer<T>` (method `void accept(T t)`)
   * `BiPredicate<T,U>` (method `boolean test(T t, U u)`)
   * `BiFunction<T,U,R>` (method `R apply(T t, U u)`)
   * `UnaryOperator<T>` (extends `Function<T,T>`)
   * `BinaryOperator<T>` (extends `BiFunction<T,T,T>`)
     **Rating:** 3/5
     *Justification:* The candidate named five of the most common ones but missed `UnaryOperator`, `BinaryOperator`, `BiPredicate`, and didn’t explain differences or use cases.

8. **Question:** “Why are we using `Optional` in Java 8? What is its importance?”
   **Candidate’s Answer (Brief):**
   “Optional provides a way to handle null; it may or may not contain a value, offering a more expressive way than using null directly.”
   **Correct Answer:**
   `Optional<T>` is a container object that may or may not hold a non-null value. It helps avoid `NullPointerException` by forcing explicit handling of absent values (`Optional.empty()`), or returning a default via `orElse()`. It encourages developers to check presence (`isPresent()`) or use functional-style operations (`map()`, `flatMap()`, `filter()`).
   **Rating:** 5/5
   *Justification:* The candidate captured the essential rationale: to handle nullability more expressively and safely.

9. **Question:** “Can you give the names of methods in `Optional`?”
   **Candidate’s Answer (Brief):**
   Listed (albeit roughly) methods: `empty()`, `of()`, `isPresent()`, `get()`, and hinted at a default value method (`orElse()`).
   **Correct Answer:**
   Common `Optional` methods include:

   * `static <T> Optional<T> empty()`
   * `static <T> Optional<T> of(T value)`
   * `static <T> Optional<T> ofNullable(T value)`
   * `boolean isPresent()`
   * `T get()`
   * `T orElse(T other)`
   * `T orElseGet(Supplier<? extends T> other)`
   * `<U> Optional<U> map(Function<? super T,? extends U> mapper)`
   * `Optional<T> filter(Predicate<? super T> predicate)`
   * `void ifPresent(Consumer<? super T> action)`
   * `T orElseThrow(Supplier<? extends X> exceptionSupplier)`
     **Rating:** 3/5
     *Justification:* The candidate named most of the core ones but missed `ofNullable()`, `orElseGet()`, `map()`, `filter()`, and `ifPresent()`. They got the basics but lacked completeness.

10. **Question:** “What is a method reference and how does it work?”
    **Candidate’s Answer (Brief):**
    “Method reference is a shorthand for a lambda expression when you just call an existing method directly. You pass the method as an argument.”
    **Correct Answer:**
    A method reference (syntax `ClassName::methodName` or `instance::methodName`) is a compact way to refer to an existing method or constructor instead of writing a lambda. For example, `list.forEach(System.out::println)` is equivalent to `list.forEach(x -> System.out.println(x))`. It can refer to static methods, instance methods, or constructors.
    **Rating:** 4/5
    *Justification:* The candidate correctly described the concept; they could have given an explicit syntax example, but the core idea is right.

11. **Question:** “What is the Stream API?”
    **Candidate’s Answer (Brief):**
    “Stream API lets us process collections in a functional style using a pipeline of operations on a sequence of elements, producing a result.”
    **Correct Answer:**
    The Stream API (`java.util.stream`) provides a way to perform functional-style operations on sequences of elements (e.g., collections, arrays). It supports a chain of **intermediate operations** (e.g., `filter()`, `map()`, `sorted()`) and a **terminal operation** (e.g., `collect()`, `forEach()`, `reduce()`), enabling declarative data processing with optional parallelization.
    **Rating:** 4/5
    *Justification:* The candidate captured the purpose and pipeline concept. They could have highlighted that streams are lazily evaluated and can be parallelized.

12. **Question:** “What is the difference between a Stream and a parallel Stream?”
    **Candidate’s Answer (Brief):**
    “Parallel Stream runs tasks in parallel for faster processing of large datasets by utilizing multiple CPU cores. To use it, convert an existing Stream to parallel.”
    **Correct Answer:**

    * A **sequential stream** processes elements one by one on a single thread, maintaining order.
    * A **parallel stream** divides data into substreams processed concurrently on multiple threads (using the Fork/Join common pool), then merges results. Parallelization can improve performance for CPU-bound operations on large datasets, but may introduce overhead or require thread-safe operations.
      **Rating:** 3/5
      *Justification:* The candidate understood the core idea but did not mention the underlying Fork/Join mechanism, lazy evaluation difference, or potential thread-safety concerns.

13. **Question:** “What is the difference between `HashMap` and `ConcurrentHashMap`?”
    **Candidate’s Answer (Brief):**
    “`HashMap` is not thread-safe—good for single-threaded environments—and allows null keys/values. `ConcurrentHashMap` is thread-safe, allows multiple threads to read/write without locking the entire map, uses segment-level (bucket-level) locks, and does not allow null keys or null values.”
    **Correct Answer:**

    * **`HashMap`**: Non-synchronized, not thread-safe; allows one null key and multiple null values; may throw `ConcurrentModificationException` if modified during iteration.
    * **`ConcurrentHashMap`**: Thread-safe; in Java 8 it uses a lock per bin or employs CAS for updates, allowing high concurrency (reads are lock-free, writes lock only a portion of the table). Does **not** permit null keys or null values. Offers atomic operations (e.g., `computeIfAbsent()`, `putIfAbsent()`).
      **Rating:** 5/5
      *Justification:* The candidate accurately identified thread-safety differences, null-permission rules, and segment/bucket locking concept.

14. **Question:** “Suppose I give two scenarios—`LinkedHashMap` and `HashMap`. How do you distinguish between these two? What is the impact on read and write operations, e.g., if something you want to write to the database or read from it, which one would you use?”
    **Candidate’s Answer (Brief):**
    “For read/write heavy operations, use `HashMap`—it doesn’t preserve order and is fast. `LinkedHashMap` maintains insertion order (or access order if configured) but is slightly slower due to its linked-list overhead.”
    **Correct Answer:**

    * **`HashMap`**: Unordered; offers average O(1) time for `get`/`put` operations. Best when order does not matter and you need maximum performance.
    * **`LinkedHashMap`**: Maintains a doubly linked list of entries to preserve insertion order (or optionally access order). Slightly higher overhead on `put` and iteration but still O(1) for `get`/`put`. Use when you need predictable iteration order (e.g., LRU caches).
      **Rating:** 4/5
      *Justification:* The candidate correctly contrasted order preservation and performance implications. They didn’t mention specific use cases (like LRU), but overall accurate.

15. **Question:** “You know dynamic binding and static binding?”
    **Candidate’s Answer (Brief):**
    “Dynamic binding and static binding refer to runtime polymorphism and compile-time polymorphism. Compile-time polymorphism applies to static methods, final methods, overloaded methods, and private methods, based on reference type.”
    **Correct Answer:**

    * **Static (compile-time) binding**: Method calls are resolved at compile time, e.g., method overloading, static methods, and final/private methods. The compiler determines which method to invoke based on the reference and parameter types.
    * **Dynamic (runtime) binding**: Method calls are resolved at runtime, e.g., overridden instance methods. The JVM determines the actual implementation based on the runtime object’s class.
      **Rating:** 4/5
      *Justification:* The candidate understood that static binding is compile-time (overloaded, static, final, private methods) and dynamic binding is runtime (overridden methods). They were concise and correct.

16. **Question:** “Suppose I want to override the static `main` method or overload the static `main` method. Can it be overridden?”
    **Candidate’s Answer (Brief):**
    “Static methods can be overloaded in Java but cannot be overridden.”
    **Correct Answer:**
    In Java, **static methods cannot be overridden** (they belong to the class, not to instances). You can **overload** static methods (same name, different parameter list), but overriding (runtime polymorphism) does not apply to static.
    **Rating:** 5/5
    *Justification:* The candidate correctly distinguished overloading vs. overriding for static methods.

17. **Question:** “Do you know the eager loading and lazy loading concept in Java?”
    **Candidate’s Answer (Brief):**
    “Eager loading refers to initializing objects immediately, e.g., class-level methods and variables loaded at class load time. Lazy loading delays initialization until needed.”
    **Correct Answer:**

    * **Eager loading**: Objects or resources are initialized upfront (e.g., static fields in a class are loaded when the class is first loaded). In JPA/Hibernate, “eager fetching” means related entities are fetched immediately in the same query.
    * **Lazy loading**: Objects or resources are initialized only when accessed for the first time. In JPA/Hibernate, “lazy fetching” defers loading related entities until their getters are invoked, reducing initial query cost.
      **Rating:** 2/5
      *Justification:* The candidate correctly stated the general idea of immediate vs. delayed initialization but did not mention the specific JPA context (eager vs. lazy fetching) nor clarify class-level vs. object-level loading.

18. **Question:** “Do you know how metaspace works in Java 8 and Java 17?”
    **Candidate’sAnswer (Brief):**
    “Metaspace replaced PermGen; it grows automatically. The old PermGen size (‘com’ size causing memory error) can cause OOM, but metaspace avoids that by dynamically expanding.”
    **Correct Answer:**
    In Java 8 and later, **Metaspace** replaced the old PermGen. Key points:

    * It stores class metadata (class definitions, method metadata) outside the heap, in native memory.
    * Metaspace auto-resizes by default (capped by OS memory), eliminating `java.lang.OutOfMemoryError: PermGen space`.
    * You can still cap metaspace growth via `-XX:MaxMetaspaceSize`.
      **Rating:** 3/5
      *Justification:* The candidate knew Metaspace replaced PermGen and grows automatically, but their phrasing (“com size causing memory error”) was unclear, and they did not mention `-XX:MaxMetaspaceSize` or native memory context.

19. **Question:** “What is the difference between synchronous API and asynchronous API?”
    **Candidate’s Answer (Brief):**
    “Asynchronous API runs tasks in the background without blocking the main thread, improving response and throughput in microservices. We use `CompletableFuture`, thread pools, `TaskExecutor`.”
    **Correct Answer:**

    * A **synchronous** API blocks the caller until the operation completes (e.g., a REST call that returns a response before proceeding).
    * An **asynchronous** API returns immediately (often a `Future` or callback), allowing the operation to proceed in the background. The main thread can continue other work. In Spring, you might use `@Async` with `CompletableFuture` or reactive WebFlux (`Mono`/`Flux`). This improves throughput and responsiveness for I/O-bound or long-running tasks.
      **Rating:** 4/5
      *Justification:* The candidate correctly explained the difference and named relevant classes (`CompletableFuture`, thread pools). They could have contrasted use cases (e.g., I/O vs. CPU-bound).

20. **Question:** “Which class/interface do you use when writing synchronous versus asynchronous code?”
    **Candidate’s Answer (Brief):**
    “I’ve used the Executor framework and `CompletableFuture`, as well as `Callable` and `Future`.”
    **Correct Answer:**

    * For **synchronous** operations in Spring, you typically use regular method calls or synchronous `RestTemplate`.
    * For **asynchronous**, you can use the **Executor** framework (`ExecutorService`, `Callable`, `Future`) or, in Spring, annotate methods with `@Async` (returns `CompletableFuture<T>`). In reactive code, use `Mono`/`Flux` (WebFlux).
      **Rating:** 4/5
      *Justification:* The candidate mentioned the right classes (`CompletableFuture`, `Callable`, Executor framework). They could have clarified which exactly apply to synchronous vs. asynchronous.

21. **Question:** “Suppose I tell you to write a Spring Boot application from scratch—what are the first and last steps to get it ready to run and test?”
    **Candidate’s Answer (Brief):**
    “First, create REST endpoints by writing controller classes. Next, create the service layer for business logic. Define model classes (entities) and set up repositories for database connection. Finally, configure application properties and run/test.”
    **Correct Answer:**
    A typical set of steps:

    1. **Initialize Project**: Use Spring Initializr or build tool (Maven/Gradle) to generate a Spring Boot project with required dependencies (Web, JPA, etc.).
    2. **Define Entities & Repositories**: Create JPA entity classes and repository interfaces (e.g., `JpaRepository`).
    3. **Implement Services**: Write service classes for business logic.
    4. **Create Controllers**: Define REST controllers with request mappings.
    5. **Configure Application**: Set `application.properties` or `application.yml` (DB URL, credentials, server port).
    6. **Run & Test**: Start the application (e.g., `mvn spring-boot:run`), write unit/integration tests (e.g., with JUnit, MockMvc).
    7. **Package & Deploy**: Build a runnable JAR/WAR and deploy locally or to cloud/containers.
       **Rating:** 4/5
       *Justification:* The candidate hit most key layers (controllers, services, entities/repositories) but did not mention project initialization (Spring Initializr) or explicit testing tools; however, the sequence is broadly correct.

22. **Question:** “What is the difference between `@Bean` and `@Component`?”
    **Candidate’s Answer (Brief):**
    “`@Bean` is used on methods inside configuration classes to create bean objects manually. `@Component` is used on classes so Spring automatically detects and registers them via component scan.”
    **Correct Answer:**

    * **`@Component`**: Stereotype annotation placed on a class. During component scanning, Spring auto-detects and registers it as a bean.
    * **`@Bean`**: Placed on a method within a `@Configuration` class. Spring executes that method to produce and register the return object as a bean. Use `@Bean` when you need to explicitly configure third-party classes or fine-tune bean instantiation.
      **Rating:** 5/5
      *Justification:* The candidate’s answer is accurate and succinct.

23. **Question:** “What is the difference between `@Service` and `@Repository`?”
    **Candidate’s Answer (Brief):**
    “`@Service` is used for business logic classes; `@Repository` is used for data-access classes (interacting with the database). Both are specializations of `@Component`, but their purposes differ.”
    **Correct Answer:**

    * **`@Service`**: Indicates a service-layer class holding business logic. Spring may apply service-specific behaviors (e.g., transaction management).
    * **`@Repository`**: Indicates a DAO/data-access class. Spring applies exception translation to wrap database exceptions into Spring’s `DataAccessException` hierarchy. Both annotations register the class as a bean, but `@Repository` adds persistence-related semantics.
      **Rating:** 4/5
      *Justification:* The candidate correctly stated that `@Service` is for business logic and `@Repository` for data access, but they did not mention exception translation provided by `@Repository`.

24. **Question:** “Suppose you want to inject a dependency into a controller without using `@Autowired`. What alternative way can you initialize that dependency?”
    **Candidate’s Answer (Brief):**
    “Use constructor injection (define a constructor with the required bean parameter). Spring will automatically inject without needing `@Autowired`. You can also use setter injection.”
    **Correct Answer:**
    Alternatives to `@Autowired` field injection include:

    * **Constructor injection**: Declare a constructor with parameters for required beans. Spring (since 4.3) can auto-inject if there’s only one constructor, no `@Autowired` needed.
    * **Setter injection**: Provide a setter method annotated with `@Autowired` or rely on a single setter if using a compatible version.
    * **`@Inject`** (Javax), **`@Resource`** annotations.
      **Rating:** 5/5
      *Justification:* The candidate correctly identified constructor injection as an alternative and implied setter injection.

25. **Question:** “What is an API Gateway? How do you manage multiple APIs behind a single endpoint?”
    **Candidate’s Answer (Brief):**
    “An API Gateway centralizes routing, providing authentication, authorization, rate limiting, load balancing, and caching. It routes client requests to downstream microservices. You can use Spring Cloud Gateway or Zuul.”
    **Correct Answer:**
    An **API Gateway** sits between clients and microservices to:

    * Provide a **single entry point** for multiple services.
    * Offer **cross-cutting concerns**: authentication/authorization, rate limiting, request/response transformation, circuit breaking, and caching.
    * Route, aggregate, or transform requests to appropriate backend services.
    * In Spring, use **Spring Cloud Gateway** or **Netflix Zuul**. In cloud environments, can use AWS API Gateway, Kong, or Apigee.
      **Rating:** 5/5
      *Justification:* The candidate’s description was complete, mentioning core responsibilities and examples of implementation.

26. **Question:** “If you’re using Spring Cloud API Gateway dependencies, how do you centralize configuration/dependencies? Any mechanism?”
    **Candidate’s Answer (Brief):**
    “Use a Config Server and a parent POM for dependency management. With config server, you centralize application properties. Parent POM (dependency management) ensures consistent dependency versions across microservices.”
    **Correct Answer:**
    To centralize configuration in a Spring Cloud ecosystem:

    * Use **Spring Cloud Config Server** to store YAML/Properties for all microservices in a Git repository. Clients fetch their configuration at startup or on refresh.
    * Use a **parent BOM (Bill of Materials)** POM to manage consistent dependency versions (e.g., Spring Cloud BOM).
    * Apply **`dependencyManagement`** in the parent POM so microservices inherit the same versions.
      **Rating:** 4/5
      *Justification:* The candidate correctly mentioned Config Server and parent POM for dependency management, though they mixed “dependencies” vs. “configuration.” They did not explicitly mention BOM or Git back-end but got the core idea.

27. **Question:** “Explain service discovery. How does it work?”
    **Candidate’s Answer (Brief):**
    “Service registry lets services dynamically register themselves. A discovery service (e.g., Eureka) holds service instances. When a service needs another service, it queries the registry to get available instances and routes requests accordingly.”
    **Correct Answer:**

    * **Service Discovery**: Microservices register themselves (name, address, port) with a **Service Registry** (e.g., Eureka, Consul, Zookeeper).
    * **Client-side load balancing**: A client or gateway queries the registry to find service instances and perform load balancing (e.g., Ribbon, Spring Cloud LoadBalancer).
    * **Server-side discovery**: An API gateway queries the registry and routes to a healthy instance.
    * Periodic heartbeats keep the registry updated with active instances.
      **Rating:** 5/5
      *Justification:* The candidate captured the dynamic registration and lookup process and mentioned Eureka specifically.

28. **Question:** “When calling one service’s API from another service in a microservices setup, what mechanism do you use in Spring Boot?”
    **Candidate’s Answer (Brief):**
    “Use `RestTemplate` or `WebClient`.”
    **Correct Answer:**

    * **Synchronous**: Use `RestTemplate` (blocking) or, in Spring 5+, `WebClient` (reactive, non-blocking).
    * **Declarative**: Use **OpenFeign** clients (`@FeignClient`) for interface-based HTTP calls.
      **Rating:** 4/5
      *Justification:* The candidate correctly named both `RestTemplate` and `WebClient`. They could have mentioned Feign as an alternative but are acceptable.

29. **Question:** “What are the advantages of using Spring Boot compared to the older Spring MVC framework?”
    **Candidate’s Answer (Brief):**
    “Spring Boot provides auto-configuration, embedded servers (Tomcat/Jetty), eliminates XML configuration, offers starter dependencies, and includes Actuator for metrics and health checks.”
    **Correct Answer:**

    * **Auto-configuration**: Automatically configures beans based on classpath and properties.
    * **Starter dependencies**: Simplifies dependency management with curated “starters” (e.g., `spring-boot-starter-web`).
    * **Embedded server**: Includes embedded Tomcat/Jetty/Undertow—no need to deploy as a WAR.
    * **Reduced configuration**: Minimal or zero XML; properties and auto-scanning reduce boilerplate.
    * **Actuator**: Built-in metrics, health endpoints, monitoring.
      **Rating:** 5/5
      *Justification:* The candidate covered all key advantages in a concise manner.

30. **Question:** “What is the role of `JpaRepository`?”
    **Candidate’s Answer (Brief):**
    Did not explicitly answer the first part; merged it into the next question.
    **Correct Answer:**
    `JpaRepository<T, ID>` is a Spring Data interface extending `PagingAndSortingRepository`, which in turn extends `CrudRepository`. It provides CRUD operations, pagination and sorting methods, and JPA-specific methods like `flush()`, `saveAndFlush()`, `getOne()`, and support for query derivation. It reduces boilerplate DAO code by auto-implementing common data-access methods.
    **Rating:** 1/5
    *Justification:* The candidate failed to define `JpaRepository`’s role, instead focusing on caching in the next question. They did not explicitly state that `JpaRepository` offers JPA-specific CRUD and pagination/sorting.

31. **Question:** “What is the difference between `CrudRepository` and `JpaRepository`?”
    **Candidate’s Answer (Brief):**
    “`CrudRepository` offers only basic CRUD operations. `JpaRepository` offers caching (second-level cache) capabilities, which must be enabled in Hibernate config.”
    **Correct Answer:**

    * **`CrudRepository<T, ID>`**: Provides generic CRUD operations (`save()`, `findById()`, `delete()`, etc.).
    * **`JpaRepository<T, ID>`**: Extends `CrudRepository` and `PagingAndSortingRepository`, adding JPA-specific methods like `flush()`, `saveAndFlush()`, `getOne()`, and methods for pagination and sorting. It does not itself enable second-level cache—that must be configured via JPA/Hibernate properties.
      **Rating:** 2/5
      *Justification:* The candidate correctly noted that `CrudRepository` is basic CRUD and `JpaRepository` offers extra features, but incorrectly attributed second-level caching as a built-in distinguishing feature (it’s a JPA/Hibernate configuration, not a repository interface difference). They did not mention pagination/sorting or JPA-specific methods.

32. **Question:** “In the database (Oracle/MySQL), when would you write a stored procedure versus a stored function? What scenario would lead you to recommend a procedure over a function?”
    **Candidate’s Answer (Brief):**
    “Procedures are precompiled stored code performing insert/update or complex operations and do not return a value; functions return a value (usable in SELECT). Use procedures for multiple operations or performance optimization to reduce Java layer cost; functions for complex queries that return a value.”
    **Correct Answer:**

    * **Stored Procedure**: A PL/SQL block precompiled in the database that can perform DML (INSERT/UPDATE/DELETE) and other logic. It may return zero, one, or many result sets via OUT parameters. Use when you need to perform multiple operations, encapsulate business logic (e.g., batch updates), or reduce network round trips.
    * **Stored Function**: Returns a single value and can be invoked in SQL statements (e.g., `SELECT my_function(...)`). Use if you need a reusable expression or value calculation within queries. Functions must not modify database state (in standard practice) and are typically used in SELECT, WHERE, or computed columns.
      **Rating:** 4/5
      *Justification:* The candidate understood that procedures do multiple operations and functions return a value, but said that functions “impact Java layer cost” without clarifying they can be used within SQL. Overall, the scenario usage is correct.

33. **Question:** “How many types of joins do we have?”
    **Candidate’s Answer (Brief):**
    “Inner join, outer join, left join, right join, self join, and union all.”
    **Correct Answer:**
    Standard join types in SQL are:

    * **Inner Join** (only matching rows)
    * **Left (Outer) Join** (all from left, matching from right)
    * **Right (Outer) Join** (all from right, matching from left)
    * **Full (Outer) Join** (all rows from both sides, with NULLs where no match)
    * **Cross Join** (Cartesian product)
    * **Self Join** (a table joined with itself)
      “Union” is not a join—it’s a set operation.
      **Rating:** 2/5
      *Justification:* The candidate listed inner, left, right, self, but saying “outer join” separately from left/right is ambiguous. They included “union all,” which is not a join type. They missed full outer and cross joins.

34. **Question:** “When would you use a left join versus a right join? Provide a scenario.”
    **Candidate’s Answer (Brief):**
    “Use left join when you want all rows from the left table along with matching rows from the right table. For example, to match all employees with their departments.”
    **Correct Answer:**

    * **Left Join**: Returns all rows from the left table and matching rows from the right table; unmatched right-side fields are NULL. Example: “List all employees and their department names, even if some employees have no department.”
    * **Right Join**: Returns all rows from the right table and matching rows from the left table; unmatched left-side fields are NULL. Example: “List all departments and show employees working in them, even if some departments have no employees.”
      Both are equivalent if you swap table positions.
      **Rating:** 3/5
      *Justification:* The candidate correctly explained left join with an employee/department example. They did not explicitly mention right join nor give a scenario for it, but implicitly understood relative usage.

35. **Question:** “Suppose you want to build a CI/CD pipeline (e.g., using Kubernetes or Docker). What steps would you take to set it up?”
    **Candidate’s Answer (Brief):**
    “First, create the pipeline. The build stage uses a Ruby script (e.g., Jenkinsfile) with stages like build, test, deploy, etc.”
    **Correct Answer:**
    A typical CI/CD pipeline includes:

    1. **Source Control**: Store code in Git (GitHub/GitLab/Bitbucket).
    2. **Build Stage**: Automate compilation, unit tests, and packaging (e.g., `mvn package`, `gradle build`). Define pipeline steps in Jenkinsfile, GitLab CI, or similar (YAML or script).
    3. **Test Stage**: Run unit/integration tests, static code analysis, security scans.
    4. **Artifact Repository**: Push built artifacts (e.g., JARs, Docker images) to Nexus/Artifactory or Docker registry.
    5. **Containerization**: Build Docker images (`Dockerfile`), tag, and push.
    6. **Deployment Stage**: Deploy to environments (Dev/QA/Staging). If on Kubernetes, apply manifests/Helm charts.
    7. **Configuration/Infrastructure as Code**: Use Helm, Terraform, or Kubernetes manifests to manage environment configuration.
    8. **Monitoring & Rollback**: Implement health checks, canary deployments, and rollback mechanisms.
       **Rating:** 2/5
       *Justification:* The candidate mentioned creating a pipeline and “Ruby script with stages,” presumably referring to Jenkins’s Groovy pipelines. However, they gave minimal detail and didn’t outline the full CI/CD flow (tests, artifact repo, container push, deployment).

36. **Question:** “What is the relationship between Kubernetes and Docker?”
    **Candidate’s Answer (Brief):**
    “Docker builds and runs containers; Kubernetes orchestrates those containers in production (an umbrella managing them).”
    **Correct Answer:**

    * **Docker** is a containerization platform to package applications and their dependencies into portable containers.
    * **Kubernetes** is a container orchestration system that schedules, scales, and manages containerized applications (often Docker containers) across clusters. It automates deployment, scaling, rolling updates, and self-healing of containers.
      **Rating:** 5/5
      *Justification:* The candidate accurately described the complementary roles: Docker for container creation, Kubernetes for orchestration.

37. **Question:** “You are using Git and Jira. How do you work in an Agile manner? Suppose your team has…”
    **Candidate’s Answer (Brief):**
    “In agile, we have a dedicated team. Use Jira or Rally for backlog management. We hold daily standups, backlog grooming/prioritization, and retrospectives (including appreciations).”
    **Correct Answer:**
    Agile practices typically include:

    * **Sprint Planning:** Define user stories and tasks in Jira; estimate effort.
    * **Daily Standups:** Short daily meetings to discuss progress, impediments, and plan for the day.
    * **Backlog Grooming (Refinement):** Regularly review and prioritize backlog items.
    * **Sprint Review/Demo:** Showcase completed work at sprint end.
    * **Sprint Retrospective:** Discuss what went well, what didn’t, and actionable improvements.
    * Use Jira to track user stories, tasks, bugs, and communicate status.
      **Rating:** 4/5
      *Justification:* The candidate captured core agile ceremonies (standups, backlog grooming, retrospectives) and tool usage (Jira/Rally). They could have mentioned sprint planning and review explicitly, but the essentials are present.

38. **Question:** “What is the role of AWS Lambda? Why do we use AWS Lambda?”
    **Candidate’s Answer (Brief):**
    “AWS Lambda is a serverless function platform where you upload code and AWS handles provisioning, scaling, integration, and resource management, so you don’t manage servers.”
    **Correct Answer:**
    AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You deploy functions; Lambda automatically scales to handle requests, charges per execution time, and integrates with AWS services (API Gateway, S3, DynamoDB, etc.). Use it for event-driven workloads, microservices, ETL tasks, and lightweight API backends to reduce operational overhead.
    **Rating:** 5/5
    *Justification:* The candidate’s explanation covered the essence: no server management, automatic scaling, and integration. They succinctly conveyed Lambda’s purpose.

---

**Overall Assessment of Candidate’s Technical Responses:**

* Strengths: Clear understanding of Java collections (HashMap/ConcurrentHashMap/LinkedHashMap), interface improvements in Java 8, Spring Boot benefits, API gateway concepts, AWS Lambda, and some JPA repository nuances.
* Areas for Improvement: Deeper detail on CI/CD pipelines, JPA repository vs. CrudRepository differences, SQL join taxonomy, and eager vs. lazy loading in JPA. In some answers, terminology was slightly imprecise (e.g., conflating “outer join” with left/right joins, unclear “com size” reference for metaspace).
* **Average Score Across All Questions:** 3.4/5
