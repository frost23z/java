# Optional Class

???+ info "What is the `Optional` Class?"
    - Introduced in Java 8, the `Optional` class helps handle null values gracefully, avoiding `NullPointerException`.

    === "Key Features"
        - **Avoid Null Checks**: Reduces explicit null checks.
        - **Functional Style**: Supports `map()`, `filter()`, and `ifPresent()`.
        - **Immutability**: Values cannot be modified after creation.

    === "When to Use"
        - Use as a return type for methods that may return null.
        - Avoid for fields, parameters, or collections to reduce overhead.

    ---

    === "Creating an `Optional`"
        - **Empty Optional**: Represents no value.

            ```java
            Optional<String> empty = Optional.empty();
            System.out.println(empty.isPresent()); // false
            ```
        - **With a Value**: Wraps a non-null value.

            ```java
            Optional<String> optional = Optional.of("Hello");
            System.out.println(optional.isPresent()); // true
            ```
        - **With Nullable Value**: Allows null values.

            ```java
            Optional<String> nullable = Optional.ofNullable(null);
            System.out.println(nullable.isPresent()); // false
            ```

    === "Common Methods"
        - **`isPresent()`**: Checks if a value exists.

            ```java
            Optional<String> optional = Optional.of("Hello");
            System.out.println(optional.isPresent()); // true
            ```
        - **`ifPresent(Consumer)`**: Executes code if a value exists.

            ```java
            Optional<String> optional = Optional.of("Hello");
            optional.ifPresent(value -> System.out.println("Value: " + value)); // Hello
            ```
        - **`orElse(T)`**: Returns the value or a default.

            ```java
            Optional<String> optional = Optional.ofNullable(null);
            System.out.println(optional.orElse("Default")); // Default
            ```
        - **`orElseGet(Supplier)`**: Returns the value or invokes a supplier.

            ```java
            Optional<String> optional = Optional.ofNullable(null);
            System.out.println(optional.orElseGet(() -> "Generated Default")); // Generated Default
            ```
        - **`orElseThrow(Supplier)`**: Throws an exception if no value exists.

            ```java
            Optional<String> optional = Optional.ofNullable(null);
            try {
                System.out.println(optional.orElseThrow(() -> new IllegalArgumentException("Value is missing")));
            } catch (Exception e) {
                System.out.println(e.getMessage()); // Value is missing
            }
            ```
        - **`map(Function)`**: Transforms the value if present.

            ```java
            Optional<String> optional = Optional.of("Hello");
            Optional<Integer> length = optional.map(String::length);
            System.out.println(length.orElse(0)); // 5
            ```
        - **`filter(Predicate)`**: Filters the value based on a condition.

            ```java
            Optional<String> optional = Optional.of("Hello");
            optional.filter(value -> value.startsWith("H"))
                    .ifPresent(System.out::println); // Hello
            ```

    === "Example"

        ```java
        import java.util.Optional;

        public class Main {
            public static void main(String[] args) {
                Optional<String> optional = Optional.ofNullable(getValue());

                optional.ifPresent(value -> System.out.println("Value: " + value));

                String result = optional.orElse("Default Value");
                System.out.println("Result: " + result);

                optional.map(String::toUpperCase)
                        .ifPresent(System.out::println);
            }

            private static String getValue() {
                return null; // Simulates a method that may return null
            }
        }
        ```