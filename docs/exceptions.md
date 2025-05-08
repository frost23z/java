# Exception Handling

## Overview

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

## Exception Hierarchy

???+ info "Exception Hierarchy"
    The following diagram illustrates the hierarchy of exceptions in Java:

    ```mermaid
    flowchart TD
        Object --> Throwable
        Throwable --> Error
        Throwable --> Exception
        Error --> ThreadDeath
        Error --> IOError
        Error --> OutOfMemoryError
        Error --> VirtualMachineError
        Exception --> RuntimeException
        Exception --> IOException
        Exception --> SQLException
        RuntimeException --> ArithmeticException
        RuntimeException --> NullPointerException
        RuntimeException --> IndexOutOfBoundsException
    ```

## `throws` Keyword

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