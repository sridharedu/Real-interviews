Below is a question‐by‐question breakdown. For each interview question, you’ll see:

1. **The question** as asked by the interviewer.
2. **The candidate’s answer** (summarized).
3. **A rating (out of 10)** reflecting completeness, correctness, and depth.

---

1. **Q: “Please introduce yourself and tell us about your most recent project.”**
   **A:**

   * Joined current org 7 years ago as a Big Data developer; that project was scrapped after three months.
   * Switched to a healthcare REST‐API project (Java/Spring), which ran for about a year.
   * Since then mostly REST-API work; past six months also handling CI/CD (using an in-house tool called Quark instead of Jenkins).
   * Current project leverages a “microservices‐style” architecture: three independently deployed components (React front-end; a Spring Boot “validation” service that reads huge JSON metadata from GCS, validates it using custom business-logic predicates, then re-uploads it; and a back-end service that authenticates via JWT/MySQL, authorizes which of 17 apps a user can view, and displays Grafana/Kibana metrics). He leads six engineers focusing on validation and some back-end code; the React front-end is handled by others.
     **Rating: 7/10**
   * **Pros:** Clear career progression, named tools (Quark, GCS, JWT, MySQL), described system components and responsibilities.
   * **Cons:** Explanation occasionally jumped around (authentication, authorization, JSON flows) rather than a strictly sequential data-flow narrative.

2. **Q: “What was the toughest validation you’ve implemented so far?”**
   **A:**

   * The JSON metadata had deeply nested parent/child structures (e.g. a “student” object inside a “department” inside another “student,” etc.). Some fields were nullable in inner nodes but not in outer nodes, and certain child fields (e.g. data-source ID) only became mandatory if the URL was “Grafana.”
   * Tried using standard validation annotations first (e.g. `@NotNull`, string length), but realized they couldn’t express interdependent rules (e.g. “if URL == Grafana then dataSourceId != null”). Switched to programmatic validation in Spring Boot using Java Predicates—validating each JSON subtree manually, then re-uploading only if JUnit coverage ≥ 80%.
     **Rating: 8/10**
   * **Pros:** Gave a concrete, complex scenario involving a JSON graph and conditional fields. Demonstrated why annotations alone didn’t suffice and how he used Predicates for business logic.
   * **Cons:** Could have mentioned JSON schema or Jackson’s tree model briefly, but overall very solid.

3. **Q: “Did you leverage `Optional` anywhere? Give a specific scenario.”**
   **A:**

   * When reading properties via `@Value("${some.key}")`, if the key didn’t exist, it would throw an NPE. Wrapped the property in an `Optional` (e.g. `Optional.ofNullable(environment.getProperty("xyz"))`) to avoid null pointers.
     **Rating: 6/10**
   * **Pros:** Shows awareness of NPE risk and knowing that `Optional` can guard property lookups.
   * **Cons:** A fairly basic example; didn’t mention alternatives like using `@ConfigurationProperties` or default values.

4. **Q: “Which development model are you following? How do you handle testing in a one-week sprint?”**
   **A:**

   * Use Agile with one-week sprints (was two weeks, but shortened for weekly stakeholder demos). Create user stories as either “dev only” or “test only.” After each week, they demo to management; production releases aren’t weekly, since it’s an internal product.
     **Rating: 6/10**
   * **Pros:** Explained why the sprint is one week and how they split dev/test work.
   * **Cons:** Didn’t discuss best practices for continuous integration or how they ensure quality under such a tight cadence.

5. **Q: “What is the primary role of Spring Boot’s auto-configuration?”**
   **A:**

   * `@SpringBootApplication` bundles `@EnableAutoConfiguration`, `@ComponentScan`, and `@Configuration`. Auto-configuration scans the base package (where `main` lives) and auto-wires common beans. If multiple auto-configured beans conflict, you can use `@Primary` or `@Qualifier` to pick one.
     **Rating: 7/10**
   * **Pros:** Correctly identified the annotations and how Spring decides which beans to load.
   * **Cons:** Could’ve mentioned `spring.factories` under the hood, but his answer was solid.

6. **Q: “How does Spring Boot Actuator enhance application management?”**
   **A:**

   * Add `spring-boot-starter-actuator` to `pom.xml`. Actuator endpoints (e.g. `/actuator/health`) report health status and request counts. In their CI/CD pipeline, they hit an Actuator health endpoint first—if unhealthy, fail the pipeline instead of fetching all 17 JSON files and doing expensive validation.
     **Rating: 7/10**
   * **Pros:** Practical use case (short-circuit validation if service is down) and knows basic actuator features.
   * **Cons:** Did not mention customizing endpoints or exposing metrics beyond “up/down,” but still good.

7. **Q: “What security measures should you implement when using Spring Boot Actuator in production?”**
   **A:**

   * “I’m not sure—haven’t worked in production yet.” Suggestion: use IP whitelisting or restrict sensitive endpoints to specific roles by passing the app name via front-end. All APIs are private.
     **Rating: 4/10**
   * **Pros:** Mentioned IP whitelisting and role-based restrictions in principle.
   * **Cons:** Lacked specifics (e.g. enabling HTTPS, securing with Spring Security roles or custom endpoint exposure, OAuth2 scopes, etc.). Overall fairly vague.

8. **Q: “How are properties managed in Spring Boot? Do you use `.properties` or `.yaml`?”**
   **A:**

   * They use `application.properties` only (not YAML). For different environments, they have `application-dev.properties`, etc., and activate a profile (e.g. `-Dspring.profiles.active=dev`) so that Spring picks the correct file.
     **Rating: 6/10**
   * **Pros:** Knows how profiles and environment-specific properties work.
   * **Cons:** Didn’t mention `@ConfigurationProperties` or how to structure nested properties, but acceptable.

9. **Q: “If you move from dev to prod, how do you overwrite datasource URLs without changing code?”**
   **A:**

   * They maintain separate files—`application.properties`, `application-staging.properties`, `application-dev.properties`. By activating the right profile, Spring loads the correct `spring.datasource.url` automatically. No code change needed.
     **Rating: 6/10**
   * **Pros:** Correct use of Spring profiles.
   * **Cons:** Very basic scenario, but it satisfies the question.

10. **Q: “Do you know about database migration in Spring Boot?”**
    **A:**

    * “Not really. I know Flyway exists, but in our app we rely on JPA (JPQL or `JpaRepository`) so we don’t write DB-specific SQL. We just change the datasource URL in properties if we need to point to a new DB.”
      **Rating: 5/10**
    * **Pros:** Aware of Flyway’s existence.
    * **Cons:** Didn’t demonstrate deeper knowledge of running migrations (Flyway vs. Liquibase, how to configure `spring.flyway.*` properties).

11. **Q: “Explain `@Transactional`. How does it work?”**
    **A:**

    * `@Transactional` demarcates a transaction with multiple steps. If any step (e.g. payment or saving user details) fails, the whole transaction rolls back so you don’t partially persist data.
      **Rating: 7/10**
    * **Pros:** Clear rollback example and why transactions are needed.
    * **Cons:** Did not mention propagation levels or isolation modes, but the core concept is correct.

12. **Q: “Can transaction management be done externally or must it be in-app?”**
    **A:**

    * They haven’t encountered external transaction managers. Acknowledged Spring Boot supports in-app declarative TX and can integrate JTA for distributed transactions.
      **Rating: 5/10**
    * **Pros:** Knows Spring can use JTA for external management.
    * **Cons:** Did not cite any real usage; answer was superficial.

13. **Q: “What validation annotations or libraries have you used most often?”**
    **A:**

    * They rely heavily on a global `@RestControllerAdvice` to catch validation exceptions. When a business-rule fails, they throw a custom `ValidationException` from the service, catch it via global handler, build an `ApiErrorResponse` (with field-level error code and message from `messages.properties`), and return JSON. They didn’t use annotation-based validators for deeply nested rules—used custom predicates instead.
      **Rating: 6/10**
    * **Pros:** Demonstrated use of `@RestControllerAdvice` and custom exception handling.
    * **Cons:** Didn’t specify common JSR-303 annotations (`@NotNull`, `@Size`, `@Pattern`) beyond “we tried them first but they didn’t suffice.”

14. **Q: “How does Spring Boot simplify deployment vs. a traditional Spring app?”**
    **A:**

    * Spring Boot uses an embedded Tomcat. You build a JAR (`mvn package`), set `server.port` in `application.properties` (default 8080), and run it (`java -jar app.jar`)—no external WAR/Tomcat deploy step needed.
      **Rating: 7/10**
    * **Pros:** Clearly explained embedded container and property override.
    * **Cons:** Could have mentioned executable JAR manifest, fat JAR layering, but still solid.

15. **Q: “Does Spring Boot support internationalization (i18n)?”**
    **A:**

    * “Yes, I know it does, but we’ve never used it so I’m not certain how it works.”
      **Rating: 3/10**
    * **Pros:** Recognized that i18n exists.
    * **Cons:** Couldn’t explain `MessageSource`, `LocaleResolver`, resource bundles, etc.

16. **Q: “How would you secure a REST API?”**
    **A:**

    * Primary answer: Use JWT tokens (authenticate username/password to generate token, TTL on tokens).
    * Mentioned a Facebook-style scenario: if a user isn’t in someone’s friend list, they can’t view that profile. They would check in MongoDB, cache friend list with a 30-second TTL, then return from cache if friend count hasn’t changed. (This example got a bit off track.)
    * Also said Spring Security (OAuth2/JWT) and MFA on front-end.
      **Rating: 5/10**
    * **Pros:** Knows JWT and Spring Security basics.
    * **Cons:** The caching/friends example was confusing; didn’t mention CSRF, CORS, role/authority mapping in Spring Security, or common best practices.

17. **Q: “Have you worked on microservice architecture? If so, how do you handle circuit-breaking?”**
    **A:**

    * They “leverage microservices” but haven’t built a fully distributed system. They have three separate deployments (front, validation, back). They don’t call each other’s REST APIs—once validation writes to GCS, that service is done.
    * For fault-tolerance, if the Grafana endpoint is down, they display a default company page with “please wait,” retry twice, then return a fallback.
      **Rating: 4/10**
    * **Pros:** Understand concept of fallback when a downstream service is unavailable.
    * **Cons:** No mention of Hystrix/Resilience4j, API Gateway (e.g. Spring Cloud Gateway), or a true circuit breaker pattern. Limited microservices experience.

18. **Q: “Which is better: monolithic or microservices?”**
    **A:**

    * No absolute answer. Monoliths are easier to manage, no separate databases, simpler. Microservices allow scaling individual components and reduce blast radius if one service needs maintenance—no need to notify everyone if just one service is down.
    * Advises against microservices unless the project is sufficiently large.
      **Rating: 7/10**
    * **Pros:** Balanced pros/cons, emphasized maintainability and scaling.
    * **Cons:** Could have touched on domain boundaries, data consistency, team structure, but overall solid.

19. **Q: “If a small client asks you to build a project from scratch, would you choose monolith or microservices?”**
    **A:**

    * Depends on requirements. For a small e-commerce (products, categories, simple cart, payment), choose monolith. For a huge enterprise shipping/tracking system with many teams and integrations, microservices would be appropriate.
      **Rating: 7/10**
    * **Pros:** Answered with concrete examples.
    * **Cons:** None major.

20. **Q: “Have you worked on reactive programming (e.g. Project Reactor, WebFlux) or event-driven systems?”**
    **A:**

    * No direct reactive experience. Knows about `@EventListener` and JPA lifecycle events (`@PreInsert`, `@PostUpdate`), but hasn’t built a fully non-blocking/reactive pipeline.
      **Rating: 4/10**
    * **Pros:** Understands JPA entity events.
    * **Cons:** Couldn’t speak to Reactor/Flux/Mono, back-pressure, or non-blocking I/O.

21. **Q: “Spring Boot offers a default in-memory cache; is it a good idea to use it or should you use an external cache like Redis?”**
    **A:**

    * Previously used Redis but faced issues when Redis nodes went down. The caching team advised not to cache critical data. Current app uses simple default caching (e.g. `@Cacheable` with default TTL \~ 5 min). They did not use Redis here because of past challenges, though Redis was used before.
      **Rating: 5/10**
    * **Pros:** Aware of trade-offs (external cache availability vs default).
    * **Cons:** Didn’t articulate specific limitations of the default cache (lack of distribution, eviction policies).

22. **Q: “What are the limitations of Spring Boot’s default cache?”**
    **A:**

    * “I’m not sure; I only know people move to external caches for reliability.”
      **Rating: 3/10**
    * **Pros:** Realized default cache isn’t distributed.
    * **Cons:** Couldn’t name TTL configuration, cache eviction, inability to share across nodes, etc.

23. **Q: “In a Spring Boot app you can use an embedded server or deploy to an external server. What are the pros and cons?”**
    **A:**

    * Embedded: by default pulls in Tomcat. You can exclude Tomcat and bundle whatever server you want (Jetty, Undertow). Pros: no separate WAR, simpler CI/CD. Cons: less fine-grained control over server configs (resource allocation, low-level tuning).
      **Rating: 6/10**
    * **Pros:** Clearly described how to switch out embedded container and main advantages.
    * **Cons:** Could have mentioned cold startup time, memory footprint, layering JAR vs. WAR, but adequate.

24. **Q: “Is there any role for Docker when deploying a Spring Boot application?”**
    **A:**

    * They build the JAR, then in CI/CD push to Kubernetes. They had issues testing on Docker Desktop vs. Kubernetes because they externalized JSON and `logback.xml`. Locally Docker Desktop worked w/o specifying file paths, but on K8s the externalized path had to be provided. Logging configuration also had to be externalized.
      **Rating: 6/10**
    * **Pros:** Demonstrated real-world Docker/K8s path issues and configuration externalization.
    * **Cons:** Didn’t discuss multi-stage Dockerfiles or best practices, but the example was relevant.

25. **Q: “When committing code you might encounter merge conflicts. How do you manage them?”**
    **A:**

    * Pull frequently from the main branch, keep your fork (feature branch) in sync. If someone merges code ahead of you, when you open your PR you’ll see conflicts. You `git pull`, resolve the conflicts locally (manually or via your IDE), then commit and push.
      **Rating: 5/10**
    * **Pros:** Knows the basic workflow (`git pull`, manual resolution, IDE tools).
    * **Cons:** Didn’t mention `git merge` vs. `git rebase`, conflict markers, or advanced strategies (e.g. `git rerere`).

26. **Q: “What is Git rebase and how do you use it?”**
    **A:**

    * In IntelliJ/Eclipse, right-click on a file/branch → Rebase. It updates your feature branch onto the latest `main` without extra merge commits. Exact command not recalled.
      **Rating: 4/10**
    * **Pros:** Understands rebase conceptually from the IDE.
    * **Cons:** Couldn’t quote `git rebase main` or talk about interactive rebase, conflict resolution during rebase, etc.

27. **Q: “How would you optimize a Maven build for a large project?”**
    **A:**

    * Unclear. Tried to tie it to Docker layering—using a base image with JDK 17, then copying the JAR. Ultimately said Maven’s sole job is to produce a JAR; optimization happens at container level. Did not provide any concrete Maven tips.
      **Rating: 2/10**
    * **Pros:** Recognized Docker builds run on an already packaged JAR.
    * **Cons:** Failed to mention `–T 2` for parallel builds, skipping tests during dev (`-DskipTests`), incremental `maven` plugin, use of local repository caching, or modular multi-module optimizations.

28. **Q: “Explain the Maven lifecycle and what `clean` does.”**
    **A:**

    * Thought `clean` checks for compilation issues (incorrect). Knew there are phases like `validate`, `compile`, `test`, `package`, `install`, `deploy`, but confused `clean` with compile checks.
      **Rating: 3/10**
    * **Pros:** Named some lifecycle phases.
    * **Cons:** Incorrect on `clean` (it deletes `target/`). Didn’t explain `validate → compile → test → package → verify → install → deploy`.

29. **Q: “Why do we need design patterns? Give an example.”**
    **A:**

    * Explained Post/Redirect/Get pattern to prevent duplicate form submissions. Gave a Spring MVC example: on a POST save, return `redirect:/someGet`, so on browser refresh it doesn’t re-POST.
      **Rating: 7/10**
    * **Pros:** Clear, correct example of a design pattern solving a common web problem.
    * **Cons:** Could have mentioned creational or structural patterns, but the PRG example was very strong.

30. **Q: “Have you used Singleton pattern before? How does Spring Boot handle singletons?”**
    **A:**

    * In Spring Boot, all beans are singletons by default (one instance per application context), so no need to implement your own `Singleton` class.
      **Rating: 7/10**
    * **Pros:** Correct and concise.
    * **Cons:** None.

31. **Q: “What is the Diamond problem in Java, and how do you address it?”**
    **A:**

    * Showed that if two interfaces both define a default method `drive()`, and a class implements both interfaces, Java will not know which to inherit. To fix it, you must either override `drive()` explicitly in the class or remove the `@Override` conflict (call `InterfaceA.super.drive()`).
      **Rating: 6/10**
    * **Pros:** Identified default‐method conflict and need to override.
    * **Cons:** Explanation slightly muddled; could have cited “`implements A, B { public void drive() { A.super.drive(); } }`” as the precise solution.

32. **Q: “How does Java handle memory leaks?”**
    **A:**

    * Java uses garbage collection (GC). In recent JDKs (Java 11+), ZGC (confused as “ZZC”) and Shenandoah reduce pause times, so they help mitigate memory leaks.
      **Rating: 5/10**
    * **Pros:** Knows that modern GCs (ZGC, Shenandoah) have low pause times.
    * **Cons:** Memory leaks occur when live references persist—should mention weak references, closing streams, removing listeners, finalization, etc. Slight confusion between GC pauses and leak prevention.

33. **Q: “What techniques (other than GC) do you use to identify and fix memory leaks?”**
    **A:**

    * Mentioned Java Flight Recorder, Eclipse Memory Analyzer (MAT), ensuring streams are closed in `finally`, removing unneeded object references.
      **Rating: 6/10**
    * **Pros:** Cited common tools (JFR, MAT) and good practice (closing streams).
    * **Cons:** Could have also mentioned heap dumps, profilers (VisualVM), JConsole, but acceptable.

34. **Q: “You suspect a memory leak in a long-running Java app—what steps do you take?”**
    **A:**

    * Use Dynatrace (or a similar APM) to spot which methods keep growing objects. Do performance testing to recreate high load, capture heap profile, pinpoint the class retaining references.
      **Rating: 6/10**
    * **Pros:** Good mention of APM (Dynatrace) and the need for load testing plus heap profiling.
    * **Cons:** Didn’t mention generating a heap dump manually, analyzing with MAT, but overall solid.

35. **Q: “How does `parallelStream()` improve performance, and when should you use it or not?”**
    **A:**

    * `parallelStream()` forks the data into multiple chunks (by default one chunk per core). For a large list (e.g., 400 employees), it splits into four parallel threads filtering concurrently—this speeds up stateless operations like `filter()` or `map()`. But if you need to sort the entire list, each thread only sorts its chunk; final results won’t be globally ordered. So avoid parallel for operations requiring a global ordering or dependent on side effects.
      **Rating: 7/10**
    * **Pros:** Correct explanation of parallelization, thread chunks, and why global operations (sorting) can break.
    * **Cons:** Could have mentioned overhead of thread forking or when data size is too small.

36. **Q: “Given a very large collection, how do you decide between parallel and sequential streams?”**
    **A:**

    * Depends on the nature of the operation and data size. For simple filters (e.g. employees by city), parallel can help. For grouping or computing max per department—since elements for the same key may appear in different chunks—parallel can require extra merge logic, making it less efficient. So choose based on whether the operation is “parallelizable” (stateless, embarrassingly parallel) and large enough to offset thread overhead.
      **Rating: 6/10**
    * **Pros:** Recognized that grouping/aggregation can complicate parallel streams.
    * **Cons:** Did not quantify (e.g. “if n > 10,000 and CPU cores > 1, use parallel”), but conceptually correct.

37. **Q: “Have you ever used the `synchronized` keyword?”**
    **A:**

    * Not in production. Knows that `synchronized` locks a method or block so that while one thread is inserting a record, no other thread can delete/save on that object until done.
      **Rating: 6/10**
    * **Pros:** Correct basic lock explanation.
    * **Cons:** Did not mention reentrancy, lock granularity, performance trade-offs, or alternatives like `ReentrantLock`.

38. **Q: “Explain serialization. Any challenges you’ve faced?”**
    **A:**

    * Serialization converts an object to a byte stream (e.g. to send over the network). You implement `Serializable`. They ran into a challenge when their controller only had raw JSON (as a `String`) and needed to deserialize into a DTO in the service layer before validation. Moved deserialization logic into a `@Configuration`-created `ObjectMapper` bean. Validated in the service instead of in the controller.
      **Rating: 6/10**
    * **Pros:** Correctly stated what serialization is and why you need it when sending over the wire. Identified a real challenge: deciding where to deserialize and how to hook into validation.
    * **Cons:** Could have also mentioned handling serialVersionUID, transient fields, or custom serializers, but good.

39. **Q: “If you build an app that loads plugins from third-party sources, how do you secure your system?”**
    **A:**

    * Never encountered this scenario. Suggested possibly writing a custom ClassLoader to restrict plugin loading and using Java’s SecurityManager to define strict policies.
      **Rating: 3/10**
    * **Pros:** Knew that a custom class loader and SecurityManager could help.
    * **Cons:** No concrete implementation details (sandboxing, code signing, verifying signatures, runtime permission checks), so answer was very superficial.

40. **Q: “Design an API to create a complex configuration object. Which design pattern helps?”**
    **A:**

    * In Spring Boot, use IoC: do not `new` objects. Prefer constructor injection over `@Autowired` (gives immutability, easier unit testing). You could also use the Builder pattern to assemble a complex object fluently, then pass it to your service.
      **Rating: 6/10**
    * **Pros:** Correctly advocated constructor injection and identified Builder as a suitable creational pattern.
    * **Cons:** Could have described a `Configuration` class with a nested static `Builder`, or shown how `@ConfigurationProperties` with a fluent API helps, but answer was acceptable.

41. **Coding Q1: “Given a `List<Integer>`, find all numbers starting with 1 using streams.”**
    **Candidate’s Code (verbal summary):**

    ```java
    List<Integer> numbers = List.of(2, 6, 11, 119, 12, 1);
    List<String> modified = numbers.stream()
        .map(n -> n.toString())
        .filter(s -> s.substring(0, 1).equals("1"))
        .distinct() // optional
        .collect(Collectors.toList());
    System.out.println(modified);
    ```

    * Printed the resulting `List<String>` of numbers whose string starts with “1.”
    * Initially forgot to print the filtered list, but fixed it.
      **Rating: 5/10**
    * **Pros:** Used `stream()`, `map()`, `filter()`, `collect()`. Checked `substring(0,1).equals("1")`.
    * **Cons:** Converting to `String` isn’t strictly necessary (could use `n >= 10 && (""+n).startsWith("1")`), but acceptable. Didn’t print as `List<Integer>`. Minor bug (forgot to print at first).

42. **Coding Q2: “Given a list, print the three maximum and three minimum numbers using streams.”**
    **Candidate’s Approach (verbal summary):**

    ```java
    // Three minimum
    List<Integer> threeMin = numbers.stream()
        .sorted()           // ascending
        .limit(3)
        .collect(Collectors.toList());

    // Three maximum
    List<Integer> threeMax = numbers.stream()
        .sorted((a, b) -> b - a)  // descending via lambda
        .limit(3)
        .collect(Collectors.toList());
    ```

    * Alternatively could do two separate streams or use `Collectors.collectingAndThen(...)` with `Comparator.reverseOrder()`.
      **Rating: 7/10**
    * **Pros:** Correct use of `sorted()`, `limit(3)`, and a custom comparator for descending order. Simple and readable.
    * **Cons:** Did two separate streams (fine), but didn’t mention `peek()` or combining in a single pass; still, straightforward.

43. **Q: “What message do you have for junior Java developers?”**
    **A:**

    * Don’t just copy/paste answers from Google or ChatGPT. First think through the problem yourself, dig into how it works, then use those tools as aids. Relying purely on copy/paste may solve the immediate issue but won’t build deep understanding, which pays off long-term.
      **Rating: 8/10**
    * **Pros:** Strong emphasis on understanding before using search/AI; good mentorship advice.
    * **Cons:** None.

---

**Summary of Ratings**

* The candidate’s strongest answers were the **“toughest validation” (8/10)** and the **“message to junior developers” (8/10)**.
* He was solid on Spring Boot fundamentals (auto-configuration, embedded server, Actuator) in the 6–7/10 range.
* He struggled on more advanced topics like **database migrations (5/10)**, **production-grade Actuator security (4/10)**, **Maven optimization (2/10)**, **Git rebase commands (4/10)**, and **plugin security (3/10)**.
* Overall, the average rating across all 43 questions is approximately **5.7/10**, reflecting a mid‐level candidate with strong Spring Boot/validation experience but gaps in some DevOps, advanced Maven, and deep Spring Security/reactive topics.
