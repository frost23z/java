# Lambda Expressions

???+ note "Lambda Expressions"
    - Lambda expressions provide a concise way to represent anonymous functions, introduced in Java 8.
    - Commonly used with functional interfaces (interfaces with a single abstract method).
    - **Benefits**:
        - Reduces boilerplate code.
        - Enhances readability and maintainability.
        - Simplifies operations on collections and functional interfaces.

    === "Basic Syntax"
        - Syntax: `(parameters) -> expression` or `(parameters) -> { statements }`
        - Example:

        ```java
        interface Greeting {
            void sayHello(String name);
        }

        public class Main {
            public static void main(String[] args) {
                Greeting greeting = (name) -> System.out.println("Hello, " + name + "!");
                greeting.sayHello("John"); // Outputs: Hello, John!
            }
        }
        ```

    === "Using with Collections"
        - Simplifies operations like filtering, mapping, and iterating.

        ```java
        import java.util.Arrays;
        import java.util.List;

        public class Main {
            public static void main(String[] args) {
                List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

                names.stream()
                     .filter(name -> name.startsWith("A"))
                     .forEach(System.out::println); // Outputs: Alice
            }
        }
        ```

    === "Method References"
        - Method references provide a shorthand notation for calling methods using `ClassName::methodName`.

        ```java
        import java.util.Arrays;
        import java.util.List;

        public class Main {
            public static void main(String[] args) {
                List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

                names.forEach(System.out::println); // Outputs: Alice Bob Charlie
            }
        }
        ```

    === "Functional Interfaces"
        - Compatible with functional interfaces like `Predicate`, `Function`, `Consumer`, and `Supplier`.

        ```java
        import java.util.function.Predicate;

        public class Main {
            public static void main(String[] args) {
                Predicate<Integer> isEven = n -> n % 2 == 0;
                System.out.println(isEven.test(4)); // Outputs: true
            }
        }
        ```