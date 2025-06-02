1. **Question:** So how much experience do you hold right now?

   **Candidate’s Answer (Brief):**
   “I have 5.4 years in IT, of which I’ve spent 4 years in Java and 2.5 years working with Spring Boot.”

   **Correct Answer:**
   A straightforward statement of total and relevant experience, e.g.: “I have 5.4 years in IT, including 4 years in Java development and 2.5 years specializing in Spring Boot.”

   **Rating:** 5/5
   *Justification:* The candidate clearly stated total years and broke down experience in Java and Spring Boot as requested.

2. **Question:** How many types of memory management are there in Java?

   **Candidate’s Answer (Brief):**
   “I think the JVM has three memory areas: heap, stack, and ‘control memory.’”

   **Correct Answer:**
   Java memory management typically refers to:

   * **Heap memory:** Stores all class instances and arrays.
   * **Stack memory:** Stores primitive local variables and call frames.
   * **Method Area (or Metaspace in newer JVMs):** Stores class metadata, static variables, and runtime constant pool.
   * **PC Registers and Native Method Stacks** can be mentioned in deeper JVM memory breakdown.

   **Rating:** 2/5
   *Justification:* The candidate correctly identified heap and stack but misnamed “method area” as “control memory” and omitted Metaspace/Method Area. They showed partial awareness but lacked precise terminology.

3. **Question:** What is the difference between `transient` and `volatile` variables?

   **Candidate’s Answer (Brief):**
   “`transient` is used during serialization so fields (like a password) aren’t stored. `volatile` ensures that updates to a variable in one thread are visible to all threads immediately.”

   **Correct Answer:**

   * **`transient`:** Marks a field to be skipped during Java serialization (`ObjectOutputStream`). Transient fields are not included in the serialized form.
   * **`volatile`:** Tells the JVM that a variable’s value may be modified by multiple threads. Reads/writes go directly to main memory (no caching), ensuring visibility of changes across threads.

   **Rating:** 5/5
   *Justification:* The candidate correctly described both keywords and their use cases.

4. **Question:** Why do we use `enum` in Java?

   **Candidate’s Answer (Brief):**
   “We use `enum` when we need a fixed set of constants, such as radio button choices like gender (Male, Female, Other). Based on the selection, we can handle logic accordingly.”

   **Correct Answer:**
   `enum` defines a type with a fixed set of named constants. It ensures type safety, can include methods/fields, and avoids magic strings or integers. Typical uses are days of the week, states, user roles, or fixed configurations (e.g., `enum Gender { MALE, FEMALE, OTHER }`).

   **Rating:** 4/5
   *Justification:* The candidate identified the core use—modeling fixed choices—but could have mentioned the type-safety and ability to add methods/fields to enums.

5. **Question:** How do you make a singleton class in Java?

   **Candidate’s Answer (Brief):**
   “I know a singleton class ensures only one instance is created to optimize memory, but I don’t have hands-on experience.”

   **Correct Answer:**
   A standard, thread-safe Singleton implementation:

   ```java
   public class Singleton {
       private static Singleton instance;
       private Singleton() { }
       public static synchronized Singleton getInstance() {
           if (instance == null) {
               instance = new Singleton();
           }
           return instance;
       }
   }
   ```

   Or the enum-based approach:

   ```java
   public enum Singleton {
       INSTANCE;
   }
   ```

   **Rating:** 2/5
   *Justification:* The candidate understood the purpose of a singleton but could not outline the implementation pattern (private constructor, static instance, `getInstance()` method), so the answer is incomplete.

6. **Question:** Suppose we have a final variable: `final int A = 10;` and we want to assign it to another variable `B` like `int B = A;`. Is that possible?

   **Candidate’s Answer (Brief):**
   “No, because once a variable is declared `final`, we cannot change its value. Assigning `B = A` would violate the final constraint.”

   **Correct Answer:**

   * You **can** assign a final variable’s value to a non-final variable:

     ```java
     final int A = 10;
     int B = A; // This is allowed, B becomes 10
     ```
   * What you cannot do is reassign `A` itself after initialization (`A = 5;` is illegal).

   **Rating:** 1/5
   *Justification:* The candidate incorrectly asserted that simply reading or assigning a final variable’s value is disallowed. They conﬂated “assign to another variable” with “reassigning the final variable” itself.

7. **Question:** How do you know the exception hierarchy? What is the superclass of all exception classes?

   **Candidate’s Answer (Brief):**
   “`Exception` is the superclass of all exception classes, and `Throwable` is the top of the hierarchy.”

   **Correct Answer:**
   The root is `java.lang.Throwable`. It has two main subclasses:

   * `java.lang.Error` (fatal errors)
   * `java.lang.Exception` (checked exceptions), which further divides into checked exceptions and `java.lang.RuntimeException` (unchecked).

   **Rating:** 4/5
   *Justification:* The candidate identified both `Exception` and `Throwable` but slightly misnamed which is the direct root. They said “`Exception` is the superclass” then corrected to “`Throwable` is the root.” Reasonably accurate.

8. **Question:** What is the superclass of Java?

   **Candidate’s Answer (Brief):**
   “`Object` class.”

   **Correct Answer:**
   Every class in Java (except `Object` itself) implicitly extends `java.lang.Object`. Therefore, `Object` is the ultimate base class.

   **Rating:** 5/5
   *Justification:* Correct.

9. **Question:** Can you name three to four methods that belong to the `Object` class?

   **Candidate’s Answer (Brief):**
   “`equals()`, `toString()`, `hashCode()`, `clone()`. ”

   **Correct Answer:**
   Common `Object` methods include `equals(Object)`, `hashCode()`, `toString()`, `clone()`, `getClass()`, `finalize()`, and `notify()/wait()/notifyAll()`.

   **Rating:** 5/5
   *Justification:* The candidate listed valid, major `Object` methods.

10. **Question:** Suppose you’re working in a project and need to avoid duplicate methods: Developer A and Developer B write methods with the same name but different parameters. How do you avoid that?

    **Candidate’s Answer (Brief):**
    “You can use method overloading by giving the same method name but different parameter signatures.”

    **Correct Answer:**
    To avoid duplicate method names with different purposes, you can:

    * Use **method overloading** (same name, different parameter types or counts).
    * Ensure a shared utility or base class defines the common method so both developers call the same implementation instead of duplicating.
    * Employ code reviews and consistent naming conventions.

    **Rating:** 4/5
    *Justification:* The candidate mentioned method overloading correctly but did not discuss code organization (e.g., shared utility class or code review process). Still, they addressed the technical mechanism.

11. **Question:** Suppose you want to create one common method that can be called from any class. How do you write it?

    **Candidate’s Answer (Brief):**
    “In a `public class Test`, write a `public void add(...) { ... }` method inside, and any other class can call `new Test().add(...)`.”

    **Correct Answer:**
    You can define a **static utility method** in a public class, for example:

    ```java
    public class Utils {
        public static void add(int x, int y) {
            // implementation
        }
    }
    ```

    Then any class calls `Utils.add(3, 4)`. Or, for an instance method, declare it `public` in a shared class so all can instantiate and invoke it:

    ```java
    public class Common {
        public void add(int x, int y) { ... }
    }
    ```

    **Rating:** 3/5
    *Justification:* The candidate showed how to declare a public method but did not mention using `static` for a truly “common” utility method. Their example works but lacks detail on best practice.

12. **Question:** In the collection framework, what is the major difference between `TreeSet` and `HashSet`?

    **Candidate’s Answer (Brief):**
    “Both implement `Set`, which disallows duplicates. `HashSet` does not preserve any order (“random order”), while `TreeSet` maintains sorted order.”

    **Correct Answer:**

    * **`HashSet`:** Backed by a hash table; O(1) average time for add/contains operations; does not guarantee any iteration order.
    * **`TreeSet`:** Backed by a Red-Black tree; O(log n) time for most operations; always iterates in sorted (natural or provided comparator) order. Both reject duplicates.

    **Rating:** 5/5
    *Justification:* The candidate correctly identified duplicate prohibition and ordering differences.

13. **Question:** Given the code snippet (with two overloaded `some()` methods, one taking an `Object` parameter and the other a `String`), and calling `some(null)`, which method is invoked first: the `String`-typed version or the `Object`-typed version?

    **Candidate’s Answer (Brief):**
    Guessed “Object type” first, then was told it was wrong. They did not explicitly give the correct answer.

    **Correct Answer:**
    When `some(null)` is called, the **most specific overload** is chosen. Since `String` is more specific than `Object`, the `some(String s)` method is invoked.

    **Rating:** 1/5
    *Justification:* The candidate guessed incorrectly and failed to correct themselves. They lacked understanding of overload resolution rules.

14. **Question:** Do you know serialization? Can you describe a scenario where serialization is used?

    **Candidate’s Answer (Brief):**
    “Yes. For serialization, we use `FileInputStream`/`FileOutputStream`. When writing a REST API, data is sent over the network in serialized form.”

    **Correct Answer:**
    **Serialization** converts an object into a byte stream so it can be saved (e.g., to a file or database) or transmitted (e.g., over a network). Deserialization reconstructs the object from that byte stream. Scenarios include:

    * Persisting Java objects to disk (`ObjectOutputStream/FileOutputStream`).
    * Sending objects across a socket or REST call (e.g., JSON or binary protocols).
    * Caching objects in memory grids or messaging systems.

    **Rating:** 2/5
    *Justification:* The candidate mentioned file streams but conflated “REST API serialization” (usually JSON/XML) with Java’s `Serializable` mechanism. They showed only a basic awareness.

15. **Question:** Suppose you are writing a REST API—how will serialization/deserialization be handled?

    **Candidate’s Answer (Brief):**
    “For a REST API, data passes over the network in serialized mode.”

    **Correct Answer:**
    In a typical Spring Boot REST API, serialization/deserialization is handled by a message converter (e.g., Jackson).

    * **Serialization:** Converting a Java object (POJO) to JSON (or XML) for the HTTP response.
    * **Deserialization:** Converting JSON payload in an HTTP request into a Java object (POJO).

    **Rating:** 2/5
    *Justification:* The candidate repeated a vague statement without mentioning the framework’s role (Jackson) or how data binding occurs.

16. **Question:** You know immutable objects. If you want to create a custom immutable object, what would you write?

    **Candidate’s Answer (Brief):**
    “Use `final` and factory design pattern.”

    **Correct Answer:**
    To create an immutable class in Java:

    1. Declare the class as `final` (to prevent subclassing).
    2. Make all fields `private final`.
    3. No setters—only getters.
    4. Initialize all fields via a constructor (or static factory method).
    5. If any field is a mutable object, return a defensive copy in getters.
       Example:

    ```java
    public final class Person {
        private final String name;
        private final int age;
        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
        public String getName() { return name; }
        public int getAge() { return age; }
    }
    ```

    **Rating:** 1/5
    *Justification:* The candidate’s answer was too high-level and didn’t specify key steps (e.g., private final fields, no setters, defensive copies). Mentioning “factory pattern” without detail isn’t sufficient.

17. **Question:** What is the use of `@SpringBootApplication` in Spring?

    **Candidate’s Answer (Brief):**
    “`@SpringBootApplication` combines `@EnableAutoConfiguration` and `@ComponentScan`. You put it on the main class. It starts the application, scans components (`@Controller`, `@Service`, `@Repository`), and auto-configures the JAR dependencies.”

    **Correct Answer:**
    `@SpringBootApplication` is a convenience annotation that combines:

    * `@Configuration` (designates the class as a source of bean definitions),
    * `@EnableAutoConfiguration` (enables Spring Boot’s auto-configuration based on classpath), and
    * `@ComponentScan` (scans the package for Spring components).
      It serves as the entry point to start the application and automatically wire all necessary beans.

    **Rating:** 5/5
    *Justification:* The candidate accurately described what `@SpringBootApplication` does.

18. **Question:** Why are we using Spring Boot rather than Spring MVC?

    **Candidate’s Answer (Brief):**
    They started to answer but did not complete before time ended.

    **Correct Answer:**

    * **Spring Boot** provides auto-configuration, starter dependencies, an embedded server, and production-ready features (Actuator), reducing boilerplate.
    * **Spring MVC** (or Spring Framework) requires manual configuration (XML or Java config) and separate servlet container setup.
      Spring Boot simplifies application setup and deployment compared to traditional Spring MVC.

    **Rating:** 1/5
    *Justification:* The candidate did not provide an answer within the time.

19. **Question:** What is the DispatcherServlet?

    **Candidate’s Answer (Brief):**
    “DispatcherServlet is the IOC container. It reads objects from the XML configuration file.”

    **Correct Answer:**
    In Spring MVC, **DispatcherServlet** is the front controller that intercepts all HTTP requests, consults one or more `HandlerMapping` to route to the appropriate controller, invokes the controller method, and then uses a `ViewResolver` to render the response. It is not the IOC container itself but part of the web layer.

    **Rating:** 2/5
    *Justification:* The candidate conflated DispatcherServlet with the IOC container and configuration loading. They did not explain its role as front controller.

20. **Question:** Do you know ViewResolver? How does it work?

    **Candidate’s Answer (Brief):**
    “I know it, but I don’t remember right now.”

    **Correct Answer:**
    **ViewResolver** in Spring MVC maps logical view names returned by controllers to actual view implementations (e.g., JSP, Thymeleaf templates). For example, “home” → `/WEB-INF/views/home.jsp`. It uses prefix/suffix configuration to form the real resource path.

    **Rating:** 1/5
    *Justification:* The candidate said they recognized it but could not explain its functionality.

21. **Question:** Do you know Actuator? What is it?

    **Candidate’s Answer (Brief):**
    “Actuator is a Spring dependency used to monitor application status.”

    **Correct Answer:**
    Spring Boot **Actuator** adds production-ready endpoints (e.g., `/actuator/health`, `/actuator/metrics`, `/actuator/info`). It provides health checks, metrics, application info, thread dumps, and other operational data.

    **Rating:** 4/5
    *Justification:* The candidate captured the monitoring purpose but could have named specific endpoints or features.

22. **Question:** In your database, what do you know about stored procedures and functions?

    **Candidate’s Answer (Brief):**
    “I know functions and queries. For a complex query in PostgreSQL, we use functions to fetch specific data. Advantage: we can fix logic at the function level without affecting other code.”

    **Correct Answer:**

    * **Stored Procedure:** A set of SQL statements stored in the database, can perform DML (INSERT/UPDATE/DELETE), return multiple result sets, and doesn’t necessarily return a single value. Used for encapsulating logic and improving performance.
    * **Stored Function:** Returns a single value and can be used in a `SELECT` statement. Use for computed values or reusable logic in queries.

    **Rating:** 3/5
    *Justification:* The candidate knew when they would use a function for a complex query but didn’t distinguish clearly between procedures and functions or mention that functions return a value and can be called within SQL.

23. **Question:** How many types of joins are there?

    **Candidate’s Answer (Brief):**
    “Four types of joins: inner join, outer join, left join, full join, and right join.”

    **Correct Answer:**
    Standard join types:

    * **INNER JOIN**
    * **LEFT (OUTER) JOIN**
    * **RIGHT (OUTER) JOIN**
    * **FULL (OUTER) JOIN**
    * **CROSS JOIN** (Cartesian product)
    * **SELF JOIN** (joining a table to itself)

    **Rating:** 2/5
    *Justification:* The candidate said “four types” but listed five categories. They conflated “outer join” with left/right/full. They missed `CROSS JOIN` and `SELF JOIN`.

24. **Question:** What is a LEFT JOIN? Provide an example.

    **Candidate’s Answer (Brief):**
    “With `LEFT JOIN`, if we have two tables `cricket` (left) and `football` (right), all rows from `cricket` are printed. For football players who are also in cricket, print their data; otherwise, print `NULL` for the football side.”

    **Correct Answer:**
    `LEFT JOIN` returns all rows from the left table and matching rows from the right. Example:

    ```sql
    SELECT c.player_name, f.team
    FROM cricket c
    LEFT JOIN football f ON c.player_id = f.player_id;
    ```

    This lists every cricket player; if they also play football, shows their football team; otherwise, `f.team` is `NULL`.

    **Rating:** 5/5
    *Justification:* The candidate described the behavior correctly with a suitable example.

25. **Question:** What is `UNION ALL`?

    **Candidate’s Answer (Brief):**
    “`UNION` prints common values for both tables.”

    **Correct Answer:**

    * **`UNION`:** Combines results of two queries and removes duplicates.
    * **`UNION ALL`:** Combines results of two queries including duplicates.

    **Rating:** 1/5
    *Justification:* The candidate’s answer is incorrect: they described `UNION` behavior but not `UNION ALL`. They did not address that `UNION ALL` preserves duplicates.

---

**Overall Assessment:**

* **Strengths:** Clear on personal experience, basic OOP (heap vs. stack), `transient` vs. `volatile`, `enum`, collections (`TreeSet` vs. `HashSet`), left join syntax.
* **Areas for Improvement:** Overload resolution, `final` variable semantics, Java memory areas (“Method Area” vs. “control memory”), proper Singleton implementation, Spring MVC internals (`DispatcherServlet`, `ViewResolver`), REST serialization mechanism, database joins taxonomy, and `UNION ALL` semantics.
* **Average Score Across All Questions:** 2.8/5
