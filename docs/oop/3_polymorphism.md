# Polymorphism

???+ abstract "Polymorphism"
    - Polymorphism allows methods to perform different tasks based on the object or context.
    - It is categorized into:

    === "Compile-Time Polymorphism (Method Overloading)"
        - Resolved at compile-time.
        - Methods have the same name but differ in the number or type of arguments.

        ```java
        class Calculator {
            int add(int a, int b) {
                return a + b;
            }
            double add(double a, double b) {
                return a + b;
            }
        }

        public class Main {
            public static void main(String[] args) {
                Calculator calc = new Calculator();
                System.out.println(calc.add(2, 3));       // Outputs: 5
                System.out.println(calc.add(2.5, 3.5));   // Outputs: 6.0
            }
        }
        ```

    === "Run-Time Polymorphism (Method Overriding)"
        - Resolved at runtime.
        - Methods have the same name and signature but are overridden in subclasses.
        - Dynamic method dispatch determines the method to call based on the object type.

        ```java
        class Animal {
            void eat() {
                System.out.println("Animal is eating");
            }
        }

        class Dog extends Animal {
            @Override
            void eat() {
                System.out.println("Dog is eating");
            }
        }

        public class Test {
            public static void main(String[] args) {
                Animal a = new Dog(); // Polymorphic reference
                a.eat();              // Outputs: Dog is eating
            }
        }
        ```

## Casting in Polymorphism

???+ abstract "Casting"
    - Casting is used to convert objects between parent and child classes, often in the context of polymorphism.

    === "Upcasting"
        - Casting from a subclass to a superclass.
        - Done implicitly or explicitly.
        - Allows treating a child class object as a parent class object.

        ```java
        class Animal {
            void sound() {
                System.out.println("Animal makes a sound");
            }
        }

        class Dog extends Animal {
            void sound() {
                System.out.println("Dog barks");
            }
        }

        public class Test {
            public static void main(String[] args) {
                Animal a = new Dog(); // Implicit upcasting
                a.sound();            // Outputs: Dog barks
            }
        }
        ```

    === "Downcasting"
        - Casting from a superclass to a subclass.
        - Must be done explicitly.
        - Allows access to methods and fields specific to the subclass.
        - Requires type checking with `instanceof` to avoid `ClassCastException`.

        ```java
        class Animal {
            void sound() {
                System.out.println("Animal makes a sound");
            }
        }

        class Dog extends Animal {
            void fetch() {
                System.out.println("Dog fetches the ball");
            }
        }

        public class Test {
            public static void main(String[] args) {
                Animal a = new Dog(); // Upcasting
                if (a instanceof Dog) {
                    Dog d = (Dog) a;  // Explicit downcasting
                    d.fetch();        // Outputs: Dog fetches the ball
                }
            }
        }
        ```
