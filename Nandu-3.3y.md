1. **Question:** Tell me about yourself.

   * **Candidate’s brief answer:**
     “My name is Nandu. I’m a Java back-end developer at Infosys. My tech stack includes Java, microservices, Spring Boot, Hibernate, JPA, JDBC, Mockito, and Spring Security. I know MySQL and have front-end exposure in HTML/CSS. My main skills are Java, data structures & algorithms, and problem solving.”
   * **Rating:** 7/10
   * **Correct answer:**
     I am Nandu, a Java back-end developer at Infosys with 3.3 years of experience. I specialize in Java, Spring Boot microservices, Hibernate/JPA for ORM, JDBC, and I write tests with JUnit and Mockito. I work with MySQL on the database side and have basic HTML/CSS skills. My core strengths are Java, data structures & algorithms, and problem-solving.

2. **Question:** You mentioned Spring Boot, Hibernate, JPA, JDBC, Mockito, Spring Security—how do you implement role-based API security?

   * **Candidate’s brief answer:**
     “Add `spring-boot-starter-security`. By default, all APIs are secured; you must log in with username/password (default username `user`). To customize, create a SecurityConfig class with `@EnableWebSecurity`, override `configure(HttpSecurity)`, and use `http.authorizeRequests().antMatchers("/api").hasRole("ROLE_NAME")`. Roles are stored in a database table (`role` table with ID and name). We link user credentials (e.g., Microsoft credentials) to roles, then Spring Security checks the user’s role to allow or deny access.”
   * **Rating:** 8/10
   * **Correct answer:**

     1. Add the `spring-boot-starter-security` dependency.
     2. Create a configuration class, e.g.:

        ```java
        @Configuration
        @EnableWebSecurity
        public class SecurityConfig extends WebSecurityConfigurerAdapter {
            @Override
            protected void configure(AuthenticationManagerBuilder auth) throws Exception {
                // Configure authentication from the database
                auth.jdbcAuthentication()
                    .dataSource(dataSource)
                    .usersByUsernameQuery("SELECT username, password, enabled FROM users WHERE username = ?")
                    .authoritiesByUsernameQuery("SELECT u.username, r.role_name FROM user_roles r JOIN users u ON r.user_id = u.id WHERE u.username = ?");
            }
            @Override
            protected void configure(HttpSecurity http) throws Exception {
                http
                  .authorizeRequests()
                    .antMatchers("/admin/**").hasRole("ADMIN")
                    .antMatchers("/user/**").hasAnyRole("USER","ADMIN")
                    .anyRequest().authenticated()
                  .and()
                  .formLogin()
                    .permitAll()
                  .and()
                  .logout()
                    .permitAll();
            }
        }
        ```
     3. In your database, maintain `users` and `roles` tables. Spring Security will load username/password and granted authorities (roles) from these tables.
     4. Annotate your controller methods with `@PreAuthorize("hasRole('ADMIN')")` or configure URL-based rules as shown above to enforce role-based access.

3. **Question:** You’re comfortable with JUnit and Mockito—what is the use of Mockito?

   * **Candidate’s brief answer:**
     “Mockito is used to write test cases. We mock service or repository dependencies so we can isolate the method under test. We assume the mocked dependency returns a particular value, then we assert that our code handles it correctly.”
   * **Rating:** 8/10
   * **Correct answer:**
     Mockito is a mocking framework. In unit tests, instead of invoking real dependencies (e.g., repositories or external services), you create mock objects. For example:

     ```java
     @ExtendWith(MockitoExtension.class)
     class UserServiceTest {
         @Mock
         private UserRepository userRepository;
         @InjectMocks
         private UserService userService;

         @Test
         void testGetUserById() {
             User mockUser = new User(1L, "Alice");
             when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));
             User user = userService.getUserById(1L);
             assertEquals("Alice", user.getName());
         }
     }
     ```

     This isolates `UserService` from the actual database or JPA layer, letting you test logic in `UserService` alone.

4. **Question:** You know JPA. What is JPA, and why use it instead of raw JDBC?

   * **Candidate’s brief answer:**
     “JPA (Java Persistence API) is the specification for object-relational mapping. It maps Java objects to database tables. Instead of writing SQL (`SELECT * FROM table` etc.) and handling `ResultSet` and `PreparedStatement` manually, JPA provides methods like `findById()`, `findAll()`, and `save()`. It handles queries and transactions automatically.”
   * **Rating:** 8/10
   * **Correct answer:**
     JPA (Java Persistence API) defines a standard way to map Java entities to relational tables. Benefits over JDBC:

     1. **Less boilerplate:** No manual `Connection`, `PreparedStatement`, `ResultSet` handling. Repositories like `findById()`, `save()`, `delete()` work out-of-the-box.
     2. **Entity relationships:** Easily model `@OneToMany`, `@ManyToOne`, `@ManyToMany` without hand-coding joins.
     3. **Transaction management:** Spring can manage transactions declaratively.
     4. **Database portability:** Switch databases by changing dialect; minimal code changes.
     5. **Query derivation & JPQL:** Write methods in repository interfaces that derive queries from method names, or use JPQL/Criteria API for dynamic queries.

5. **Question:** Are you aware of JPA mapping annotations—`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`?

   * **Candidate’s brief answer:**
     “Yes. In the entity class, if two tables have a one-to-one relationship, I annotate the field with `@OneToOne`. For one-to-many and many-to-many mapping, I use `@OneToMany` and `@ManyToMany` annotations accordingly.”
   * **Rating:** 7/10
   * **Correct answer:**

     * **`@OneToOne`:** Maps a single entity to a single entity. E.g.:

       ```java
       @Entity
       public class User {
           @Id
           private Long id;
           @OneToOne
           @JoinColumn(name = "profile_id")
           private UserProfile profile;
       }
       ```
     * **`@OneToMany`:** Maps one entity to many child entities. Usually paired with `@ManyToOne` on the other side. E.g.:

       ```java
       @Entity
       public class Order {
           @Id
           private Long id;
           @OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
           private List<OrderItem> items;
       }
       @Entity
       public class OrderItem {
           @Id
           private Long id;
           @ManyToOne
           @JoinColumn(name = "order_id")
           private Order order;
       }
       ```
     * **`@ManyToMany`:** Many entities can relate to many others via a join table. E.g.:

       ```java
       @Entity
       public class Student {
           @Id
           private Long id;
           @ManyToMany
           @JoinTable(
             name = "student_course",
             joinColumns = @JoinColumn(name = "student_id"),
             inverseJoinColumns = @JoinColumn(name = "course_id"))
           private List<Course> courses;
       }
       @Entity
       public class Course {
           @Id
           private Long id;
           @ManyToMany(mappedBy = "courses")
           private List<Student> students;
       }
       ```

6. **Question:** Why use JPA rather than JDBC?

   * **Candidate’s brief answer:**
     “JDBC is an API to connect Java to the database. In `application.properties`, you specify `spring.datasource.url=jdbc:mysql://…`. If I use pure JDBC, I must write manual SQL (e.g., `SELECT * FROM table`). With JPA, I don’t write manual queries; I just call repository methods like `findById()` or `save()`.”
   * **Rating:** 8/10
   * **Correct answer:**
     JDBC requires writing SQL queries by hand and managing connections, statements, and result sets manually. JPA provides:

     1. **Automatic mapping** of entities to tables via `@Entity`, `@Table`, `@Column`.
     2. **CRUD repository methods** (`save()`, `findById()`, `findAll()`) without writing SQL.
     3. **Declarative transactions** via `@Transactional`.
     4. **Relationship management** (`@OneToMany`, etc.) without manual joins.
     5. **Portability**—switching databases only requires changing the dialect or driver, not rewriting SQL.

7. **Question:** In Hibernate, what are eager loading and lazy loading?

   * **Candidate’s brief answer:**
     “I’ve heard about `FetchType.EAGER` and `FetchType.LAZY`, but I haven’t used them much.”
   * **Rating:** 3/10
   * **Correct answer:**

     * **Eager loading (`FetchType.EAGER`)**: Hibernate fetches the associated entity or collection immediately along with the owner entity. E.g., if `Order` has `@OneToMany(fetch = FetchType.EAGER) List<OrderItem>`, then fetching an `Order` will also fetch all its `OrderItem`s in a single query (or via JOIN).
     * **Lazy loading (`FetchType.LAZY`)**: Hibernate fetches only the owner entity initially. The associated collection or entity is loaded on the first access. E.g., `@OneToMany(fetch = FetchType.LAZY)` means that `order.getItems()` triggers a separate query only when you call `getItems()`.

8. **Question:** Why use Spring Boot instead of Spring MVC?

   * **Candidate’s brief answer:**
     “With Spring Boot, you don’t write manual configuration. It provides in-memory database support and auto-configuration, so you don’t need XML or boilerplate code.”
   * **Rating:** 7/10
   * **Correct answer:**

     * **Auto-configuration:** Spring Boot automatically configures many beans (e.g., a `DataSource`, `EntityManagerFactory`, `Tomcat` server) based on classpath dependencies. With plain Spring MVC, you must define these configurations manually—XML or JavaConfig.
     * **Embedded server:** Spring Boot embeds Tomcat/Jetty, so you can run `java -jar myapp.jar` without deploying to an external container.
     * **Starter POMs:** A single dependency like `spring-boot-starter-web` pulls in everything you need for a web app.
     * **Opinionated defaults:** Sensible defaults (port 8080, H2 DataSource, Jackson JSON) that you can override as needed.
     * **Production readiness:** Spring Boot Actuator endpoints for health checks, metrics, and application insights.

9. **Question:** Explain Dependency Injection and IoC.

   * **Candidate’s brief answer:**
     “Dependency Injection is used in Spring to maintain loose coupling. Instead of manually instantiating dependencies, Spring’s IoC container automatically injects them. There are three types: constructor injection, setter injection, and field injection. The IoC container manages bean lifecycles.”
   * **Rating:** 9/10
   * **Correct answer:**

     * **IoC (Inversion of Control):** The principle that the framework (Spring) controls object creation and lifecycle, instead of application code.
     * **Dependency Injection (DI):** A design pattern where an object’s dependencies are “injected” by an external entity (the IoC container) rather than the object creating them itself.

       1. **Constructor injection:** Dependencies are passed via constructor parameters.
       2. **Setter injection:** Dependencies are set via setter methods.
       3. **Field injection:** Dependencies are injected directly into fields annotated with `@Autowired`.
          Using DI/IoC leads to loose coupling and easier unit testing (you can mock dependencies).

10. **Question:** What is `@RestController`?

    * **Candidate’s brief answer:**
      “`@RestController` annotates a class whose methods handle HTTP requests (`@GetMapping`, `@PostMapping`, etc.) and return JSON (or other formats).”
    * **Rating:** 9/10
    * **Correct answer:**
      `@RestController` is a convenience annotation combining `@Controller` and `@ResponseBody`. It marks a class as a web controller whose methods return JSON (or XML) responses directly rather than view names. For example:

      ```java
      @RestController
      @RequestMapping("/api/users")
      public class UserController {
          @GetMapping("/{id}")
          public UserDto getUser(@PathVariable Long id) { … }
      }
      ```

11. **Question:** What is `ResponseEntity<T>`?

    * **Candidate’s brief answer:**
      “`ResponseEntity<T>` is not an annotation. It’s a return type for REST methods when you need to return both a body and an HTTP status. For example:

      ```java
      return new ResponseEntity<>("Success", HttpStatus.OK);
      ```

      ”
    * **Rating:** 8/10
    * **Correct answer:**
      `ResponseEntity<T>` is a generic type that represents the entire HTTP response: status code, headers, and body. For example:

      ```java
      @GetMapping("/{id}")
      public ResponseEntity<UserDto> getUser(@PathVariable Long id) {
          UserDto user = userService.findById(id);
          if (user == null) {
              return ResponseEntity.status(HttpStatus.NOT_FOUND).build();
          }
          return ResponseEntity.ok(user);
      }
      ```

12. **Question:** What is the difference between `@Controller` and `@RestController`?

    * **Candidate’s brief answer:**
      “`@Controller` is a normal web controller (for serving views). `@RestController` is specifically for REST APIs.”
    * **Rating:** 8/10
    * **Correct answer:**

      * `@Controller` is used for controllers that return view names (e.g., Thymeleaf templates) or use `@ResponseBody` on individual methods.
      * `@RestController` is equivalent to `@Controller + @ResponseBody` on every method, meaning methods return data (e.g., JSON) directly, not view names.

13. **Question:** What is `@Service` and `@Repository`?

    * **Candidate’s brief answer:**
      “`@Service` marks a class containing business logic. `@Repository` marks a data-access class, which Spring turns into a bean for database operations.”
    * **Rating:** 8/10
    * **Correct answer:**

      * `@Service` is a specialization of `@Component` indicating that the class holds business logic.
      * `@Repository` also extends `@Component` and indicates a data-access component. It adds exception translation for persistence exceptions.

14. **Question:** What is Spring Boot Actuator?

    * **Candidate’s brief answer:**
      “Actuator is used to monitor the health of the application—whether it’s active or not.”
    * **Rating:** 7/10
    * **Correct answer:**
      Spring Boot Actuator provides production-ready features to help you monitor and manage your application:

      * **Health endpoint** (`/actuator/health`)
      * **Metrics** (`/actuator/metrics`)
      * **Info** (`/actuator/info`)
      * **Environment** (`/actuator/env`), etc.
        It exposes endpoints that report on the application’s health, metrics, environment, and other operational information. You can customize which endpoints are enabled.

15. **Question:** Have you used an API Gateway (Spring Cloud Gateway) in microservices?

    * **Candidate’s brief answer:**
      “Yes, I’ve used API Gateway, but I’m not too familiar with Spring Cloud Gateway specifics.”
    * **Rating:** 5/10
    * **Correct answer:**
      Spring Cloud Gateway is a reactive, non-blocking gateway built on Spring WebFlux. To use it:

      1. Add the `spring-cloud-starter-gateway` dependency.
      2. In `application.yml`, configure routes:

         ```yaml
         spring:
           cloud:
             gateway:
               routes:
                 - id: user-service
                   uri: lb://USER-SERVICE
                   predicates:
                     - Path=/users/**
         ```
      3. Register your services with a discovery server (Eureka). The gateway resolves `lb://USER-SERVICE` to actual instances.
      4. The gateway can handle rate limiting, retries, filters, and circuit breakers before routing requests to downstream services.

16. **Question:** Are you aware of Docker/Kubernetes?

    * **Candidate’s brief answer:**
      “I’ve used Docker locally. Docker packages applications and dependencies so the client can run it on any machine—even if they don’t have Java 8 installed. I haven’t used Kubernetes.”
    * **Rating:** 6/10
    * **Correct answer:**

      * **Docker:** A containerization platform. You write a `Dockerfile` to package your JAR and runtime into an image. Example `Dockerfile`:

        ```dockerfile
        FROM openjdk:8-jdk-alpine
        VOLUME /tmp
        ARG JAR_FILE=target/myapp.jar
        COPY ${JAR_FILE} app.jar
        ENTRYPOINT ["java","-jar","/app.jar"]
        ```

        Build with `docker build -t myapp .` and run with `docker run -p 8080:8080 myapp`.
      * **Kubernetes:** An orchestration platform for containers. You define `Deployment`, `Service`, and `Ingress` YAMLs to run and expose your Dockerized application in a Kubernetes cluster, which handles scaling, rolling updates, and self-healing.

17. **Question:** Explain OOP concepts.

    * **Candidate’s brief answer:**
      “The four pillars are Encapsulation (data hiding in a class), Inheritance (child inherits parent properties), Abstraction (hide unnecessary details via `abstract` classes), and Polymorphism (overloading at compile-time, overriding at runtime).”
    * **Rating:** 8/10
    * **Correct answer:**

      * **Encapsulation:** Bundle fields and methods in a class, exposing only what’s necessary via access modifiers.
      * **Inheritance:** Create a subclass that inherits fields and methods from a superclass, promoting code reuse.
      * **Abstraction:** Define interfaces or abstract classes to expose only essential functionality, hiding implementation details.
      * **Polymorphism:**

        1. **Compile-time (method overloading):** Same method name, different parameter lists.
        2. **Runtime (method overriding):** Subclass overrides a superclass method; the JVM calls the appropriate implementation at runtime.

18. **Question:** Can you override a static method?

    * **Candidate’s brief answer:**
      “No—static methods belong to the class, so they cannot be overridden.”
    * **Rating:** 9/10
    * **Correct answer:**
      Static methods are resolved at compile-time by the class reference, not the instance, so they cannot be overridden. You can hide a static method by declaring another static method with the same signature in a subclass, but that’s not true overriding.

19. **Question:** Do you know how to write an immutable class?

    * **Candidate’s brief answer:**
      “No, I do not.”
    * **Rating:** 1/10
    * **Correct answer:**
      To create an immutable class:

      1. Declare the class `final`.
      2. Make all fields `private final`.
      3. Provide a constructor that initializes all fields.
      4. Don’t provide any setters—only getters.
      5. If a field is a mutable object, return a defensive copy in its getter. Example:

      ```java
      public final class Person {
          private final String name;
          private final int age;
          private final Date birthDate; // mutable

          public Person(String name, int age, Date birthDate) {
              this.name = name;
              this.age = age;
              this.birthDate = new Date(birthDate.getTime());
          }
          public String getName() { return name; }
          public int getAge() { return age; }
          public Date getBirthDate() { return new Date(birthDate.getTime()); }
      }
      ```

20. **Question:** What is the difference between `StringBuilder` and `StringBuffer`?

    * **Candidate’s brief answer:**
      “`String` is immutable; `StringBuilder` and `StringBuffer` provide mutability. `StringBuilder` is not thread-safe; `StringBuffer` is thread-safe, so `StringBuilder` is faster.”
    * **Rating:** 10/10
    * **Correct answer:**
      Exactly. `StringBuilder` is faster because it’s not synchronized. `StringBuffer` synchronizes its methods to be thread-safe, which incurs overhead. Use `StringBuilder` when thread safety is not needed.

21. **Question:** How many ways can you create a synchronized block?

    * **Candidate’s brief answer:**
      “Two ways: method-level using `public synchronized void myMethod()`, and block-level using `synchronized(this) { … }`.”
    * **Rating:** 9/10
    * **Correct answer:**
      You can synchronize either an entire method:

      ```java
      public synchronized void myMethod() { … }
      ```

      or a code block on a specific lock object:

      ```java
      synchronized(lock) {
        // critical section
      }
      ```

      If you synchronize on `this`, it locks the current instance; you can also use any other object as the lock.

22. **Question:** Are you aware of design patterns? If so, which ones?

    * **Candidate’s brief answer:**
      “I know the Builder design pattern.”
    * **Rating:** 5/10
    * **Correct answer:**
      Common design patterns include:

      * **Creational:** Singleton, Builder, Factory Method, Prototype.
      * **Structural:** MVC (Model-View-Controller), Adapter, Decorator, Facade.
      * **Behavioral:** Strategy, Observer, Iterator.
        Knowing more than one pattern—e.g., Singleton and Strategy—demonstrates broader familiarity.

23. **Question:** What are the SOLID principles?

    * **Candidate’s brief answer:**
      “SOLID stands for: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion.”
    * **Rating:** 9/10
    * **Correct answer:**
      Exactly. SOLID principles guide maintainable, extensible software design. Briefly:

      * **S:** Single Responsibility Principle
      * **O:** Open/Closed Principle
      * **L:** Liskov Substitution Principle
      * **I:** Interface Segregation Principle
      * **D:** Dependency Inversion Principle

24. **Question:** What are the basic features of Java 8?

    * **Candidate’s brief answer:**
      “Lambda functions, functional interfaces, Stream API, Optional class, Collector classes.”
    * **Rating:** 8/10
    * **Correct answer:**
      Java 8 introduced:

      1. **Lambda expressions** (`(x, y) -> x + y`)
      2. **Functional interfaces** (`@FunctionalInterface`)
      3. **Stream API** for functional-style collection processing
      4. **Optional<T>** to avoid `NullPointerException`
      5. **Default and static methods** in interfaces
      6. **Date/Time API** (`java.time.*`)
      7. **Collectors** and enhancements to `java.util`.

25. **Question:** Is `Optional` a static class or a final class?

    * **Candidate’s brief answer:**
      “Static class.”
    * **Rating:** 2/10
    * **Correct answer:**
      `Optional<T>` is a **final** class (cannot be subclassed), not a static nested class. It resides in `java.util`.

26. **Question:** What is method reference?

    * **Candidate’s brief answer:**
      “No.”
    * **Rating:** 1/10
    * **Correct answer:**
      A method reference is a shorthand for a lambda that calls a method. It comes in four forms:

      1. **Static method:** `ClassName::staticMethod`
      2. **Instance method of a particular object:** `objectRef::instanceMethod`
      3. **Instance method of an arbitrary object of a type:** `ClassName::instanceMethod`
      4. **Constructor reference:** `ClassName::new`
         Example:

      ```java
      List<String> names = List.of("alice", "bob");
      names.stream()
           .map(String::toUpperCase)
           .collect(Collectors.toList());
      ```

27. **Question:** What is the difference between a sequential stream and a parallel stream?

    * **Candidate’s brief answer:**
      “Sequential stream runs one after another. Parallel stream runs in parallel but isn’t thread-safe.”
    * **Rating:** 5/10
    * **Correct answer:**

      * **Sequential Stream:** Processes elements in a single thread, in encounter order (unless the source is unordered).
      * **Parallel Stream:** Splits the data into multiple substreams and processes them in parallel across available CPU cores. The terminal operation merges results.
        Parallel streams can improve performance for large datasets if operations are CPU-bound and stateless. Thread safety concerns apply only if you use non-thread-safe operations inside the pipeline.

28. **Question:** What is the difference between synchronous API and asynchronous API?

    * **Candidate’s brief answer:**
      “Synchronous means run parallel; asynchronous means run sequential.” (Incorrect.)
    * **Rating:** 2/10
    * **Correct answer:**

      * **Synchronous API:** The caller waits (blocks) until the operation completes, then continues. Example: `restTemplate.getForObject(…)`.
      * **Asynchronous API:** The operation returns immediately (often a `Future` or callback), and the caller can continue execution without waiting. Example: Spring’s `WebClient` returning a `Mono<T>` or `CompletableFuture<T>`.

29. **Question:** In Java 8, what are terminal operators and intermediate operators in streams?

    * **Candidate’s brief answer:**
      “Terminal operators (e.g., `collect`, `reduce`) return a result. Intermediate operators (e.g., `filter`, `map`) do not return a final result—they return another stream.”
    * **Rating:** 9/10
    * **Correct answer:**

      * **Intermediate (non-terminal) operations:** Return a new stream (lazy). Examples: `filter()`, `map()`, `limit()`, `skip()`.
      * **Terminal operations:** Produce a result or side-effect and close the stream. Examples: `collect()`, `forEach()`, `reduce()`, `findFirst()`.

30. **Question:** How do you synchronize a `HashMap`?

    * **Candidate’s brief answer:**
      “Use `Collections.synchronizedMap(new HashMap<>())`. A `ConcurrentHashMap` is in `java.util.concurrent`. Also, `synchronizedMap(...)` returns a synchronized view.”
    * **Rating:** 8/10
    * **Correct answer:**

      * Use `Collections.synchronizedMap(...)`:

        ```java
        Map<K, V> syncMap = Collections.synchronizedMap(new HashMap<>());
        ```
      * Alternatively, use `ConcurrentHashMap<K,V>` for better concurrency (no need to wrap with `synchronizedMap`).

31. **Question:** Which types of indexes do you know in the database?

    * **Candidate’s brief answer:**
      “Index helps select operations perform faster. I don’t know how many types.”
    * **Rating:** 3/10
    * **Correct answer:**
      Common index types include:

      1. **Clustered Index:** Determines the physical order of data (only one per table).
      2. **Non-Clustered Index:** Separate structure from data pages; can have multiple per table.
      3. **Unique Index:** Enforces uniqueness on one or more columns.
      4. **Composite Index:** An index on multiple columns.
      5. **Full-Text Index:** For text-search in long text columns.
      6. **Bitmap Index, Hash Index, Spatial Index, etc.,** depending on the database engine.

32. **Question:** How many types of joins are there?

    * **Candidate’s brief answer:**
      “Inner join, left outer join, right outer join, self join.”
    * **Rating:** 7/10
    * **Correct answer:**
      SQL join types include:

      * **INNER JOIN:** Returns rows when there is a match in both tables.
      * **LEFT (OUTER) JOIN:** Returns all rows from the left table, matching rows from the right, or `NULL` if no match.
      * **RIGHT (OUTER) JOIN:** Returns all rows from the right table, matching rows from the left, or `NULL` if no match.
      * **FULL (OUTER) JOIN:** Returns rows when there is a match in one of the tables.
      * **CROSS JOIN:** Cartesian product.
      * **SELF JOIN:** A table joined with itself.

33. **Question:** How do you express a JOIN in JPA?

    * **Candidate’s brief answer:**
      “We used the EntityManager to write a native query with `entityManager.createNativeQuery(...)`. I haven’t used the `@JoinColumn` annotation directly.”
    * **Rating:** 4/10
    * **Correct answer:**
      You can join tables in JPA using JPQL or the Criteria API:

      ```java
      @Entity
      public class Order {
          @Id
          private Long id;

          @ManyToOne
          @JoinColumn(name = "customer_id")
          private Customer customer;
      }
      // Query using JPQL
      @Query("SELECT o FROM Order o JOIN o.customer c WHERE c.name = :name")
      List<Order> findByCustomerName(@Param("name") String name);
      ```

      Or use `@OneToMany(mappedBy = "order")` and fetch joins:

      ```java
      @Query("SELECT o FROM Order o JOIN FETCH o.items WHERE o.id = :id")
      Optional<Order> findByIdWithItems(@Param("id") Long id);
      ```

34. **Question:** How do you find the third highest salary from a table with columns (`id`, `name`, `salary`)?

    * **Candidate’s brief answer:**
      (Candidate did not write the SQL; they asked “Should I write?” But did not provide an answer in the transcript.)
    * **Rating:** 0/10
    * **Correct answer:**
      There are several ways. Two common approaches:

      1. Using `LIMIT` / `OFFSET` (MySQL, PostgreSQL):

         ```sql
         SELECT salary
         FROM employees
         ORDER BY salary DESC
         LIMIT 1 OFFSET 2;
         ```

         This orders salaries descending, then skips the top two to get the third.
      2. Using a subquery (ANSI SQL):

         ```sql
         SELECT MAX(salary) AS third_highest
         FROM employees
         WHERE salary < (
             SELECT MAX(salary)
             FROM employees
             WHERE salary < (
                 SELECT MAX(salary) FROM employees
             )
         );
         ```
      3. Using window functions (if supported):

         ```sql
         SELECT DISTINCT salary
         FROM (
           SELECT salary, ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn
           FROM employees
         ) ranked
         WHERE rn = 3;
         ```

---

**Overall Rating for Candidate:** 5.5/10
