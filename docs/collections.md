# Collections

### Introduction to Collections

???+ info "What is the Java Collections Framework?"
    - The Java Collections Framework (JCF) is a set of classes and interfaces that implement commonly reusable collection data structures.
    - It provides a unified architecture for storing, retrieving, and manipulating data.
    - Key benefits:
        - Reduces programming effort by providing ready-to-use data structures.
        - Improves performance with efficient algorithms.
        - Increases code reusability and maintainability.

    === "Key Interfaces"
    - **Collection**: The root interface for most collections.
    - **List**: Ordered collection that allows duplicate elements (e.g., `ArrayList`, `LinkedList`).
    - **Set**: Collection that does not allow duplicate elements (e.g., `HashSet`, `TreeSet`).
    - **Queue**: Collection designed for holding elements prior to processing (e.g., `PriorityQueue`).
    - **Map**: Collection of key-value pairs (e.g., `HashMap`, `TreeMap`).

### List Interface

???+ info "List Interface"
    - A `List` is an ordered collection that allows duplicate elements.
    - Common implementations:
        - **`ArrayList`**: Resizable array implementation.
        - **`LinkedList`**: Doubly-linked list implementation.
        - **`Vector`**: Synchronized resizable array (legacy class).

    === "Example: Using `ArrayList`"
        ```java
        import java.util.ArrayList;

        public class Main {
            public static void main(String[] args) {
                ArrayList<String> list = new ArrayList<>();
                list.add("Apple");
                list.add("Banana");
                list.add("Cherry");

                System.out.println("List: " + list); // Outputs: [Apple, Banana, Cherry]

                list.remove("Banana");
                System.out.println("After removal: " + list); // Outputs: [Apple, Cherry]

                System.out.println("Element at index 1: " + list.get(1)); // Outputs: Cherry
            }
        }
        ```

### Set Interface

???+ info "Set Interface"
    - A `Set` is a collection that does not allow duplicate elements.
    - Common implementations:
        - **`HashSet`**: Unordered set backed by a hash table.
        - **`TreeSet`**: Ordered set backed by a red-black tree.
        - **`LinkedHashSet`**: Maintains insertion order.

    === "Example: Using `HashSet`"
        ```java
        import java.util.HashSet;

        public class Main {
            public static void main(String[] args) {
                HashSet<String> set = new HashSet<>();
                set.add("Apple");
                set.add("Banana");
                set.add("Apple"); // Duplicate, will not be added

                System.out.println("Set: " + set); // Outputs: [Apple, Banana]
            }
        }
        ```

### Map Interface

???+ info "Map Interface"
    - A `Map` is a collection of key-value pairs.
    - Common implementations:
        - **`HashMap`**: Unordered map backed by a hash table.
        - **`TreeMap`**: Ordered map backed by a red-black tree.
        - **`LinkedHashMap`**: Maintains insertion order.

    === "Example: Using `HashMap`"
        ```java
        import java.util.HashMap;

        public class Main {
            public static void main(String[] args) {
                HashMap<String, Integer> map = new HashMap<>();
                map.put("Apple", 1);
                map.put("Banana", 2);
                map.put("Cherry", 3);

                System.out.println("Map: " + map); // Outputs: {Apple=1, Banana=2, Cherry=3}

                map.remove("Banana");
                System.out.println("After removal: " + map); // Outputs: {Apple=1, Cherry=3}

                System.out.println("Value for 'Apple': " + map.get("Apple")); // Outputs: 1
            }
        }
        ```

### Queue Interface

???+ info "Queue Interface"
    - A `Queue` is a collection designed for holding elements prior to processing.
    - Common implementations:
        - **`PriorityQueue`**: A priority-based queue.
        - **`LinkedList`**: Can also be used as a queue.

    === "Example: Using `PriorityQueue`"
        ```java
        import java.util.PriorityQueue;

        public class Main {
            public static void main(String[] args) {
                PriorityQueue<Integer> queue = new PriorityQueue<>();
                queue.add(10);
                queue.add(5);
                queue.add(20);

                System.out.println("Queue: " + queue); // Outputs: [5, 10, 20]

                System.out.println("Polled element: " + queue.poll()); // Outputs: 5
                System.out.println("Queue after poll: " + queue); // Outputs: [10, 20]
            }
        }
        ```

### Iterator

???+ info "Iterator"
    - An `Iterator` is used to traverse elements in a collection.
    - Methods:
        - `hasNext()`: Returns `true` if there are more elements.
        - `next()`: Returns the next element.
        - `remove()`: Removes the last element returned by the iterator.

    === "Example: Using `Iterator`"
        ```java
        import java.util.ArrayList;
        import java.util.Iterator;

        public class Main {
            public static void main(String[] args) {
                ArrayList<String> list = new ArrayList<>();
                list.add("Apple");
                list.add("Banana");
                list.add("Cherry");

                Iterator<String> iterator = list.iterator();
                while (iterator.hasNext()) {
                    String element = iterator.next();
                    System.out.println(element);
                }
            }
        }
        ```

### Comparable and Comparator

???+ info "Comparable and Comparator"
    - Used for sorting collections.

    === "Using `Comparable`"
        - The `Comparable` interface is used to define the natural ordering of objects.
        - It requires implementing the `compareTo()` method.

        ```java
        import java.util.ArrayList;
        import java.util.Collections;

        class Student implements Comparable<Student> {
            String name;
            int age;

            public Student(String name, int age) {
                this.name = name;
                this.age = age;
            }

            @Override
            public int compareTo(Student other) {
                return this.age - other.age; // Sort by age
            }

            @Override
            public String toString() {
                return name + " (" + age + ")";
            }
        }

        public class Main {
            public static void main(String[] args) {
                ArrayList<Student> students = new ArrayList<>();
                students.add(new Student("Alice", 22));
                students.add(new Student("Bob", 20));
                students.add(new Student("Charlie", 25));

                Collections.sort(students);
                System.out.println(students); // Outputs: [Bob (20), Alice (22), Charlie (25)]
            }
        }
        ```

    === "Using `Comparator`"
        - The `Comparator` interface is used to define custom sorting logic.
        - It requires implementing the `compare()` method.

        ```java
        import java.util.ArrayList;
        import java.util.Collections;
        import java.util.Comparator;

        class Student {
            String name;
            int age;

            public Student(String name, int age) {
                this.name = name;
                this.age = age;
            }

            @Override
            public String toString() {
                return name + " (" + age + ")";
            }
        }

        public class Main {
            public static void main(String[] args) {
                ArrayList<Student> students = new ArrayList<>();
                students.add(new Student("Alice", 22));
                students.add(new Student("Bob", 20));
                students.add(new Student("Charlie", 25));

                // Sort by name
                Collections.sort(students, new Comparator<Student>() {
                    @Override
                    public int compare(Student s1, Student s2) {
                        return s1.name.compareTo(s2.name);
                    }
                });

                System.out.println(students); // Outputs: [Alice (22), Bob (20), Charlie (25)]
            }
        }
        ```

### Stream API

???+ info "What is the Stream API?"
    - The Stream API, introduced in Java 8, provides a functional programming approach to process collections of data.
    - It allows operations like filtering, mapping, and reducing data in a declarative way.
    - Streams do not store data; they operate on the source data and produce a result.

    === "Key Features"
    - **Lazy Evaluation**: Intermediate operations are not executed until a terminal operation is invoked.
    - **Parallel Processing**: Streams can be processed in parallel to improve performance.
    - **Immutability**: Streams do not modify the original data source.
    - **Non-Reusability**: Streams cannot be reused after a terminal operation. Attempting to reuse a stream will throw an `IllegalStateException`.

    === "Example: Non-Reusability of Streams"
        ```java
        import java.util.Arrays;
        import java.util.List;

        public class Main {
            public static void main(String[] args) {
                List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

                var stream = names.stream();
                stream.forEach(System.out::println); // Terminal operation

                // Attempting to reuse the stream will throw an exception
                stream.forEach(System.out::println); // Throws IllegalStateException
            }
        }
        ```

    === "Common Stream Operations"
    - **Intermediate Operations**: Transform the stream (e.g., `filter()`, `map()`, `sorted()`).
    - **Terminal Operations**: Produce a result or side effect (e.g., `forEach()`, `collect()`, `reduce()`).

    === "Example: Using Stream API"
        ```java
        import java.util.Arrays;
        import java.util.List;
        import java.util.stream.Collectors;

        public class Main {
            public static void main(String[] args) {
                List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

                // Filter names starting with 'A' and collect them into a new list
                List<String> filteredNames = names.stream()
                                                  .filter(name -> name.startsWith("A"))
                                                  .collect(Collectors.toList());

                System.out.println("Filtered Names: " + filteredNames); // Outputs: [Alice]

                // Convert names to uppercase and print them
                names.stream()
                     .map(String::toUpperCase)
                     .forEach(System.out::println);
            }
        }
        ```

### Common Stream Functions

???+ info "Common Stream Functions"
    - The Stream API provides a variety of functions to process collections efficiently.

    === "Intermediate Operations"
    - **`filter(Predicate)`**: Filters elements based on a condition.
        ```java
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> evenNumbers = numbers.stream()
                                           .filter(n -> n % 2 == 0)
                                           .collect(Collectors.toList());
        System.out.println(evenNumbers); // Outputs: [2, 4]
        ```
    - **`map(Function)`**: Transforms each element in the stream.
        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        List<Integer> nameLengths = names.stream()
                                         .map(String::length)
                                         .collect(Collectors.toList());
        System.out.println(nameLengths); // Outputs: [5, 3, 7]
        ```
    - **`sorted()`**: Sorts elements in natural order.
        ```java
        List<Integer> numbers = Arrays.asList(5, 3, 1, 4, 2);
        List<Integer> sortedNumbers = numbers.stream()
                                             .sorted()
                                             .collect(Collectors.toList());
        System.out.println(sortedNumbers); // Outputs: [1, 2, 3, 4, 5]
        ```
    - **`distinct()`**: Removes duplicate elements.
        ```java
        List<Integer> numbers = Arrays.asList(1, 2, 2, 3, 3, 3);
        List<Integer> uniqueNumbers = numbers.stream()
                                             .distinct()
                                             .collect(Collectors.toList());
        System.out.println(uniqueNumbers); // Outputs: [1, 2, 3]
        ```

    === "Terminal Operations"
    - **`forEach(Consumer)`**: Performs an action for each element.
        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        names.stream().forEach(System.out::println);
        ```
    - **`collect(Collector)`**: Collects elements into a collection.
        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        Set<String> nameSet = names.stream()
                                   .collect(Collectors.toSet());
        System.out.println(nameSet); // Outputs: [Alice, Bob, Charlie]
        ```
    - **`reduce(BinaryOperator)`**: Reduces elements to a single value.
        ```java
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        int sum = numbers.stream()
                         .reduce(0, Integer::sum);
        System.out.println(sum); // Outputs: 15
        ```
    - **`count()`**: Counts the number of elements in the stream.
        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        long count = names.stream().count();
        System.out.println(count); // Outputs: 3
        ```

### Parallel Streams

???+ info "Parallel Streams"
    - Parallel streams divide the data into multiple chunks and process them concurrently using multiple threads.
    - Use `parallelStream()` or `stream().parallel()` to create a parallel stream.

    === "Example: Using Parallel Streams"
        ```java
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        numbers.parallelStream()
               .forEach(n -> System.out.println(Thread.currentThread().getName() + " - " + n));
        ```

    === "Caution: Avoid Using `sorted()` with Parallel Streams"
    - The `sorted()` operation is stateful and requires maintaining order, which can lead to unpredictable results or degraded performance when used with parallel streams.
    - Always use sequential streams when sorting is required.

    ```java
    List<Integer> numbers = Arrays.asList(5, 3, 1, 4, 2);

    // Sequential stream with sorted
    List<Integer> sortedNumbers = numbers.stream()
                                         .sorted()
                                         .collect(Collectors.toList());
    System.out.println(sortedNumbers); // Outputs: [1, 2, 3, 4, 5]

    // Avoid using sorted with parallel streams
    List<Integer> parallelSortedNumbers = numbers.parallelStream()
                                                 .sorted()
                                                 .collect(Collectors.toList());
    System.out.println(parallelSortedNumbers); // May produce unpredictable results
    ```

### `forEach` Method

???+ info "What is the `forEach` Method?"
    - The `forEach` method is a terminal operation in the Stream API.
    - It is used to iterate over each element in a stream and perform an action.

    === "Syntax"
        ```java
        stream.forEach(action);
        ```

    === "Example: Using `forEach`"
        ```java
        import java.util.Arrays;
        import java.util.List;

        public class Main {
            public static void main(String[] args) {
                List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

                // Print each name using forEach
                names.stream()
                     .forEach(name -> System.out.println("Name: " + name));
            }
        }
        ```

    === "Using `forEach` with Method References"
        - Method references provide a shorthand for lambda expressions.

        ```java
        import java.util.Arrays;
        import java.util.List;

        public class Main {
            public static void main(String[] args) {
                List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

                // Print each name using method reference
                names.stream()
                     .forEach(System.out::println);
            }
        }
        ```

    === "Key Points"
    - `forEach` is a terminal operation and cannot be reused after execution.
    - It is primarily used for side effects, such as printing or logging.
    - Avoid modifying the data source within `forEach` to prevent unexpected behavior.
