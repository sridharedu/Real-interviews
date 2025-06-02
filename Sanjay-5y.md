1. **Question:** Tell me about yourself.

   * **Candidate’s answer (brief):**
     Sanjay, B.E. in Electronics & Communication, 5 years as software developer (3 years in Java). Worked on Spring Boot, Spring Security, REST APIs, Kafka, JUnit 5, Mockito, CI/CD. Migrated BNSF mainframe to Java 8/11 and integrated microservices.
   * **Rating:** 8/10
   * **Your answer (correct):**
     I’m Sanjay, a software engineer with a B.E. in Electronics & Communication and 5 years of experience—3 of those in Java. My core stack includes Spring Boot (2.7), Spring Security, RESTful APIs, Apache Kafka, JUnit 5, Mockito, and CI/CD pipelines. Recently, I led the migration of a large mainframe-based logistics-tracking system (BNSF) to Java 8/11, integrating it into a microservices architecture.

2. **Question:** You have created a CI/CD pipeline?

   * **Candidate’s answer (brief):**
     No, I collaborated with DevOps but did not build it myself.
   * **Rating:** 6/10
   * **Your answer (correct):**
     While I did not author the pipeline scripts, I worked closely with the DevOps team in Jenkins, defining build, test, and deployment steps for our Spring Boot services to ensure automated packaging, testing, and deployment.

3. **Question:** How do you implement API Gateway in microservices?

   * **Candidate’s answer (brief):**
     Use Spring Cloud Gateway; register with service discovery; add gateway dependency; configure `spring.cloud.gateway.routes.[id].uri` and `.predicates` in `application.properties`.
   * **Rating:** 7/10
   * **Your answer (correct):**
     Add the `spring-cloud-starter-gateway` dependency, ensure the gateway is registered with Eureka (service discovery), then in `application.properties` define routes under `spring.cloud.gateway.routes[n]`:

     ```properties
     spring.cloud.gateway.routes[0].id=service-a
     spring.cloud.gateway.routes[0].uri=lb://SERVICE-A
     spring.cloud.gateway.routes[0].predicates=Path=/service-a/**
     ```

     The gateway acts as a single entry point, handling load balancing, routing, and filters before forwarding requests to the correct microservice.

4. **Question:** Which properties do you add in `application.properties` for the Gateway?

   * **Candidate’s answer (brief):**
     Kept a common `application.properties` and added entries like:

     ```
     spring.cloud.gateway.routes.route1.uri=lb://SERVICE-A  
     spring.cloud.gateway.routes.route1.predicates=Path=/service-a/**  
     spring.cloud.gateway.routes.route2.uri=lb://SERVICE-B  
     spring.cloud.gateway.routes.route2.predicates=Path=/service-b/**  
     ```
   * **Rating:** 6/10
   * **Your answer (correct):**
     In `application.properties`, define each route under `spring.cloud.gateway.routes`, for example:

     ```properties
     spring.cloud.gateway.discovery.locator.enabled=true
     spring.cloud.gateway.routes[0].id=service-a
     spring.cloud.gateway.routes[0].uri=lb://SERVICE-A
     spring.cloud.gateway.routes[0].predicates=Path=/service-a/**

     spring.cloud.gateway.routes[1].id=service-b
     spring.cloud.gateway.routes[1].uri=lb://SERVICE-B
     spring.cloud.gateway.routes[1].predicates=Path=/service-b/**
     ```

     Enabling service discovery locator ensures all registered services are picked up automatically.

5. **Question:** Why use Spring Data JPA instead of plain JDBC?

   * **Candidate’s answer (brief):**
     Reduces boilerplate; provides built-in methods like `findById()`, `save()`, `delete()`; manages DB connections and transactions; enforces data integrity.
   * **Rating:** 8/10
   * **Your answer (correct):**
     Spring Data JPA abstracts JDBC, giving CRUD methods automatically (e.g., `findById()`, `save()`, `delete()`) without writing SQL. It handles connections, entity mapping, and transactions for you. It also supports pagination and deriving queries from method names, reducing boilerplate and improving productivity.

6. **Question:** Which annotations do you use in Spring Boot?

   * **Candidate’s answer (brief):**
     `@SpringBootApplication` (combines `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`), `@Component`, `@Controller`, `@Service`, `@Repository`, `@Primary`, `@Qualifier`, plus implied `@Autowired`, `@Bean`, `@Configuration`.
   * **Rating:** 9/10
   * **Your answer (correct):**
     Common annotations:

     * `@SpringBootApplication` on the main class (auto-configuration, component scan, configuration).
     * Stereotypes: `@Component` (generic), `@Service` (business logic), `@Repository` (data layer), `@Controller`/`@RestController` (web layer).
     * `@Autowired` for DI, `@Qualifier`/`@Primary` for choosing between multiple beans.
     * `@Bean` inside a `@Configuration` class to explicitly declare beans.

7. **Question:** When do you use `@Qualifier`?

   * **Candidate’s answer (brief):**
     When more than two beans of the same type exist; use `@Qualifier` with `@Autowired` to disambiguate.
   * **Rating:** 8/10
   * **Your answer (correct):**
     Use `@Qualifier("beanName")` whenever Spring finds multiple bean candidates of the same type, pairing it with `@Autowired` to explicitly select which bean to inject.

8. **Question:** What’s the difference between `@Bean` and `@Component`?

   * **Candidate’s answer (brief):**
     `@Bean` is method-level inside a `@Configuration` class; `@Component` is class-level for component scanning.
   * **Rating:** 8/10
   * **Your answer (correct):**
     `@Component` is placed on a class for component scanning, letting Spring auto-detect it. `@Bean` is placed on a method inside a `@Configuration` class; Spring executes that method at runtime and registers its return value as a bean.

9. **Question:** What is the use of `@Service`?

   * **Candidate’s answer (brief):**
     Marks a class as business-logic bean in the service layer.
   * **Rating:** 8/10
   * **Your answer (correct):**
     `@Service` is a specialization of `@Component` indicating that the class holds business logic. It makes the class a Spring-managed bean and clarifies that it resides in the service layer.

10. **Question:** Alternative to `@Autowired` for injecting a dependency in a controller?

    * **Candidate’s answer (brief):**
      Use constructor injection or manually define beans in a `@Configuration` class.
    * **Rating:** 7/10
    * **Your answer (correct):**
      Use constructor-based injection by declaring required beans in the controller’s constructor (Spring will auto-inject them). Example:

      ```java
      @RestController
      public class MyController {
          private final MyService myService;
          public MyController(MyService myService) {
              this.myService = myService;
          }
      }
      ```

11. **Question:** What features are in Java 8?

    * **Candidate’s answer (brief):**
      Lambda expressions, method references, default and static methods in interfaces, functional interfaces, Optional class, Stream API.
    * **Rating:** 8/10
    * **Your answer (correct):**
      Java 8 introduced:

      1. Lambda expressions (`(a, b) -> a + b`)
      2. Method references (`ClassName::methodName`)
      3. Default and static methods in interfaces
      4. Functional interfaces (`@FunctionalInterface`, e.g., `Predicate`)
      5. `Optional<T>` to avoid nulls
      6. Stream API with intermediate (`filter`, `map`) and terminal (`collect`, `forEach`) operations.

12. **Question:** How does a parallel stream work?

    * **Candidate’s answer (brief):**
      Fetches data asynchronously—splits tasks into multiple pipelines (parallel).
    * **Rating:** 6/10
    * **Your answer (correct):**
      A parallel stream uses the Fork/Join framework to split the data source into chunks, processes each chunk concurrently on multiple threads, then merges the results. It can speed up large data operations but adds overhead and potential ordering differences.

13. **Question:** Name some terminal and non-terminal stream functions.

    * **Candidate’s answer (brief):**
      Terminal: `reduce()`, `collect()`, `max()`, etc.
      Intermediate (non-terminal): `filter()`, `map()`, `skip()`, `limit()`.
    * **Rating:** 7/10
    * **Your answer (correct):**

      * **Intermediate (non-terminal) operations:** `filter()`, `map()`, `flatMap()`, `distinct()`, `sorted()`, `skip()`, `limit()`.
      * **Terminal operations:** `forEach()`, `collect()`, `reduce()`, `count()`, `max()`, `min()`, `anyMatch()`, `allMatch()`.

14. **Question:** Name predefined functional interfaces in Java 8.

    * **Candidate’s answer (brief):**
      `Predicate<T>`, `Function<T,R>`, `Supplier<T>`, `Consumer<T>`, etc.
    * **Rating:** 7/10
    * **Your answer (correct):**
      Common built-in functional interfaces include:

      * `Predicate<T>` (`boolean test(T)`)
      * `Function<T,R>` (`R apply(T)`)
      * `Supplier<T>` (`T get()`)
      * `Consumer<T>` (`void accept(T)`)
      * Additional: `UnaryOperator<T>`, `BinaryOperator<T>`, `BiFunction<T,U,R>`, `BiConsumer<T,U>`, `BiPredicate<T,U>`.

15. **Question:** Why was `Optional` introduced in Java 8?

    * **Candidate’s answer (brief):**
      To reduce `NullPointerException` by representing “no value” explicitly.
    * **Rating:** 7/10
    * **Your answer (correct):**
      `Optional<T>` models a container that may or may not hold a non-null value. It forces handling the possibility of absence and helps avoid null checks and `NullPointerException` by providing methods like `Optional.ofNullable()`, `orElse()`, `orElseThrow()`, and `ifPresent()`.

16. **Question:** What is a method reference?

    * **Candidate’s answer (brief):**
      Shorthand for a lambda; can refer to static, instance, or constructor methods (e.g., `ClassName::staticMethod`, `instance::method`, `ClassName::new`).
    * **Rating:** 7/10
    * **Your answer (correct):**
      A method reference is a shorthand for a lambda expression that calls an existing method directly. Forms include:

      1. `ClassName::staticMethod`
      2. `instance::instanceMethod`
      3. `ClassName::instanceMethod` (for a parameter’s method)
      4. `ClassName::new` (constructor reference)
         It must match the signature of a functional interface’s single abstract method.

17. **Question:** Difference between a normal interface and a functional interface?

    * **Candidate’s answer (brief):**
      Normal interface can have multiple abstract methods; functional interface has exactly one abstract method (plus default/static methods).
    * **Rating:** 8/10
    * **Your answer (correct):**

      * **Normal interface:** Can have multiple abstract methods; from Java 8 onward, can also include default and static methods.
      * **Functional interface:** Contains exactly one abstract method (annotated `@FunctionalInterface`), allowing it to be used in lambda expressions. It may also have default and static methods.

18. **Question:** Difference between an abstract class and an interface?

    * **Candidate’s answer (brief):**
      Interface (pre-Java 8) has only method signatures (no implementation) and no state; cannot instantiate. Abstract class can contain abstract and concrete methods, and fields; still cannot instantiate directly.
    * **Rating:** 7/10
    * **Your answer (correct):**

      * **Interface (Java 8+):** Can have abstract methods, default methods, static methods, and constants. Cannot hold state. Cannot instantiate; classes implement interfaces.
      * **Abstract class:** Can have abstract methods, concrete methods, and instance variables. Cannot instantiate; subclasses extend it. Use abstract classes when you need shared code or state; interfaces define contracts.

19. **Question:** What is polymorphism?

    * **Candidate’s answer (brief):**
      Ability of one object to take multiple forms; compile-time (method overloading) and runtime (method overriding).
    * **Rating:** 6/10
    * **Your answer (correct):**
      Polymorphism means “many forms.”

      * **Compile-time polymorphism:** Method overloading (same method name, different parameters).
      * **Runtime polymorphism:** Method overriding (subclass provides specific implementation, invoked via a superclass reference at runtime).

20. **Question:** Difference between `HashMap` and `TreeMap`?

    * **Candidate’s answer (brief):**
      `HashMap`: unordered, allows one null key and multiple null values.
      `TreeMap`: sorted by natural order or `Comparator`, disallows null keys/values.
    * **Rating:** 8/10
    * **Your answer (correct):**

      * **HashMap:** Backed by a hash table, O(1) average for put/get, no guaranteed order, allows one null key and multiple null values.
      * **TreeMap:** Backed by a Red-Black tree, O(log n) for put/get, keys sorted according to natural order or provided `Comparator`, does not allow null keys (null values also cause exceptions in comparison).

21. **Question:** How many ways can you implement multithreading?

    * **Candidate’s answer (brief):**
      Extend `Thread` class; implement `Runnable` interface.
    * **Rating:** 9/10
    * **Your answer (correct):**
      Common ways:

      1. Extend `Thread` class and override `run()`.
      2. Implement `Runnable` interface and pass an instance to a `Thread` constructor.
      3. (Optional) Implement `Callable<V>` and submit to an `ExecutorService` to get a `Future<V>` for return values or checked exceptions.

22. **Question:** Do you know about databases?

    * **Candidate’s answer (brief):**
      Familiar at a basic level; did not elaborate.
    * **Rating:** 5/10
    * **Your answer (correct):**
      I’ve worked with relational databases such as Oracle and MySQL—designing tables, writing SQL queries, understanding normalization, and performing CRUD operations. I’ve used JPA/Hibernate for ORM and can optimize queries via indexing, stored procedures, and pagination.

23. **Question:** Do you know AngularJS?

    * **Candidate’s answer (brief):**
      Has not used AngularJS; knows React, HTML, CSS, JavaScript.
    * **Rating:** 4/10
    * **Your answer (correct):**
      I have not worked directly with AngularJS. I do have experience using React, HTML, CSS, and vanilla JavaScript for front-end development, but no hands-on AngularJS projects.

24. **Question:** Which cloud servers are you using?

    * **Candidate’s answer (brief):**
      “Open” cloud (unclear).
    * **Rating:** 3/10
    * **Your answer (correct):**
      I’ve deployed applications on AWS using EC2 for compute, S3 for storage, and Elastic Beanstalk for platform management. I’m also familiar with Azure basics like App Service and Azure SQL Database.

25. **Question:** Do you know AWS or Azure?

    * **Candidate’s answer (brief):**
      Familiar with AWS.
    * **Rating:** 5/10
    * **Your answer (correct):**
      I have practical experience with AWS services such as EC2, S3, RDS, Lambda, and CloudWatch. I understand AWS architecture patterns for high availability. I have basic knowledge of Azure but have not worked on it extensively.

26. **Question:** Can you tell me what a lambda function is?

    * **Candidate’s answer (brief):**
      Anonymous function syntax in Java 8: `(a, b) -> a + b`; compiler infers types.
    * **Rating:** 7/10
    * **Your answer (correct):**
      A lambda expression is an anonymous function that implements a functional interface’s single method. Example:

      ```java
      BiFunction<Integer,Integer,Integer> add = (a, b) -> a + b;
      ```

      The compiler infers parameter types, and you don’t need a method name. It enables functional-style code by passing behavior as data.

27. **Question:** Difference between `UNION` and `UNION ALL`?

    * **Candidate’s answer (brief):**
      `UNION`: returns unique rows (deduplicates).
      `UNION ALL`: returns all rows, including duplicates.
    * **Rating:** 8/10
    * **Your answer (correct):**

      * **UNION:** Combines result sets and removes duplicate rows (implicitly performs `DISTINCT`).
      * **UNION ALL:** Combines result sets without removing duplicates, improving performance since no extra deduplication step is needed.

28. **Question:** How many types of joins are there?

    * **Candidate’s answer (brief):**
      Inner Join, Left Join, Right Join, Full Join.
    * **Rating:** 8/10
    * **Your answer (correct):**
      Four primary types:

      1. **INNER JOIN:** Returns only rows matching in both tables.
      2. **LEFT (OUTER) JOIN:** Returns all rows from left table and matching rows from right (or NULL).
      3. **RIGHT (OUTER) JOIN:** Returns all rows from right table and matching rows from left (or NULL).
      4. **FULL (OUTER) JOIN:** Returns all rows from either table, matching where possible and `NULL` otherwise.
         (Optionally, **CROSS JOIN** for Cartesian product.)

29. **Question:** What table optimization techniques do you know?

    * **Candidate’s answer (brief):**
      Create indexes (good for SELECT; careful with heavy CRUD). Use stored procedures/functions (pre-compiled, reusable). Fetch only required columns instead of `SELECT *`. Use pagination to limit result sets.
    * **Rating:** 7/10
    * **Your answer (correct):**
      Common techniques:

      * **Indexing:** Create indexes on frequently searched columns to speed up SELECT, but avoid over-indexing on write-heavy tables.
      * **Stored procedures/functions:** Pre-compile SQL logic in the database to reduce parsing overhead and reuse logic.
      * **Selective column retrieval:** Use `SELECT col1, col2` instead of `SELECT *`.
      * **Pagination:** Fetch results in pages using `LIMIT` or `ROWNUM`.
      * **Partitioning/sharding:** Split large tables by key or range to improve performance on very large datasets.
      * **Query plan analysis:** Review execution plans and adjust schema or queries accordingly.

30. **Question:** Given a `List<List<T>>`, how do you use `flatMap` to flatten it?

    * **Candidate’s answer (brief):**

      ```java
      listOfLists.stream()
                 .flatMap(List::stream)
                 .collect(Collectors.toList());
      ```
    * **Rating:** 9/10
    * **Your answer (correct):**
      Exactly that:

      ```java
      List<T> flatList = listOfLists.stream()
          .flatMap(List::stream)
          .collect(Collectors.toList());
      ```

      `flatMap` converts each inner `List<T>` into a `Stream<T>`, merges them into one continuous stream, and then collects to a `List<T>`.
