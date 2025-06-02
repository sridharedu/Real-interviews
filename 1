1. **Question:** “Let’s start our discussion with Java 8 features. Please explain Java 8 features in detail.”
   **Candidate’s Answer (Brief):**
   Mentioned Lambda expressions, functional interfaces, Optional class, method references, Stream API, and new Date/Time API in `java.time`.
   **Correct Answer:**
   Java 8 introduced:

   * **Lambda expressions** (e.g., `(args) -> expression`) to enable functional programming.
   * **Functional interfaces** (interfaces with a single abstract method) and the `@FunctionalInterface` annotation.
   * **Method references** (e.g., `ClassName::methodName`) as shorthand for lambdas.
   * **Stream API** (`java.util.stream`) for processing collections in a functional style with operations like `filter()`, `map()`, `reduce()`.
   * **Optional** (`java.util.Optional`) to avoid `NullPointerException` by representing optional values.
   * **Default and static methods** in interfaces to add new functionality without breaking existing implementations.
   * **New Date/Time API** (`java.time` package) replacing the legacy `java.util.Date`/`Calendar` with immutable, thread-safe classes (`LocalDate`, `LocalDateTime`, etc.).
   * **Nashorn JavaScript engine**, **Repeatable annotations**, and **Type annotations** (JSR 308).
     **Rating:** 3/5
     *Justification:* The candidate named most major features but did not mention default/static methods in interfaces explicitly or the Nashorn engine, and gave only a high-level list without clarifying how they work or why they matter.

2. **Question:** “So what were changes in case of interfaces?”
   **Candidate’s Answer (Brief):**
   Stated that a functional interface can declare only one abstract method and multiple static or default methods.
   **Correct Answer:**
   In Java 8, interfaces can have:

   * **Default methods** (with a method body, declared with the `default` keyword), allowing interface evolution without breaking existing implementations.
   * **Static methods** (with a method body, declared with the `static` keyword), callable on the interface itself.
   * **Private methods** (added in Java 9) are not relevant to Java 8.
   * **Functional interfaces**: interfaces annotated with `@FunctionalInterface` must have exactly one abstract method (but can have any number of default/static methods).
     Pre-Java 8 interfaces allowed only abstract methods (implicitly `public abstract`) and `public static final` constants.
     **Rating:** 3/5
     *Justification:* The candidate correctly identified default and static methods in functional interfaces but conflated “changes in interfaces” with only the functional interface restriction; they did not explicitly mention that regular interfaces also gained default/static methods (even if not marked functional).

3. **Question:** “What is the difference between an interface and a functional interface?”
   **Candidate’s Answer (Brief):**
   Said that a normal interface can have multiple abstract methods and static variables; a functional interface (annotated `@FunctionalInterface`) can have only one abstract method.
   **Correct Answer:**

   * A **normal interface** may declare any number of abstract methods, and may contain `public static final` constants, default methods, and static methods.
   * A **functional interface** is an interface with exactly one abstract method (the “functional method”), optionally annotated with `@FunctionalInterface`. It can also have any number of default or static methods. The annotation is not strictly required but enforces the single-abstract-method rule. This allows it to be used as the target of a lambda expression or method reference.
     **Rating:** 4/5
     *Justification:* The candidate’s distinction was essentially correct, though they referred to “static variables” rather than stating that normal interfaces can have multiple abstract methods and default/static methods. They understood the single-abstract-method requirement.

4. **Question:** “What were changes in case of HashMap internal function in Java? In HashMap, what changed in Java 8?”
   **Candidate’s Answer (Brief):**
   Described that HashMap still uses buckets and linked lists for collision handling; mentioned that iteration with `forEach(key, value)` is easier. Spoke vaguely about default capacity (16) and nodes with key, hash, next.
   **Correct Answer:**
   In Java 8, `HashMap`’s collision handling changed:

   * When a bucket’s linked list length exceeds a threshold (TREEIFY\_THRESHOLD = 8), the chain is replaced by a balanced **red-black tree** (`TreeNode`), improving worst-case lookup from O(n) to O(log n).
   * Methods like `forEach`, `computeIfAbsent`, `merge`, `remove(key, value)` were added for functional and atomic operations.
   * The default initial capacity and load factor remained 16 and 0.75, but the bucket structure is now hybrid (`LinkedList` → `TreeNode`).
   * The resize threshold logic and index calculation remained largely the same (`(n – 1) & hash`).
     **Rating:** 2/5
     *Justification:* The candidate recognized bucket/linked-list structure and iterating with `forEach`, but failed to mention the critical treeification of buckets or new methods like `computeIfAbsent`. Their answer omitted the main Java 8 optimization.

5. **Question:** “Can you explain how ConcurrentHashMap works?”
   **Candidate’s Answer (Brief):**
   Said that in multithreading, HashMap causes concurrent modification exceptions; ConcurrentHashMap uses segmented/minor segment locking so multiple threads can operate in parallel.
   **Correct Answer:**
   In Java 8, `ConcurrentHashMap` is reimplemented without fixed segments:

   * It uses internal **bin-level (node) synchronization** (via `synchronized` or CAS) on individual buckets (or tree nodes), allowing high concurrency with minimal contention.
   * **Read operations** are non-blocking (lock-free) using `volatile` reads.
   * **Write operations** (insertion, deletion) lock only the bin (bucket) they affect, not the entire map; when a bucket becomes too large, it can be transformed into a tree to reduce contention.
   * The map is divided into **Node\<K,V>** bins; resizing is done cooperatively by multiple threads.
   * Supports atomic retrieval/update methods like `computeIfAbsent`, `putIfAbsent`.
     **Rating:** 3/5
     *Justification:* The candidate understood that ConcurrentHashMap avoids global locking and allows parallel access, but did not describe bin-level locking, non-blocking reads, or cooperative resizing. Their explanation was high-level and lacked detail.

6. **Question:** “There is a HashMap, a synchronized map, and a ConcurrentHashMap. What are the differences between them?”
   **Candidate’s Answer (Brief):**
   Explained that a synchronized map (via `Collections.synchronizedMap`) is like a Hashtable and locks the entire map on each operation, causing poor performance; ConcurrentHashMap uses segment-based locks so only portions are locked, allowing parallelism.
   **Correct Answer:**

   * **HashMap:** Not thread-safe. Concurrent modifications by multiple threads can cause data inconsistency or `ConcurrentModificationException` during iteration.
   * **SynchronizedMap (via `Collections.synchronizedMap`) or Hashtable:** Wraps the map so all operations are synchronized on a single lock. Only one thread can perform any operation (read or write) at a time.
   * **ConcurrentHashMap:** Thread-safe without synchronizing the entire map. It uses finer-grained locking (bin-level locks in Java 8) or partition-level locking in earlier versions, allowing multiple threads to read and write different parts concurrently. Read operations are mostly lock-free.
     **Rating:** 4/5
     *Justification:* The candidate correctly contrasted global locking vs. segmented locking. They called `synchronizedMap` a Hashtable, which is slightly incorrect (Hashtable is separate, though conceptually similar). But overall, they captured the key performance differences.

7. **Question:** “How do Hashtable and HashMap differ from each other?”
   **Candidate’s Answer (Brief):**
   Said that Hashtable does not allow null keys/values; HashMap allows one null key. Both use similar hashing/collision logic, but Hashtable is synchronized and HashMap is not.
   **Correct Answer:**

   * **Null handling:** `HashMap` allows one null key and multiple null values; `Hashtable` does not allow any null key or null value (throws `NullPointerException`).
   * **Synchronization:** `Hashtable` is inherently synchronized (thread-safe by default). `HashMap` is not thread-safe.
   * **Legacy status:** `Hashtable` is legacy and was retrofitted to implement `Map`; `HashMap` is newer (post-Java 1.2) and generally preferred.
   * **Iteration performance:** `HashMap`’s iterators are fail-fast, while `Hashtable`’s enumerations are not fail-fast.
   * **Subclass:** `HashMap` has `LinkedHashMap` subclass for insertion-order iteration; `Hashtable` does not.
     **Rating:** 4/5
     *Justification:* The candidate correctly noted null-handling and synchronization differences, though they did not mention iterator behavior or legacy status. They covered the two main distinctions adequately.

8. **Question:** “Hashtable is deprecated. Why was it deprecated, and what replaced it?”
   **Candidate’s Answer (Brief):**
   Explained that Hashtable is a legacy class from pre-generics era (before Java 1.5), and that `ConcurrentHashMap` is now the better choice.
   **Correct Answer:**

   * **Reason for deprecation (legacy):** `Hashtable` predates Java 2 collections and does not support generics (everything is `Object`). Its methods are synchronized on the entire map, causing contention.
   * **Replacement:** In most single-threaded contexts, use `HashMap`; in multi-threaded contexts, use `ConcurrentHashMap` (Java 5+). In rare legacy code, `Hashtable` is still supported but discouraged.
     **Rating:** 4/5
     *Justification:* The candidate correctly identified the generics issue and pointed to `ConcurrentHashMap`. They didn’t explicitly mention that `HashMap` replaces it in single-threaded code, but overall the essential reasoning was present.

9. **Question:** “There is a Set interface and classes like HashSet, LinkedHashSet, TreeSet. On what basis should I use each of them?”
   **Candidate’s Answer (Brief):**
   Misinterpreted the question as about `LinkedHashMap` instead of `LinkedHashSet`. They said: for full CRUD operations on a map, use `LinkedHashMap` (faster than `HashMap` and `TreeSet`)? They mixed up Set and Map.
   **Correct Answer:**

   * **HashSet:** Backed by a `HashMap`; does not guarantee any ordering; offers O(1) average time for basic operations (`add`, `remove`, `contains`). Use when you don’t need ordering.
   * **LinkedHashSet:** Backed by a `LinkedHashMap`; maintains **insertion order**. Slightly slower than `HashSet` due to linked list overhead. Use when you need to iterate in insertion order.
   * **TreeSet:** Backed by a `TreeMap`; maintains **sorted order** (natural ordering or via a provided `Comparator`). Operations cost O(log n). Use when you need sorted order.
     **Rating:** 1/5
     *Justification:* The candidate completely misunderstood and talked about `LinkedHashMap` rather than any `Set` implementation. They provided no correct information about `HashSet`, `LinkedHashSet`, or `TreeSet`.

10. **Question:** “I want to know the ordering and differences of them so that I can know in which condition I should use which one.” (Follow-up on Set vs. Set implementations)
    **Candidate’s Answer (Brief):**
    Said: use `HashSet` for read operations, `TreeSet` for sorted data, and “LinkedHashMap” for insert/update/delete operations, claiming it’s faster than `HashSet` and “TreeSet.”
    **Correct Answer:**

    * **HashSet:** No ordering guarantee; best for constant-time operations when order does not matter.
    * **LinkedHashSet:** Maintains insertion order; good when iteration order must match insertion.
    * **TreeSet:** Maintains sorted order; good when you need a naturally ordered set or custom ordering.
      `LinkedHashMap` is unrelated to `Set`; do not use it as a Set implementation.
      **Rating:** 1/5
      *Justification:* Again, the candidate confused `Set` implementations with Map implementations. They did not correctly address insertion vs. sorted ordering.

11. **Question:** “What is `java.util.Stream` (streams)?”
    **Candidate’s Answer (Brief):**
    Described a Stream as a way to process collections functionally; mentioned terminal vs. non-terminal (intermediate) operations (e.g., `filter`, `map`, `distinct`) and that Streams work on collections (`ArrayList`, `LinkedList`, `Map`, `TreeMap`, `HashMap`) to achieve faster results.
    **Correct Answer:**

    * A **Stream** is not a data structure but a sequence of elements supporting **functional operations**. Introduced in Java 8 under `java.util.stream`.
    * **Intermediate operations** (e.g., `filter()`, `map()`, `flatMap()`, `distinct()`) return another Stream and are lazy.
    * **Terminal operations** (e.g., `collect()`, `forEach()`, `reduce()`) produce a result or side effect and trigger execution.
    * Streams can be created from collections via `collection.stream()` or `collection.parallelStream()`, or from arrays, I/O channels, generator functions, etc.
    * Streams enable declarative data processing, possibly with internal iteration, and can be parallelized for multi-core performance.
      **Rating:** 3/5
      *Justification:* The candidate captured the essence—intermediate vs. terminal operations on collection-based streams—but did not clarify that streams are not the collections themselves and omitted how Streams can be built or combined. Their explanation was functional but lacked precision.

12. **Question:** “What is the difference between a normal stream and a parallel stream?”
    **Candidate’s Answer (Brief):**
    Said a parallel stream can perform operations “in parallel,” but they do not have much idea about how it works; they mostly use normal streams.
    **Correct Answer:**

    * **Normal (sequential) Stream:** Processes elements **in order** on a single thread. All intermediate and terminal operations execute on the calling thread.
    * **Parallel Stream:** The stream is divided into multiple **substreams**, which are processed concurrently on multiple threads from the common Fork/Join pool. Merges results after processing. Good for CPU-bound operations on large datasets but can introduce overhead or require thread-safe operations.
      Example:

    ```java
    List<Integer> list = Arrays.asList(1, 2, 3, 4);
    list.stream()             // sequential processing
        .filter(x -> x % 2 == 0)
        .forEach(System.out::println);
    list.parallelStream()     // parallel processing
        .filter(x -> x % 2 == 0)
        .forEach(System.out::println);
    ```

    **Rating:** 2/5
    *Justification:* The candidate knew that parallel means “parallel,” but they offered no detail on Fork/Join, threading, or when to use it. Their answer was superficial.

13. **Question:** “What is the difference between the two operations `filter` and `map` in streams?”
    **Candidate’s Answer (Brief):**
    Attempted to explain `map` as a way to “concatenate or change elements,” gave an example converting an array to a list, then to a stream, and using `filter` to find elements starting with a digit “1.” They conflated `map` and `filter`.
    **Correct Answer:**

    * **`filter(Predicate<T> predicate)`:** Intermediate operation that **selects** elements matching a condition. Returns a Stream of the subset. E.g., `.filter(x -> x % 2 == 0)` retains only even numbers.
    * **`map(Function<T,R> mapper)`:** Intermediate operation that **transforms** each element. Returns a Stream of the mapped values. E.g., `.map(x -> x * x)` converts each number to its square.
      Example:

    ```java
    List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
    names.stream()
         .filter(name -> name.startsWith("A"))   // retains "Alice"
         .map(String::toUpperCase)                // converts "Alice" to "ALICE"
         .forEach(System.out::println);
    ```

    **Rating:** 2/5
    *Justification:* The candidate did not clearly distinguish `filter` from `map` and gave an unclear example. They showed a partial understanding of `filter` but mischaracterized `map`.

14. **Question:** “Could you let me know how many types of predefined functional interfaces in Java are used day-to-day? Specifically interfaces like `Function`, `Supplier`, `Consumer`, `Predicate`. I want to know the difference between them, which methods they have, and in which condition we should use each.”
    **Candidate’s Answer (Brief):**
    Mentioned `Function` and its `apply` method; said they have little knowledge about `Consumer`; did not mention `Supplier` or `Predicate`.
    **Correct Answer:**
    Common Java 8 functional interfaces (in `java.util.function`):

    * **`Predicate<T>`** – takes a `T`, returns `boolean`. Method: `boolean test(T t)`. Use for boolean-valued conditions (e.g., filtering).
    * **`Function<T,R>`** – takes a `T`, returns an `R`. Method: `R apply(T t)`. Use for transforming or mapping values.
    * **`Consumer<T>`** – takes a `T`, returns nothing. Method: `void accept(T t)`. Use for side-effect operations (e.g., printing, saving).
    * **`Supplier<T>`** – takes no arguments, returns a `T`. Method: `T get()`. Use for lazy value generation or factories.
    * **`UnaryOperator<T>`** – extends `Function<T,T>`; takes a `T`, returns a `T`. Method: `T apply(T t)`. Use when input and output are same type.
    * **`BinaryOperator<T>`** – extends `BiFunction<T,T,T>`; takes two `T`s, returns a `T`. Method: `T apply(T t1, T t2)`. Use for reducing or combining.
    * **`BiFunction<T,U,R>`** – takes `T` and `U`, returns `R`. Use for two-argument transformations.
    * **`BiConsumer<T,U>`** – takes `T` and `U`, returns nothing. Use for side effects with two inputs.
    * **`BiPredicate<T,U>`** – takes `T` and `U`, returns a boolean. Use for two-argument boolean conditions.
      Usage examples:

    ```java
    Predicate<String> isEmpty = String::isEmpty;
    Function<String, Integer> toLength = String::length;
    Consumer<String> printer = System.out::println;
    Supplier<Date> dateSupplier = Date::new;
    ```

    **Rating:** 2/5
    *Justification:* The candidate only mentioned `Function` and vaguely `Consumer`, did not address `Predicate` or `Supplier`, and gave no usage scenarios. Their answer was incomplete.

---

**Overall Assessment:**

* The candidate demonstrated a basic awareness of Java 8 features and collections concepts but often provided superficial or partially incorrect answers.
* Areas of strong knowledge: distinguishing HashMap vs. Hashtable, synchronization differences, basic lambda/stream ideas.
* Areas needing improvement: correct understanding of Set implementations, in-depth knowledge of ConcurrentHashMap internals, precise Stream operation semantics, and familiarity with the full suite of functional interfaces.
* **Average Score Across All Questions:** 2.3/5.
