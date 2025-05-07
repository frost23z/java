### Stream API

???+ info "Stream API Overview"
    - Introduced in Java 8, the Stream API provides a functional programming approach to process collections of data declaratively.
    - **Key Features**:
        - **Lazy Evaluation**: Operations are executed only when a terminal operation is invoked.
        - **Parallel Processing**: Streams can process data concurrently.
        - **Immutability**: Streams do not modify the source data.
        - **Non-Reusability**: Streams cannot be reused after a terminal operation.

    === "Example: Non-Reusability"

        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        var stream = names.stream();
        stream.forEach(System.out::println); // Terminal operation
        stream.forEach(System.out::println); // Throws IllegalStateException
        ```

    === "Common Operations"
        - **Intermediate**: `filter()`, `map()`, `sorted()`. They return a new stream and are lazy.
        - **Terminal**: `forEach()`, `collect()`, `reduce()`. Produce a result or side effect and consume the stream.

        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        List<String> filtered = names.stream()
                                     .filter(name -> name.startsWith("A"))
                                     .collect(Collectors.toList());
        System.out.println(filtered); // Outputs: [Alice]
        ```

### Common Stream Functions

???+ info "Stream Functions"
    - **Intermediate Operations**:
        - `filter(Predicate)`: Filters elements.

            ```java
            List<Integer> even = numbers.stream()
                                        .filter(n -> n % 2 == 0)
                                        .collect(Collectors.toList());
            ```
        - `map(Function)`: Transforms elements.

            ```java
            List<Integer> lengths = names.stream()
                                         .map(String::length)
                                         .collect(Collectors.toList());
            ```
        - `sorted()`: Sorts elements.

            ```java
            List<Integer> sorted = numbers.stream()
                                          .sorted()
                                          .collect(Collectors.toList());
            ```
        - `distinct()`: Removes duplicates.

            ```java
            List<Integer> unique = numbers.stream()
                                          .distinct()
                                          .collect(Collectors.toList());
            ```

    - **Terminal Operations**:
        - `forEach(Consumer)`: Performs an action for each element.

            ```java
            names.stream().forEach(System.out::println);
            ```
        - `collect(Collector)`: Collects elements into a collection.

            ```java
            Set<String> nameSet = names.stream()
                                       .collect(Collectors.toSet());
            ```
        - `reduce(BinaryOperator)`: Reduces elements to a single value.

            ```java
            int sum = numbers.stream().reduce(0, Integer::sum);
            ```
        - `count()`: Counts elements.

            ```java
            long count = names.stream().count();
            ```

### Parallel Streams

???+ info "Parallel Streams"
    - Parallel streams divide data into chunks for concurrent processing.
    - Use `parallelStream()` or `stream().parallel()`.

    === "Example"

        ```java
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        numbers.parallelStream()
               .forEach(n -> System.out.println(Thread.currentThread().getName() + " - " + n));
        ```

    === "Caution"
        - Avoid `sorted()` with parallel streams due to unpredictable results.

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

???+ info "`forEach` Method"
    - A terminal operation used for side effects like printing or logging.
    - Avoid modifying the data source within `forEach`.

    === "Example"

        ```java
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using Lambda Expression
        names.stream().forEach(name -> System.out.println("Name: " + name));

        // Using Method Reference
        names.stream().forEach(System.out::println);
        ```