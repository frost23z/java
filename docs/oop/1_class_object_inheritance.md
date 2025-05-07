# Class, Object, and Inheritance

## Class and Object

???+ abstract "Class and Object"
    === "Class"
        - A **class** is a blueprint or template for creating objects.
        - It defines **fields** (attributes/properties) and **methods** (behaviors/functions).
        - Can include constructors, static blocks, and nested classes.
        - Loaded once by the class loader and stored in the **Method Area**.
        - No memory for fields is allocated until an object is created.
        - Classes help organize code and promote reusability.

        ```java
        class Car {
            String color;
            void drive() {
                System.out.println("Driving...");
            }
        }
        ```
        
    === "Object"
        - An **object** is an instance of a class.
        - Has its own state (values of fields) and behavior (methods).
        - Created using the `new` keyword; memory is allocated in the **heap**.
        - Multiple objects can be created from the same class, each with independent state.
        - Objects are garbage collected when no longer referenced.

        ```java
        Car myCar = new Car(); // Object creation
        myCar.color = "Red";
        myCar.drive();
        ```

    === "Key Differences"

        | Class                     | Object                     |
        |---------------------------|----------------------------|
        | Blueprint/template        | Instance of a class        |
        | No memory allocated       | Memory allocated in heap   |
        | Defines structure         | Has actual data/state      |
        | Loaded once               | Can create many objects    |
        | Stored in **Method Area** | **Stored in Heap**         |

    === "Anonymous Object"
        - An object created without a reference variable.
        - Useful for one-time method calls or quick operations.
        - Destroyed after the statement; no reference is kept.

        ```java
        new Car().drive(); // Anonymous object
        ```

        - Common in event handling and callbacks.
        - Saves memory if the object is not needed after the method call.

    !!! info ""
        - **Class:** Blueprint, defines structure, no memory until instantiated.
        - **Object:** Instance, has state/behavior, memory allocated in heap.
        - **Anonymous Object:** No reference, used for one-time actions.

        > **Tip:** Use classes to model real-world entities and objects to represent specific instances in your programs.

## Inheritance

???+ abstract "Inheritance"
    - Inheritance allows a class (child class) to acquire properties and methods of another class (parent class).
    - It promotes code reuse and establishes a parent-child relationship.
    - Java supports **single inheritance**, where a class can extend only one parent class. However, this can be multi-leveled (a class can inherit from another class, which in turn inherits from another class, and so on).
    - Java does not support **multiple inheritance** with classes to avoid ambiguity (commonly referred to as the "diamond problem").
    - **Multiple inheritance** is supported through interfaces, allowing a class to implement multiple interfaces.
    - The `extends` keyword is used to inherit from a class, and the `implements` keyword is used to implement interfaces.
    - For inheritance to work, the compiled `.class` files of the parent class must be available in the classpath.

    === "Multiple Inheritance through Interfaces"

        ```java
        interface InterfaceA {
            void methodA();
        }

        interface InterfaceB {
            void methodB();
        }

        // A class implementing both interfaces
        class Implementation implements InterfaceA, InterfaceB {
            @Override
            public void methodA() {
                System.out.println("Method A from InterfaceA");
            }

            @Override
            public void methodB() {
                System.out.println("Method B from InterfaceB");
            }
        }

        public class Main {
            public static void main(String[] args) {
                Implementation obj = new Implementation();
                obj.methodA(); // Calls methodA from InterfaceA
                obj.methodB(); // Calls methodB from InterfaceB
            }
        }
        ```

    === "Method Resolution in Multiple Interfaces"
        - If two interfaces have methods with the same signature, the implementing class must override the method to resolve ambiguity.

        ```java
        interface InterfaceA {
            default void display() {
                System.out.println("Display from InterfaceA");
            }
        }

        interface InterfaceB {
            default void display() {
                System.out.println("Display from InterfaceB");
            }
        }

        // A class implementing both interfaces
        class Implementation implements InterfaceA, InterfaceB {
            @Override
            public void display() {
                // Resolving ambiguity by explicitly calling methods from both interfaces
                InterfaceA.super.display();
                InterfaceB.super.display();
            }
        }

        public class Main {
            public static void main(String[] args) {
                Implementation obj = new Implementation();
                obj.display(); // Calls display methods from both interfaces
            }
        }
        ```

## `this` and `super` Keywords

???+ info "this and super"
    - `this` refers to the current object, used to resolve naming conflicts or call another constructor in the same class.
    - `super` refers to the parent class, used to access parent class members or call its constructor.
    - `this()` and `super()` must be the first statement in a constructor.
    - If `super()` is not explicitly called, the compiler adds it by default.

    === "Using `this` and `super` in Constructors"

        ```java
        class A {
            public A() {
                System.out.println("in A");
            }
            public A(int n) {
                System.out.println("in A int");
            }
        }

        class B extends A {
            public B() {
                super(); // Calls parent class constructor
                System.out.println("in B");
            }
            public B(int n) {
                this();  // Calls another constructor in the same class
                System.out.println("in B int");
            }
        }

        public class Demo {
            public static void main(String[] args) {
                B obj = new B(5); // Output: in A, in B, in B int
                // Additional test to demonstrate the use of constructors
                B obj2 = new B(); // Output: in A, in B
            }
        }
        ```

    === "Using `this` in Methods"

        ```java
        class Example {
            int x;

            Example(int x) {
                this.x = x; // Resolves naming conflict
            }

            void display() {
                System.out.println("Value of x: " + this.x);
            }

            void setX(int x) {
                this.x = x; // Refers to the instance variable
            }
        }

        public class Main {
            public static void main(String[] args) {
                Example obj = new Example(10);
                obj.display(); // Output: Value of x: 10
                obj.setX(20);
                obj.display(); // Output: Value of x: 20
            }
        }
        ```


## Inner Class

???+ abstract "Inner Class"
    - An **Inner Class** is a class defined within another class.
    - Inner classes can access the members (including private members) of the outer class.
    - They are used to logically group classes that are only used in one place or to increase encapsulation.
    - Types of inner classes:
        - **Non-static Inner Class**: Associated with an instance of the outer class.
        - **Static Nested Class**: Does not require an instance of the outer class.
        - **Local Inner Class**: Defined inside a method or block.
        - **Anonymous Inner Class**: A class without a name, used for one-time use.

    === "Non-static Inner Class"
        - Tied to an instance of the outer class.
        - Can access all members of the outer class, including private ones.
        - Use when the inner class logically depends on an instance of the outer class.

        ```java
        class Outer {
            private String message = "Hello from Outer class!";

            class Inner {
                void display() {
                    System.out.println(message); // Accessing outer class's private member
                }
            }
        }

        public class Main {
            public static void main(String[] args) {
                Outer outer = new Outer(); // Create an object of the outer class
                Outer.Inner inner = outer.new Inner(); // Create an object of the inner class
                inner.display(); // Outputs: Hello from Outer class!
            }
        }
        ```

    === "Static Nested Class"
        - Not tied to an instance of the outer class.
        - Can only access static members of the outer class.
        - Use when the nested class does not require access to instance members of the outer class.

        ```java
        class Outer {
            static String staticMessage = "Hello from Outer class!";

            static class Nested {
                void display() {
                    System.out.println(staticMessage); // Accessing static member of the outer class
                }
            }
        }

        public class Main {
            public static void main(String[] args) {
                Outer.Nested nested = new Outer.Nested(); // Create an instance of the static nested class
                nested.display(); // Outputs: Hello from Outer class!
            }
        }
        ```

    === "Local Inner Class"
        - Defined inside a method or block.
        - Can access local variables of the enclosing method if they are declared `final` or effectively final.
        - Use for encapsulating logic that is specific to a single method.

        ```java
        class Outer {
            void display() {
                final String localMessage = "Hello from Local Inner Class!";

                class LocalInner {
                    void print() {
                        System.out.println(localMessage); // Accessing local variable
                    }
                }

                LocalInner localInner = new LocalInner();
                localInner.print(); // Outputs: Hello from Local Inner Class!
            }
        }

        public class Main {
            public static void main(String[] args) {
                Outer outer = new Outer();
                outer.display();
            }
        }
        ```

    === "Anonymous Inner Class"
        - A class without a name, used for one-time use.
        - Can provide an implementation of an interface, extend a class, or instantiate an abstract class.
        - Use for quick, one-off implementations.

        ```java
        abstract class Shape {
            abstract void draw();
        }

        public class Main {
            public static void main(String[] args) {
                // Instantiating an abstract class using an anonymous inner class
                Shape shape = new Shape() {
                    @Override
                    void draw() {
                        System.out.println("Drawing a shape using an anonymous inner class!");
                    }
                };

                shape.draw(); // Outputs: Drawing a shape using an anonymous inner class!
            }
        }
        ```

    === "When to Use Each Type"
        - **Non-static Inner Class**: When the inner class needs access to instance members of the outer class.
        - **Static Nested Class**: When the inner class does not need access to instance members of the outer class.
        - **Local Inner Class**: When the inner class is specific to a method and encapsulates method-specific logic.
        - **Anonymous Inner Class**: When a one-time implementation of an interface, abstract class, or superclass is needed.
