# Annotations

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