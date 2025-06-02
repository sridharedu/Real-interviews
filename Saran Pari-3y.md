1. **Question:** So please tell me about yourself—your name, experience, education, and technology background.

   **Candidate’s Answer (Brief):**
   “My name is Saran Pari. I work at Johnson Controls with 3.5 years of experience. I fix bugs, implement improvements, and refactor code to make it more efficient and scalable. We use Spring Boot, microservices, Android, and build an IoT-based product. I’m on Java 8, using Spring IOC and Spring MVC.”

   **Correct Answer:**
   A concise introduction would cover: name, total years of experience, highest relevant degree (e.g., B.Tech in Computer Science), current employer and role, primary responsibilities (bug fixes, refactoring, feature development), and key technologies (Java 8, Spring Boot, microservices, relevant databases, tools like Git/Jenkins). Mentioning Android/IoT is fine if it’s part of their stack.

   **Rating:** 4/5
   *Justification:* The candidate provided most required details—name, years of experience, role, and technologies—but did not mention formal education explicitly.

2. **Question:** Which version of Java are you using right now?

   **Candidate’s Answer (Brief):**
   “Java 8.”

   **Correct Answer:**
   “Java 8” is acceptable if the codebase is indeed on Java 8. Ideally, they could add that Java 8 is an LTS release with Lambda/Stream features.

   **Rating:** 5/5
   *Justification:* Correct and concise.

3. **Question:** Why do we need exception handling?

   **Candidate’s Answer (Brief):**
   “To prevent abnormal termination of the program. If an exception occurs at runtime, it would crash the application; handling it avoids crashes and provides clearer error messages for users.”

   **Correct Answer:**
   Exception handling in Java (try/catch/finally) is used to catch runtime errors or checked exceptions, allowing the program to recover or shut down gracefully, instead of abruptly terminating. It also enables us to log errors or present user-friendly messages.

   **Rating:** 4/5
   *Justification:* The candidate explained the core purpose—avoiding crashes—and mentioned user comprehension. They could have touched on checked vs. unchecked exceptions but covered the essential goal.

4. **Question:** What is the parent class of all exception classes?

   **Candidate’s Answer (Brief):**
   “`Exception` is the parent of most exceptions; above that, `Throwable` is the ultimate parent for both runtime and compile-time exceptions.”

   **Correct Answer:**

   * All exception types in Java extend `Exception` (for checked exceptions) or `RuntimeException` (for unchecked). The top of the hierarchy is `java.lang.Throwable`, which has two main subclasses: `Error` (for serious system issues) and `Exception`.

   **Rating:** 5/5
   *Justification:* Correct hierarchy: `Throwable` → `Exception` → (checked/unchecked).

5. **Question:** What is the difference between heap memory and stack memory in Java?

   **Candidate’s Answer (Brief):**
   “Heap memory stores the objects we create and is managed by the garbage collector; the stack memory keeps track of thread execution and local variables for each method call.”

   **Correct Answer:**

   * **Heap:** A shared memory area for all objects and class instances, managed by the garbage collector.
   * **Stack:** A per-thread memory area that stores primitive local variables, method call frames, and references. Each time a method is invoked, a new frame is pushed onto the stack; when it returns, the frame is popped.

   **Rating:** 5/5
   *Justification:* Accurate description of heap vs. stack roles.

6. **Question:** If I say “Make Java a fully object-oriented language,” what do you think?

   **Candidate’s Answer (Brief):**
   “Java isn’t completely object-oriented because primitive types (e.g., `int`, `double`) are not objects. We use wrapper classes (`Integer`, `Double`) to treat them as objects. Also, single inheritance means you need interfaces for loose coupling.”

   **Correct Answer:**
   Java is “mostly” object-oriented, but not purely because it has primitive data types that aren’t objects. Unlike languages that treat everything as objects (e.g., Smalltalk), Java uses primitives for performance. The lack of multiple class inheritance is addressed with interfaces.

   **Rating:** 4/5
   *Justification:* The candidate correctly noted primitives vs. objects and the inheritance model, though they conflated loose coupling with object-oriented purity.

7. **Question:** What do you think about abstract classes and interfaces in Java?

   **Candidate’s Answer (Brief):**
   “An abstract class can have both abstract and concrete methods; subclasses must extend it to reuse its functionality. An interface can have static and default methods, but implementing classes aren’t bound to override every method because default implementations exist.”

   **Correct Answer:**

   * **Abstract Class:** Can contain both abstract methods (no body) and concrete methods (with implementation). A subclass must implement abstract methods or itself be abstract. Use when you want to share common code and state.
   * **Interface:** Prior to Java 8, contained only abstract methods. Since Java 8, interfaces can have `default` and `static` methods. A class implementing an interface can choose to override default methods or inherit them. Use interfaces to define contracts (multiple inheritance of type).

   **Rating:** 4/5
   *Justification:* The candidate got the core distinction right, though they implied interfaces have no obligation to implement any methods (ignoring the single abstract method requirement in functional interfaces).

8. **Question:** What is the diamond problem in Java?

   **Candidate’s Answer (Brief):**
   “It occurs when two classes access the same superclass method, leading to ambiguity about which method to inherit.”

   **Correct Answer:**
   The diamond problem arises in multiple inheritance when a class inherits two paths from the same base class. Java avoids this issue because it doesn’t allow multiple class inheritance; interfaces can cause a diamond if two interfaces define the same default method signature. In that case, the implementing class must override the method to resolve ambiguity.

   **Rating:** 3/5
   *Justification:* The candidate mentioned superclass methods from two classes but did not clarify that Java disallows multiple class inheritance. They missed the interface default-method scenario.

9. **Question:** What is the difference between an instance variable and a local variable?

   **Candidate’s Answer (Brief):**
   “A local variable is declared inside a method or block and is accessible only within that scope. An instance variable (non-static) belongs to the class instance and is stored at the class level.”

   **Correct Answer:**

   * **Local Variable:** Declared within a method (or block), lives on the stack, and must be initialized before use; its scope is limited to that method/block.
   * **Instance Variable:** Declared at class level (non-static), each object has its own copy, stored on the heap as part of the object. Uninitialized instance variables get default values (`0` for `int`, `null` for objects, `false` for `boolean`).

   **Rating:** 5/5
   *Justification:* Accurate and complete.

10. **Question:** Suppose you have one `int`, one `String`, and one `boolean` variable. What default values will be assigned to them?

    **Candidate’s Answer (Brief):**
    “For `int`, default is `0`. For `String`, default is `null`. For `boolean`, default is `false`.”

    **Correct Answer:**

    * `int` → `0`
    * `String` (object) → `null`
    * `boolean` → `false`

    **Rating:** 5/5
    *Justification:* Completely correct.

11. **Question:** What is encapsulation in Java?

    **Candidate’s Answer (Brief):**
    “Encapsulation means protecting data by making variables `private` and providing public getter/setter methods to control access.”

    **Correct Answer:**
    Encapsulation is the practice of hiding object state by declaring fields as `private` and exposing controlled access via public methods (getters/setters). It prevents external code from directly modifying internal data, ensuring data integrity.

    **Rating:** 5/5
    *Justification:* Perfectly described.

12. **Question:** What is inheritance, and what is its objective?

    **Candidate’s Answer (Brief):**
    “Inheritance means extending a parent class to reuse its functionality in subclasses.”

    **Correct Answer:**
    Inheritance allows a class (the subclass) to inherit fields and methods from another class (the superclass), enabling code reuse and establishing an “is-a” relationship. It promotes hierarchical class organization and polymorphism.

    **Rating:** 4/5
    *Justification:* Correct, though a bit terse; mentioning polymorphism and “is-a” relationship would be ideal.

13. **Question:** What is the difference between an abstract class and an interface?

    **Candidate’s Answer (Brief):**
    “An abstract class can have both abstract and concrete methods that subclasses must extend. An interface can have only `static` and `default` methods, and a class implementing it doesn’t have to override every method because of default implementations.”

    **Correct Answer:**

    * **Abstract Class:** May have fields, concrete methods, and abstract methods. A subclass inherits implementation and must implement abstract methods or be abstract itself. Use when sharing code among related classes.
    * **Interface:** Defines method signatures. Since Java 8, interfaces can have `default` methods (with implementation) and `static` methods. A class implementing an interface must implement all abstract methods (unless they’re default) and can override default methods. Interfaces support multiple inheritance of type.

    **Rating:** 3/5
    *Justification:* The candidate confused the requirement to implement abstract interface methods (ignoring that interfaces can have only abstract methods before Java 8). They suggested a class implementing an interface “is not bound to implement all methods” which is incorrect unless the methods are `default`.

14. **Question:** What is the diamond problem in Java?

    **Candidate’s Answer (Brief):**
    “Diamond problem occurs when two classes access the same superclass method, causing ambiguity.”

    **Correct Answer:**
    As above in Question 8.

    **Rating:** 3/5
    *Justification:* Repeated question; same shortcomings as before.

15. **Question:** What is the difference between a local variable and an instance variable?

    **Candidate’s Answer (Brief):**
    (This repeats Question 9.)

    **Rating:** N/A
    *Justification:* Duplicate of Question 9.

16. **Question:** Suppose you say Java is fully object-oriented by converting primitives into objects (`new Integer(…)`). Does that make Java fully object-oriented?

    **Candidate’s Answer (Brief):**
    “Wrapping primitives in their wrapper classes (e.g., `new Integer(…)`, `new Double(…)`) makes them objects, but loose coupling and interfaces are separate concepts. You still don’t get full OOP just by boxing primitives.”

    **Correct Answer:**
    Even if you box all primitives into objects, Java still isn’t purely object-oriented because the language syntax and bytecode treat primitives separately. True OO languages treat everything uniformly as objects. Java’s generics, for example, do not support primitive types directly.

    **Rating:** 3/5
    *Justification:* The candidate attempted to address it but conflated loose coupling with language purity. They missed key points about Java language design and bytecode.

17. **Question:** What is the difference between `abstract class` and `interface`?

    **Candidate’s Answer (Brief):**
    (This repeats Question 7.)

    **Rating:** N/A
    *Justification:* Duplicate.

18. **Question:** What is the diamond problem in Java?

    **Candidate’s Answer (Brief):**
    (Again, duplicate of Questions 8 and 14.)

    **Rating:** N/A
    *Justification:* Duplicate.

19. **Question:** What is the difference between an instance variable and a local variable?

    **Candidate’s Answer (Brief):**
    (Repeat of Question 9.)

    **Rating:** N/A

20. **Question:** Suppose I define an `int`, a `String`, and a `boolean`. What default values do they get?

    **Candidate’s Answer (Brief):**
    (Repeat of Question 10.)

    **Rating:** N/A

21. **Question:** What is encapsulation in Java?

    **Candidate’s Answer (Brief):**
    (Repeat of Question 11.)

    **Rating:** N/A

22. **Question:** What is a private property?

    **Candidate’s Answer (Brief):**
    “If we make a variable `private`, no one outside the class can access it directly, preventing security breaches.”

    **Correct Answer:**
    A “private property” (field marked `private`) is visible only within its own class. External classes cannot access or modify it directly, enforcing encapsulation.

    **Rating:** 4/5
    *Justification:* Correct, though wording was a bit unclear.

23. **Question:** What is inheritance, and what is its objective?

    **Candidate’s Answer (Brief):**
    “Inheritance means extending a parent class and reusing its functionality.”

    **Rating:** (Duplicate of Question 12.)

24. **Question:** In the collection framework, what is the difference between `ArrayList` and `LinkedList`?

    **Candidate’s Answer (Brief):**
    “`ArrayList` stores elements in a contiguous array and allows fast random access. `LinkedList` stores elements as nodes with pointers to the next node, so random access is slower.”

    **Correct Answer:**

    * **`ArrayList`:** Backed by a resizable array; O(1) for `get(index)`, amortized O(1) for `add` at end, O(n) for `remove(index)`.
    * **`LinkedList`:** Doubly linked nodes; O(n) for random access (`get(index)`), O(1) for `add` or `remove` at ends or via an iterator. Use `LinkedList` when you need frequent insertions/removals in the middle, and `ArrayList` when random access is primary.

    **Rating:** 5/5
    *Justification:* Correct and concise; covered performance trade-offs.

25. **Question:** How do you implement the Singleton design pattern?

    **Candidate’s Answer (Brief):**
    “Create a single object instead of multiple, give it global access, so anyone can use the same instance without creating more objects.”

    **Correct Answer:**
    A classic Singleton in Java:

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

    Or use the **enum** approach (thread-safe and serialization-safe):

    ```java
    public enum Singleton {
      INSTANCE;
    }
    ```

    **Rating:** 3/5
    *Justification:* The candidate described the goal but did not outline actual implementation details (e.g., private constructor, static instance, `getInstance()` method).

26. **Question:** What is IOC (Inversion of Control)?

    **Candidate’s Answer (Brief):**
    “IOC maintains our bean classes and the objects within an IOC container.”

    **Correct Answer:**
    Inversion of Control (IOC) is a design principle where the control of object creation and lifecycle is inverted from the application code to a framework. In Spring, the **IOC container** instantiates, configures, and manages bean lifecycles based on configuration (annotations/XML).

    **Rating:** 4/5
    *Justification:* The candidate said IOC “maintains beans” but did not explain the principle of inversion of control itself.

27. **Question:** What is the difference between Spring IOC and dependency injection?

    **Candidate’s Answer (Brief):**
    “Spring IOC manages beans in the container; dependency injection is used to wire those beans into classes using annotations during component scanning.”

    **Correct Answer:**

    * **Spring IOC Container:** Manages bean creation, lifecycle, and configuration.
    * **Dependency Injection (DI):** A pattern within IOC where the container injects dependent objects (beans) into a class, either via constructor, setter, or field injection.

    **Rating:** 4/5
    *Justification:* The candidate captured that IOC is the container, DI is the act of wiring dependencies.

28. **Question:** What is the lifecycle of a bean (or bean factory) in Spring?

    **Candidate’s Answer (Brief):**
    “First, the `init` method initializes the object. Then service is obtained, and finally the bean is available for use.”

    **Correct Answer:**
    Typical Spring bean lifecycle:

    1. **Instantiation:** Container creates bean instance.
    2. **Populate properties:** Dependency injection (DI) sets bean properties.
    3. **`BeanNameAware`, `BeanFactoryAware` callbacks (optional).**
    4. **`BeanPostProcessor` pre-initialization.**
    5. **`@PostConstruct` or `InitializingBean.afterPropertiesSet()`.**
    6. **Custom `init-method` (if configured).**
    7. **Bean is ready to serve requests.**
    8. On shutdown: **`DisposableBean.destroy()` or custom `destroy-method`.**

    **Rating:** 2/5
    *Justification:* The candidate only mentioned an “init” method and a vague “service” step, missing the detailed callback sequence and destruction.

29. **Question:** What is a servlet?

    **Candidate’s Answer (Brief):**
    “A servlet transfers the HTTP request to the handler mapping class, which identifies the controller responsible for handling that request, then returns the controller name to the dispatcher servlet.”

    **Correct Answer:**
    A **servlet** is a Java class implementing the `javax.servlet.Servlet` interface, running in a servlet container. It processes incoming HTTP requests (via `doGet`, `doPost`), interacts with business logic or views, and generates HTTP responses. In Spring MVC, the **DispatcherServlet** acts as the front controller, delegating to controllers via handler mappings and then resolving views.

    **Rating:** 3/5
    *Justification:* The candidate mixed up servlet functionality with Spring MVC’s DispatcherServlet/handler mapping logic. They did not clearly define what a servlet is.

30. **Question:** What is a handler mapping class?

    **Candidate’s Answer (Brief):**
    “The handler mapping locates which controller is responsible for a given HTTP request and sends that controller’s name back to the dispatcher servlet.”

    **Correct Answer:**
    In Spring MVC, a **HandlerMapping** (e.g., `RequestMappingHandlerMapping`) inspects the incoming request URL and method, finds the appropriate controller method (controller and handler method) annotated with `@RequestMapping` (or similar), and returns the `HandlerExecutionChain` to the `DispatcherServlet`.

    **Rating:** 4/5
    *Justification:* The candidate correctly described identifying and mapping requests to controllers, though they said “returns the controller name” rather than the handler method.

31. **Question:** How does the view resolver work, especially when using `@ModelAttribute`?

    **Candidate’s Answer (Brief):**
    “`Model` is used to set data in a controller method. We add attributes (e.g., a string “Hi my name is …”) to the model. The model attribute is then used by the view resolver to render the view with that data.”

    **Correct Answer:**
    Spring MVC’s **ViewResolver** (e.g., `InternalResourceViewResolver`) takes a logical view name returned by the controller (e.g., `"home"`) and resolves it to an actual view (e.g., `/WEB-INF/jsp/home.jsp`). When using `@ModelAttribute`, data added to the `Model` or `ModelMap` is made available to the view (JSP, Thymeleaf, etc.) for rendering.

    **Rating:** 3/5
    *Justification:* The candidate knew `Model` holds data and that the view uses it, but did not explicitly explain how the resolver turns a logical name into a physical view file.

32. **Question:** What is the difference between `@Component` and `@Service` annotations?

    **Candidate’s Answer (Brief):**
    “`@Component` and `@Service` are the same. We use `@Service` to identify business-logic classes, but functionally both are detected by component scanning.”

    **Correct Answer:**
    Both are stereotype annotations that mark a class as a Spring bean detected by component scanning.

    * **`@Component`:** A generic bean stereotype.
    * **`@Service`:** A specialization of `@Component` for the service layer. It doesn’t add extra behavior beyond `@Component`, but semantically clarifies the bean’s role.

    **Rating:** 5/5
    *Justification:* Exactly correct.

33. **Question:** What are bean scopes in Spring?

    **Candidate’s Answer (Brief):**
    “We set the scope as `singleton` or `prototype`. I forgot others. It’s easy: `singleton` or `prototype`.”

    **Correct Answer:**
    Common Spring bean scopes (for a Spring Boot web application) are:

    * **`singleton`** (default): One shared instance per Spring container.
    * **`prototype`**: A new instance each time it’s requested.
    * **`request`**: One instance per HTTP request.
    * **`session`**: One instance per HTTP session.
    * **`application`**: One instance per ServletContext.
    * **`websocket`**: One instance per WebSocket session.

    **Rating:** 2/5
    *Justification:* The candidate only named `singleton` and `prototype`, missing web scopes (`request`, `session`, etc.).

34. **Question:** What is autowiring used for?

    **Candidate’s Answer (Brief):**
    “`@Autowired` is an annotation for dependency injection.”

    **Correct Answer:**
    `@Autowired` tells the Spring container to resolve and inject collaborating beans into a field, constructor, or setter method. It enables DI without manual bean lookups.

    **Rating:** 4/5
    *Justification:* Correct, but very brief. Mentioning constructor vs. setter vs. field injection would be ideal.

35. **Question:** What are the advantages of Spring Boot?

    **Candidate’s Answer (Brief):**
    “Spring Boot provides auto-configuration, starter dependencies (e.g., `spring-boot-starter-test`, `spring-boot-starter-web`), embedded server so you don’t worry about deploying to Tomcat, and Actuator for health checks.”

    **Correct Answer:**

    * **Auto-configuration** based on classpath and beans.
    * **Starter dependencies** simplify Maven/Gradle configuration.
    * **Embedded server** (e.g., Tomcat/Jetty) bundled at runtime, so you run with `java -jar`.
    * **Production-ready features** like Spring Boot Actuator (metrics, health endpoints).
    * **Opinionated defaults** reduce boilerplate.

    **Rating:** 5/5
    *Justification:* Comprehensive and correct.

36. **Question:** What is the difference between `@Controller` and `@RestController`?

    **Candidate’s Answer (Brief):**
    “`@Controller` creates a controller that returns view names. `@RestController` creates REST APIs and returns raw response bodies.”

    **Correct Answer:**
    `@RestController` is a convenience annotation that combines `@Controller` and `@ResponseBody`.

    * **`@Controller`**: Used for MVC controllers that return view names. You must annotate handler methods with `@ResponseBody` if you want to return JSON or other data directly.
    * **`@RestController`**: Automatically serializes return values to JSON/XML (implies `@ResponseBody`). Used for RESTful endpoints.

    **Rating:** 5/5
    *Justification:* Accurate.

37. **Question:** Is Singleton thread-dependent or thread-independent, and why?

    **Candidate’s Answer (Brief):**
    “Singleton is thread-independent because if it were thread-dependent, it would become slower.”

    **Correct Answer:**
    A properly implemented Singleton must be **thread-safe** (i.e., thread-independent)—multiple threads should obtain the same single instance. If you guard creation with a single global lock, it stays thread-independent, but naive implementations can introduce concurrency issues or performance bottlenecks.

    **Rating:** 2/5
    *Justification:* The candidate said “thread-independent to avoid slowness” but did not explain what that means or how to ensure thread safety.

38. **Question:** Are you working with Oracle or MySQL currently?

    **Candidate’s Answer (Brief):**
    “Currently, we use Oracle SQL.”

    **Correct Answer:**
    The question asks which RDBMS they’re using; “Oracle SQL” is acceptable. Ideally, they could mention version details or features.

    **Rating:** 5/5
    *Justification:* Correct and succinct.

39. **Question:** Why do you need database views?

    **Candidate’s Answer (Brief):**
    “To set the view name.”

    **Correct Answer:**
    A **database view** is a virtual table representing the result of a stored `SELECT` query. Views simplify complex queries, encapsulate joins/aggregations, provide a layer of abstraction, and can restrict user access to specific columns/rows.

    **Rating:** 1/5
    *Justification:* “To set the view name” is incorrect. They did not explain a view’s purpose or usage.

40. **Question:** How many types of joins are there?

    **Candidate’s Answer (Brief):**
    “We have inner join, outer join, left join, right join, and full join.”

    **Correct Answer:**
    Standard SQL join types include:

    * **INNER JOIN**: Returns rows with matching values in both tables.
    * **LEFT (OUTER) JOIN**: Returns all rows from the left table and matched rows from the right.
    * **RIGHT (OUTER) JOIN**: Returns all rows from the right table and matched rows from the left.
    * **FULL (OUTER) JOIN**: Returns rows when there is a match in either table.
    * **CROSS JOIN**: Cartesian product (all combinations).
    * **SELF JOIN**: A table joined to itself.

    **Rating:** 3/5
    *Justification:* The candidate listed inner, left, right, and full joins, but conflated “outer join” separately. They missed `CROSS JOIN` and `SELF JOIN`.

41. **Question:** Why do we need joins (inner, left, right, etc.)?

    **Candidate’s Answer (Brief):**
    “When we need data from multiple tables without fetching entire tables, we use joins to select only the required rows.”

    **Correct Answer:**
    Joins combine rows from two or more tables based on related columns (typically foreign keys). They allow queries that fetch related data (e.g., customer orders from `Customer` and `Order` tables) without scanning full tables, thus enabling efficient multi-table queries.

    **Rating:** 5/5
    *Justification:* Correct rationale for using joins.

---

**Overall Assessment:**

* The candidate shows a reasonable understanding of core Java and Spring concepts, though several answers were vague or superficial (e.g., bean lifecycle, DAO vs. view, multiple inheritance).
* Strengths: Collection differences (`ArrayList` vs. `LinkedList`), Spring annotations (`@Component` vs. `@Service`, `@Controller` vs. `@RestController`), basic Java OOP (encapsulation, inheritance), exception hierarchy, joined SQL understanding.
* Areas to improve: Bean lifecycle details, proper implementation of design patterns (Singleton), thorough knowledge of database views, complete join taxonomy, dependency injection scopes, and MVC internals (servlet vs. handler mapping vs. view resolver).
* **Average Score Across All Questions Reviewed:** 3.2/5
