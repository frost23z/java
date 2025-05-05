# Additional

### Annotations

???+ note "Annotations"
    - Annotations are a way to add metadata to your code.
    - They provide additional information about the code, such as its purpose, author, or version.
    - Common use cases include:
        - Marking code as deprecated.
        - Providing hints to the compiler.
        - Associating metadata with classes, methods, or variables.

    === "Key Features"
        - **Retention Policies**:
            - `SOURCE`: Annotations are discarded during the compile-time.
            - `CLASS`: Annotations are present in the `.class` file but not available at runtime.
            - `RUNTIME`: Annotations are available at runtime via reflection.
        - **Target Elements**:
            - `@Target` specifies where an annotation can be applied (e.g., `METHOD`, `FIELD`, `TYPE`).
        - **Custom Annotations**:
            - You can define your own annotations using `@interface`.

    === "Common Built-in Annotations"
        - **`@Override`**: 
            - Indicates that a method overrides a method in a superclass.
            - **Benefit**: Ensures that the method exists in the superclass. If the method signature is incorrect or the method does not exist, the compiler will throw an error, preventing runtime issues.
            - Example:

                ```java
                class Parent {
                    void display() {
                        System.out.println("Parent display");
                    }
                }

                class Child extends Parent {
                    @Override
                    void display() { // Ensures this method correctly overrides the parent method
                        System.out.println("Child display");
                    }
                }
                ```

        - **`@Deprecated`**: 
            - Marks a method or class as deprecated.
            - **Benefit**: Alerts developers that the annotated element should no longer be used and may be removed in future versions.
            - Example:

                ```java
                class Example {
                    @Deprecated
                    public void oldMethod() {
                        System.out.println("This method is deprecated.");
                    }
                }
                ```

        - **`@SuppressWarnings`**: 
            - Suppresses compiler warnings.
            - **Benefit**: Allows developers to suppress specific warnings, keeping the code clean without removing potentially useful constructs.
            - Example:

                ```java
                class Example {
                    @SuppressWarnings("unchecked")
                    public void uncheckedMethod() {
                        // Suppresses unchecked warnings
                    }
                }
                ```

        - **`@FunctionalInterface`**: 
            - Marks an interface as a functional interface (with a single abstract method).
            - **Benefit**: Ensures that the interface has exactly one abstract method. If additional methods are added, the compiler will throw an error. Some IDEs also provide real-time feedback before compilation.
            - Example:

                ```java
                @FunctionalInterface
                interface Greeting {
                    void sayHello(String name); // Single abstract method
                }

                public class Main {
                    public static void main(String[] args) {
                        Greeting greeting = (name) -> System.out.println("Hello, " + name + "!");
                        greeting.sayHello("John"); // Outputs: Hello, John!
                    }
                }
                ```

    === "Custom Annotations"
        - You can create custom annotations using `@interface`.
        - Example:

        ```java
        import java.lang.annotation.ElementType;
        import java.lang.annotation.Retention;
        import java.lang.annotation.RetentionPolicy;
        import java.lang.annotation.Target;

        @Retention(RetentionPolicy.RUNTIME)
        @Target(ElementType.METHOD)
        public @interface MyAnnotation {
            String value();
        }

        class Example {
            @MyAnnotation(value = "Custom Annotation Example")
            public void annotatedMethod() {
                System.out.println("This method is annotated.");
            }
        }
        ```

    === "Processing Annotations"
        - Annotations with `RUNTIME` retention can be processed using reflection.

        ```java
        import java.lang.reflect.Method;

        public class AnnotationProcessor {
            public static void main(String[] args) throws Exception {
                Method method = Example.class.getMethod("annotatedMethod");
                if (method.isAnnotationPresent(MyAnnotation.class)) {
                    MyAnnotation annotation = method.getAnnotation(MyAnnotation.class);
                    System.out.println("Annotation value: " + annotation.value());
                }
            }
        }
        ```

### Lambda Expressions

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

### Exception Handling

???+ info "Overview"
    Exception handling in Java is a mechanism to handle runtime errors, ensuring the normal flow of the application. It uses `try`, `catch`, `finally`, `throw`, and `throws` keywords.

    === "Basic Example"

        ```java
        try {
            int result = 10 / 0; // This will throw ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero: " + e.getMessage());
        } finally {
            System.out.println("Execution completed.");
        }
        ```

???+ info "Checked vs Unchecked Exceptions"
    - **Checked Exceptions:** Must be declared in the method signature using `throws` or handled with `try-catch`.
        - Example: `IOException`, `SQLException`
    - **Unchecked Exceptions:** Do not need to be declared or handled.
        - Example: `ArithmeticException`, `NullPointerException`

???+ info "Custom Exceptions"
    You can create your own exceptions by extending the `Exception` class.

    === "Example"

        ```java
        class CustomException extends Exception {
            public CustomException(String message) {
                super(message);
            }
        }

        public class Main {
            public static void main(String[] args) {
                try {
                    throw new CustomException("This is a custom exception");
                } catch (CustomException e) {
                    System.out.println(e.getMessage());
                }
            }
        }
        ```

### Exception Hierarchy

???+ info "Exception Hierarchy"
    The following diagram illustrates the hierarchy of exceptions in Java:

    ```mermaid
    classDiagram
        Object <|-- Throwable
        Throwable <|-- Error
        Throwable <|-- Exception
        Error <|-- ThreadDeath
        Error <|-- IOError
        Error <|-- OutOfMemoryError
        Error <|-- VirtualMachineError
        Exception <|-- RuntimeException
        Exception <|-- IOException
        Exception <|-- SQLException
        RuntimeException <|-- ArithmeticException
        RuntimeException <|-- NullPointerException
        RuntimeException <|-- IndexOutOfBoundsException
    ```

### `throws` Keyword

???+ info "`throws` Keyword"
    - The `throws` keyword in Java is used in a method declaration to specify the exceptions that the method can throw.
    - It informs the caller of the method about the exceptions that need to be handled or declared further.

    === "Syntax"
        ```java
        returnType methodName(parameters) throws ExceptionType1, ExceptionType2 {
            // Method body
        }
        ```

    === "Example"

        ```java
        import java.io.IOException;

        public class Example {
            public void readFile() throws IOException {
                throw new IOException("File not found");
            }

            public static void main(String[] args) {
                Example example = new Example();
                try {
                    example.readFile();
                } catch (IOException e) {
                    System.out.println("Caught exception: " + e.getMessage());
                }
            }
        }
        ```

    === "Key Points"
    - The `throws` keyword is used to declare checked exceptions.
    - It does not handle the exception; it only propagates it to the caller.
    - Multiple exceptions can be declared, separated by commas.
    - Unchecked exceptions (subclasses of `RuntimeException`) do not need to be declared with `throws`.

### Try with Resources

???+ info "Try with Resources"
    - The "try-with-resources" statement in Java is used to automatically close resources (like files, sockets, or database connections) that implement the `AutoCloseable` interface.
    - Introduced in Java 7, it simplifies resource management and reduces boilerplate code.

    === "Syntax"

        ```java
        try (ResourceType resource = new ResourceType()) {
            // Use the resource
        } catch (ExceptionType e) {
            // Handle exception
        }
        ```

    === "Example"

        ```java
        import java.io.BufferedReader;
        import java.io.FileReader;
        import java.io.IOException;

        public class Example {
            public static void main(String[] args) {
                try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
                    String line;
                    while ((line = reader.readLine()) != null) {
                        System.out.println(line);
                    }
                } catch (IOException e) {
                    System.out.println("Error reading file: " + e.getMessage());
                }
            }
        }
        ```

    === "Key Points"
    - Resources declared in the `try` block are automatically closed at the end of the block.
    - Multiple resources can be declared, separated by semicolons (`;`).
    - The resources must implement the `AutoCloseable` interface (or its subinterface, `Closeable`).
    - Reduces the need for explicit `finally` blocks to close resources.