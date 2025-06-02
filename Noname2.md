1. **Question:** Which Java version are you using right now, and what is the difference between Java 8 and Java 16? What did you evaluate when using both versions?

   * **Candidate’s brief answer:**
     “We’re on Java 16. Java 8 introduced lambda expressions, functional interfaces, Stream API, Optional, the new date/time API, and CompletableFuture for async. Java 16 adds records, pattern matching for `instanceof`, sealed classes, and the Foreign Linker API as an incubator.”
   * **Rating:** 8/10
   * **Your answer (correct):**
     We currently use Java 16.

     * **Java 8 (2014)** brought:
       • Lambda expressions (`(a, b) -> a + b`)
       • Functional interfaces (`Function<T,R>`, `Predicate<T>`, etc.)
       • Stream API for pipeline processing on collections
       • `Optional<T>` to avoid nulls
       • The modern `java.time` (JSR 310) API
       • `CompletableFuture` for asynchronous programming
     * **Java 16 (2021)** introduces:
       • **Records** (compact syntax for immutable data holders)
       • **Pattern matching for `instanceof`** (type check + cast in one statement)
       • **Sealed classes** (restrict which classes can extend a superclass)
       • **Foreign Linker API** (incubator feature for calling native libraries without JNI)
       • Various minor language enhancements and performance optimizations.
       When migrating, we evaluated backward compatibility with existing code and libraries, performance benchmarks (e.g., Stream optimizations), developer productivity gains (e.g., replacing boilerplate DTOs with records), and third-party support for Java 16.

2. **Question:** In Java 8, why was the Stream concept introduced?

   * **Candidate’s brief answer:**
     “Streams let us perform different operations on collections (List, Set, Map) instead of using for-loops or while-loops.”
   * **Rating:** 6/10
   * **Your answer (correct):**
     The Stream API was introduced to:

     1. **Enable functional-style processing:** Chain operations (filter, map, reduce) on data sources without manual loops.
     2. **Improve readability and maintainability:** A pipeline like

        ```java
        list.stream()
            .filter(x -> x % 2 == 0)
            .map(x -> x * 2)
            .collect(Collectors.toList());
        ```

        replaces verbose loop logic with a clear declaration of intent.
     3. **Support lazy evaluation:** Intermediate operations (filter, map) are only executed when a terminal operation (e.g., `collect`, `forEach`) is invoked, avoiding unnecessary work.
     4. **Simplify parallelism:** Switching from `stream()` to `parallelStream()` leverages multiple CPU cores with minimal code changes.
     5. **Separate “what” from “how”:** Focus on *what* transformations you want, while the Stream framework handles iteration and optimizations.

3. **Question:** How do you use `Function` as a functional interface in programming? You know `Function`?

   * **Candidate’s brief answer:**
     “`Function<T,R>` is a functional interface (annotated with `@FunctionalInterface`). We need it when passing behavior as a parameter or writing reusable, testable logic.”
   * **Rating:** 7/10
   * **Your answer (correct):**
     The `java.util.function.Function<T,R>` interface represents a function taking a `T` and returning an `R`. It has one abstract method:

     ```java
     R apply(T t);
     ```

     **How to use it:**

     1. **Declare a `Function` instance:**

        ```java
        Function<String,Integer> parseInt = s -> Integer.valueOf(s);
        Function<Integer,Integer> square  = x -> x * x;
        ```
     2. **Chain functions with `andThen` or `compose`:**

        ```java
        Function<String,Integer> parseThenSquare = parseInt.andThen(square);
        int result = parseThenSquare.apply("5"); // returns 25
        ```
     3. **Pass it as a parameter to generic methods:**

        ```java
        public <T,R> List<R> transformList(List<T> list, Function<T,R> fn) {
            return list.stream()
                       .map(fn)
                       .collect(Collectors.toList());
        }
        // Usage:
        List<String> words = List.of("10","20","30");
        List<Integer> ints = transformList(words, parseInt); // [10, 20, 30]
        ```

     Using `Function` lets you encapsulate reusable behavior as an object rather than hard-coding logic.

4. **Question:** How do you use `map` and `flatMap`?

   * **Candidate’s brief answer:**
     “`map` transforms each element to exactly one new element—e.g., `strings.stream().map(String::toUpperCase)`. `flatMap` handles nested structures: each element produces a `Stream<R>`, and `flatMap` flattens those streams into one.”
   * **Rating:** 8/10
   * **Your answer (correct):**

     * **`map(Function<T,R>)`:** Transforms each element of a stream into one new element. For example:

       ```java
       List<String> names = List.of("alice","bob","carol");
       List<String> upper = names.stream()
                                 .map(String::toUpperCase)
                                 .collect(Collectors.toList());
       // ["ALICE","BOB","CAROL"]
       ```
     * **`flatMap(Function<T,Stream<R>>)`**: Each input element produces a `Stream<R>`, and `flatMap` concatenates them into a single `Stream<R>`. Commonly used to flatten nested lists. For example:

       ```java
       List<List<String>> listOfLists = List.of(
           List.of("a","b"),
           List.of("c"),
           List.of("d","e")
       );
       List<String> flat = listOfLists.stream()
                                      .flatMap(List::stream)
                                      .collect(Collectors.toList());
       // ["a","b","c","d","e"]
       ```

     Use `map` for one-to-one transformations, and `flatMap` for one-to-many where you need to flatten nested streams.

5. **Question:** Suppose I have a string `"ABC"` in lowercase—how do I convert it to uppercase using Java 8 Stream API?

   * **Candidate’s brief answer:**
     “Given `String str = "abc"`, use `str.chars()`, then `mapToObj(ch -> (char)ch)`, then `map(Character::toUpperCase)`, then `collect(Collectors.joining())`.” (They sketched:

     ```java
     String result = str.chars()
                        .mapToObj(ch -> Character.toString((char) ch).toUpperCase())
                        .collect(Collectors.joining());
     ```

     )
   * **Rating:** 7/10
   * **Your answer (correct):**
     A simpler way without dealing with code points is:

     ```java
     String str = "abc";
     String result = str.chars()
                        .mapToObj(ch -> Character.toString((char) ch).toUpperCase())
                        .collect(Collectors.joining());
     System.out.println(result); // "ABC"
     ```

     Or you can just call `String::toUpperCase` directly on the string:

     ```java
     String result = str.toUpperCase(); // "ABC"
     ```

     If you must use a stream, iterate over `str.chars()`, convert each code point to a `String`, call `toUpperCase()`, and join.

6. **Question:** Make a Builder design pattern for a `Product` class.

   * **Candidate’s brief answer:**
     Defined a `public final class Product` with `private final String name`, `private final int price`, `private final String description`, plus a nested `public static class ProductBuilder` holding the same fields, setter methods returning `this`, and a `build()` method that calls `new Product(this)`. Then in `main()` they wrote:

     ```java
     Product laptop = Product.builder()
                             .setName("Dell")
                             .setPrice(3000)
                             .setDescription("High-end laptop")
                             .build();
     System.out.println("Product: " + laptop.getName() + ", Price: " + laptop.getPrice());
     ```
   * **Rating:** 9/10
   * **Your answer (correct):**

     ```java
     public class Product {
         private final String name;
         private final int price;
         private final String description;

         private Product(ProductBuilder builder) {
             this.name = builder.name;
             this.price = builder.price;
             this.description = builder.description;
         }

         public String getName() { return name; }
         public int getPrice() { return price; }
         public String getDescription() { return description; }

         public static ProductBuilder builder() {
             return new ProductBuilder();
         }

         public static class ProductBuilder {
             private String name;
             private int price;
             private String description;

             public ProductBuilder setName(String name) {
                 this.name = name;
                 return this;
             }
             public ProductBuilder setPrice(int price) {
                 this.price = price;
                 return this;
             }
             public ProductBuilder setDescription(String description) {
                 this.description = description;
                 return this;
             }
             public Product build() {
                 return new Product(this);
             }
         }
     }

     // Usage:
     public class Main {
         public static void main(String[] args) {
             Product laptop = Product.builder()
                                     .setName("Dell")
                                     .setPrice(3000)
                                     .setDescription("High-end laptop")
                                     .build();
             System.out.println("Product: " + laptop.getName() +
                                ", Price: " + laptop.getPrice() +
                                ", Description: " + laptop.getDescription());
         }
     }
     ```

7. **Question:** Suppose two threads are running in an execution block, and you don’t want either thread to be interrupted—what method(s) do you use to avoid interruption?

   * **Candidate’s brief answer:**
     “Use `try-catch` around thread code, or set a global uncaught exception handler via `Thread.setDefaultUncaughtExceptionHandler(...)`, or use the `synchronized` keyword for mutual exclusion.”
   * **Rating:** 4/10
   * **Your answer (correct):**
     To prevent interruption exceptions when two threads share a block:

     1. Wrap blocking calls (e.g., `Thread.sleep(…)`) in a `try { … } catch (InterruptedException e) { Thread.currentThread().interrupt(); }` to handle interrupts without terminating the thread.
     2. If you need to ensure mutual exclusion (so no thread can preempt the other in that block), use `synchronized(lockObject) { … }`. This prevents context switching inside that block until the lock is released.
     3. Avoid calling `thread.interrupt()` on those threads, or catch and ignore `InterruptedException` if you want the thread to continue.

8. **Question:** Suppose you want to write a REST API using Spring Boot—what initial steps do you take, and which annotations are needed?

   * **Candidate’s brief answer:**
     “Use Java (version 16) and Spring Boot 2.7.x (or 3.x). Add dependencies: `spring-boot-starter-web`, `spring-boot-starter-data-jpa`, H2 (demo), Lombok, and `spring-boot-starter-validation` if needed. Create an `@Entity` class for the database model (e.g., `Order`). Write an `@Repository` interface extending `JpaRepository<Order,Long>`. Create a `@Service` class with `@Autowired` repository. Finally, create an `@RestController` with `@RequestMapping("/orders")`, and inside methods like `@GetMapping`, `@PostMapping`, annotate parameters with `@RequestParam`, `@PathVariable`, or `@RequestBody`.”
   * **Rating:** 8/10
   * **Your answer (correct):**

     1. **Generate a Spring Boot project** (e.g., via start.spring.io) with dependencies:

        * `spring-boot-starter-web` (for REST controllers)
        * `spring-boot-starter-data-jpa` (for JPA)
        * A database driver (H2/MySQL/PostgreSQL)
        * Lombok (optional)
        * Validation (e.g., `spring-boot-starter-validation`)
     2. **Create an `@Entity` class** (e.g., `Order`) with fields annotated `@Id`, `@GeneratedValue`, and other mappings.
     3. **Define a repository** as `public interface OrderRepository extends JpaRepository<Order, Long> { }`.
     4. **Write a service** annotated `@Service` that injects `OrderRepository` (via constructor) to handle business logic.
     5. **Write a controller** annotated `@RestController` and `@RequestMapping("/orders")`, with methods annotated `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`. Use `@PathVariable` for IDs and `@RequestBody` for request payloads.
     6. **Annotate the main class** with `@SpringBootApplication` to bootstrap the application.

9. **Question:** What is the use of `@SpringBootApplication` annotation?

   * **Candidate’s brief answer:**
     “It’s a convenience annotation placed on the main class. It combines `@Configuration`, `@ComponentScan`, and `@EnableAutoConfiguration`. It bootstraps the Spring context, enables auto-configuration based on classpath dependencies, and triggers component scanning.”
   * **Rating:** 9/10
   * **Your answer (correct):**
     `@SpringBootApplication` is a shorthand annotation that bundles:

     * `@Configuration` (marks the class as a source of bean definitions)
     * `@EnableAutoConfiguration` (tells Spring Boot to auto-configure beans based on classpath and properties)
     * `@ComponentScan` (scans the package and its subpackages for `@Component`, `@Service`, `@Repository`, `@Controller`).
       Placed on the main application class, it bootstraps the Spring context when you call `SpringApplication.run(…)`.

10. **Question:** You know JPA—why do we use JPA instead of plain JDBC?

    * **Candidate’s brief answer:**
      “JPA (Java Persistence API) is a specification for ORM. It automates mapping Java objects (orders, products, customers, payments, inventory) to database tables. Without JPA, we’d write SQL and handle `ResultSet` and `PreparedStatement` manually. JPA handles that automatically via `@Entity`, `@Id`, relationships (`@OneToMany`, etc.).”
    * **Rating:** 8/10
    * **Your answer (correct):**
      JPA abstracts low-level JDBC, letting us map Java classes to database tables via annotations (`@Entity`, `@Id`, `@Column`, etc.) instead of writing SQL and parsing `ResultSet` manually. Benefits include:

      1. **Reduced boilerplate:** No need to write CRUD SQL; methods like `save()`, `findById()` come out-of-the-box.
      2. **Entity relationships:** Easily define `@OneToMany`, `@ManyToOne`, etc.
      3. **Transaction management:** Spring handles transactions declaratively.
      4. **Query derivation:** Derive queries from method names or use JPQL/Criteria API.
      5. **Portability:** JPA implementations (e.g., Hibernate) let you switch databases with minimal changes.

11. **Question:** Which scenario needs stored procedures?

    * **Candidate’s brief answer:**
      “Stored procedures (PL/SQL) encapsulate business logic in the database. Use them when you have complex logic requiring multiple database operations or heavy calculations—e.g., calculating order discounts with various rules, applying tax rates based on location or category. Stored procedures ensure consistent execution across applications, provide transactional integrity, performance optimizations, and security. They’re also useful for data transformations, aggregations, repetitive operations, and batch processing.”
    * **Rating:** 9/10
    * **Your answer (correct):**
      Stored procedures are best when:

      1. **Complex, reusable business logic** must run near the data (e.g., calculating discounts, tax rules, or inventory replenishment) so you avoid repeated SQL parsing.
      2. **Transactional integrity** is critical across multiple operations (all succeed or fail together).
      3. **Performance optimization:** Precompiled code in the database can run faster than dynamic SQL from the application.
      4. **Security:** Encapsulate data logic so applications can call a procedure without direct table access.
      5. **Batch processing:** Process large data sets (e.g., nightly updates) more efficiently on the database server.

---

**Overall Rating:** 8/10
