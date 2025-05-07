# Abstraction

## Abstract Class

???+ abstract "Abstract Class"
    - An abstract class is a blueprint for other classes and cannot be instantiated directly.
    - Declared with the `abstract` keyword, it can include:
        - **Abstract methods**: Methods without implementation that must be overridden by subclasses.
        - **Concrete methods**: Methods with implementation that can be inherited by subclasses.
    - Abstract classes allow code reuse and enforce a structure for subclasses.

    === "Key Features"
        - Cannot be instantiated directly.
        - Can have both abstract and concrete methods.
        - Can have constructors, which are called during subclass instantiation.
        - Abstract methods cannot be private, static, or final.

    === "Example: Abstract Class"

        ```java
        abstract class Shape {
            protected String color;

            public Shape(String color) {
                this.color = color;
            }

            abstract double calculateArea();

            public void displayColor() {
                System.out.println("Color: " + color);
            }
        }

        class Circle extends Shape {
            private double radius;

            public Circle(String color, double radius) {
                super(color);
                this.radius = radius;
            }

            @Override
            double calculateArea() {
                return Math.PI * radius * radius;
            }
        }

        public class AbstractDemo {
            public static void main(String[] args) {
                // Shape shape = new Shape("Red"); // ❌ Cannot instantiate abstract class
                Circle circle = new Circle("Blue", 5.0);
                circle.displayColor();             // Outputs: Color: Blue
                System.out.println("Area: " + circle.calculateArea()); // Outputs: Area: 78.54
            }
        }
        ```

    === "Abstract Class vs Interface"

        | Feature           | Abstract Class                       | Interface                          |
        |-------------------|--------------------------------------|------------------------------------|
        | Instantiation     | Cannot be instantiated              | Cannot be instantiated            |
        | Inheritance       | Single inheritance only             | Multiple inheritance possible     |
        | Fields            | Can have instance variables         | Only constants (public static final) |
        | Methods           | Abstract and concrete methods       | Abstract (pre-Java 8), default/static (Java 8+) |
        | Constructor       | Can have constructors               | Cannot have constructors          |
        | Purpose           | "is-a" relationship (shared code)   | "can-do" relationship (API contract) |
        | Usage             | For related classes with shared implementation | For unrelated classes needing common behavior |

## Interface

???+ note "Interface"
    - An **Interface** defines a contract for behavior and is implemented by classes.
    - Key characteristics:
        - All methods are `public` and `abstract` by default (pre-Java 8).
        - All variables are `public`, `static`, and `final` by default.
        - Supports multiple inheritance.
        - Can have default and static methods (since Java 8).
        - Functional interfaces (with a single abstract method) are used in lambda expressions.

    === "Example"

        ```java
        interface Animal {
            void eat();     // implicitly public and abstract
            void sleep();
        }

        class Dog implements Animal {
            @Override
            public void eat() {
                System.out.println("Dog is eating");
            }

            @Override
            public void sleep() {
                System.out.println("Dog is sleeping");
            }
        }

        public class Main {
            public static void main(String[] args) {
                Animal dog = new Dog();
                dog.eat();   // Outputs: Dog is eating
                dog.sleep(); // Outputs: Dog is sleeping
            }
        }
        ```

    === "Default and Static Methods (Java 8+)"

        ```java
        interface Vehicle {
            void start();

            default void stop() { // Default method
                System.out.println("Vehicle is stopping");
            }

            static void service() { // Static method
                System.out.println("Vehicle is being serviced");
            }
        }

        class Car implements Vehicle {
            @Override
            public void start() {
                System.out.println("Car is starting");
            }
        }

        public class Main {
            public static void main(String[] args) {
                Vehicle car = new Car();
                car.start();       // Outputs: Car is starting
                car.stop();        // Outputs: Vehicle is stopping
                Vehicle.service(); // Outputs: Vehicle is being serviced
            }
        }
        ```

    === "Functional Interface and Lambda Expressions"
        - Functional interfaces are essential for enabling functional programming in Java.
        - They simplify the use of lambda expressions and method references, making code more concise and readable.

        ```java
        @FunctionalInterface
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

        === "Method References"
            - Method references provide a shorthand for calling methods using the `::` operator.
            - Types of method references:
                1. **Static Method Reference**: `ClassName::staticMethod`
                2. **Instance Method Reference**: `instance::instanceMethod`
                3. **Instance Method of an Arbitrary Object**: `ClassName::instanceMethod`

            ```java
            import java.util.Arrays;
            import java.util.List;

            public class Main {
                public static void main(String[] args) {
                    List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

                    // Static method reference
                    names.forEach(System.out::println); // Outputs: Alice Bob Charlie

                    // Instance method reference
                    names.stream()
                         .map(String::toUpperCase)
                         .forEach(System.out::println); // Outputs: ALICE BOB CHARLIE
                }
            }
            ```

        === "Constructor References"
            - Constructor references are used to create objects using the `::` operator.
            - Syntax: `ClassName::new`

            ```java
            import java.util.function.Supplier;

            class Example {
                String message;

                public Example() {
                    this.message = "Default Constructor";
                }

                public Example(String message) {
                    this.message = message;
                }

                @Override
                public String toString() {
                    return message;
                }
            }

            public class Main {
                public static void main(String[] args) {
                    // Constructor reference for default constructor
                    Supplier<Example> defaultConstructor = Example::new;
                    Example example1 = defaultConstructor.get();
                    System.out.println(example1); // Outputs: Default Constructor

                    // Constructor reference for parameterized constructor
                    java.util.function.Function<String, Example> paramConstructor = Example::new;
                    Example example2 = paramConstructor.apply("Parameterized Constructor");
                    System.out.println(example2); // Outputs: Parameterized Constructor
                }
            }
            ```

    === "Marker Interface"
        - **Marker Interface**: An interface with no methods, used to mark a class for specific behavior (e.g., `Serializable`).

        ```java
        // Marker Interface Example
        interface Marker {}

        class Example implements Marker {
            // Class marked with Marker interface
        }
        ```

    === "Extending Interfaces"

        ```java
        interface A {
            void methodA();
        }

        interface B extends A {
            void methodB();
        }

        class Implementation implements B {
            @Override
            public void methodA() {
                System.out.println("Method A from Interface A");
            }

            @Override
            public void methodB() {
                System.out.println("Method B from Interface B");
            }
        }

        public class Main {
            public static void main(String[] args) {
                B obj = new Implementation();
                obj.methodA(); // Outputs: Method A from Interface A
                obj.methodB(); // Outputs: Method B from Interface B
            }
        }
        ```

## When to Use

???+ tip "When to Use Abstract Classes"
    - Use abstract classes when:
        - You need to share code among closely related classes.
        - You want to provide a common base class with default behavior.
        - You need constructors or non-final instance variables.

???+ tip "When to Use Interfaces"
    - Use interfaces when:
        - You need to define a contract for unrelated classes.
        - You want to achieve multiple inheritance.
        - You need to take advantage of default or static methods (Java 8+).
        - You are designing functional interfaces for lambda expressions.
