# Object Oriented Programming

### Class and Object

???+ note "Class and Object"
    === "Class"
        - A blueprint for creating objects.
        - Defines properties (attributes) and behaviors (methods).
        - Can contain constructors, methods, and nested classes.
        - Loaded by the class loader and stored in the Method Area.
        - Passed by reference and acts as a template for objects.
        - A user-defined data type and a collection of objects.
    === "Object"
        - An instance of a class.
        - Contains state (attributes) and behavior (methods).
        - Created using `new` keyword in heap memory.
        - Garbage collected when no longer referenced.
        - Passed by reference; changes to the object are reflected in the reference.
    === "Key Notes"
        - Class loading stores it in the Method Area; object creation allocates memory in the heap.
        - Static blocks initialize static variables and execute once when the class is loaded, before the main method or object creation.
        - Static blocks execute in the order they appear and only once, even if multiple objects are created.
        - If no object is created, the class, static block, constructor, and instance block are not executed.
        - Use `Class.forName("ClassName")` to execute static blocks without creating an object.
    === "Anonymous Object"
        - An object that has no reference is called an anonymous object.
        - Anonymous objects are used to call the methods of the class. After calling the method, the object is destroyed. So when you need to call a method only once, you can use an anonymous object.

        ```java
        class Example {
            void display() {
                System.out.println("Hello from Example class!");
            }
        }

        public class Main {
            public static void main(String[] args) {
                new Example().display(); // Creating an anonymous object and calling the method
            }
        }
        ```

### Inheritance

???+ note "Inheritance"
    - Inheritance allows a class (child class) to acquire properties and methods of another class (parent class).
    - Promotes code reuse and establishes a parent-child relationship.
    - Java supports single inheritance (a class can extend only one class and it can be multi leveled).
    - Java does not support multiple inheritance with classes to avoid ambiguity (diamond problem).
    - Multiple inheritance is supported through interfaces.
    - `extends` keyword is used to inherit from a class, and the `implements` keyword is used to implement interfaces.
    - For inheritance to work, the compiled `.class` files of the parent class must be available in the classpath.

    === "Multiple Inheritance through Interfaces"

        ```java
        interface InterfaceA {
            void methodA();
        }

        interface InterfaceB {
            void methodB();
        }

        class Implementation implements InterfaceA, InterfaceB {
            public void methodA() {
                System.out.println("Method A from InterfaceA");
            }

            public void methodB() {
                System.out.println("Method B from InterfaceB");
            }
        }

        public class Main {
            public static void main(String[] args) {
                Implementation obj = new Implementation();
                obj.methodA();
                obj.methodB();
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

        class Implementation implements InterfaceA, InterfaceB {
            @Override
            public void display() {
                // Resolving ambiguity by explicitly calling one of the interface methods
                InterfaceA.super.display();
                InterfaceB.super.display();
            }
        }

        public class Main {
            public static void main(String[] args) {
                Implementation obj = new Implementation();
                obj.display();
            }
        }
        ```

### `This` and `Super` Keywords

???+ note
    - The `this` keyword provides a reference to the current object in a method or constructor.
    - It is used to avoid naming conflicts between instance variables and parameters.
    - `this()` is used to call another constructor in the same class and must be the first statement in the constructor.
    - The `super` keyword provides a reference to the parent class.
    - `super()` is used to call the parent class's constructor and must be the first statement in the constructor.
    - If `super()` is not explicitly called, the compiler adds it by default.

    === "Using `this` and `super` in Constructors"

        ```java
        class A {
            public A() {
                super(); // Implicit call to Object class constructor
                System.out.println("in A");
            }
            public A(int n) {
                super();
                System.out.println("in A int");
            }
        }

        class B extends A {
            public B() {
                super(); // Explicit call to parent class constructor
                System.out.println("in B");
            }
            public B(int n) {
                this();  // Call constructor of the same class
                System.out.println("in B int");
            }
        }

        public class Demo {
            public static void main(String[] args) {
                // B obj = new B(); // Uncomment to see output for default constructor
                B obj = new B(5); // Calls parameterized constructor
            }
        }
        ```

        **Output:**
        ```
        in A
        in B
        in B int
        ```

    === "Using `this` in Methods"

        ```java
        class Example {
            int x; // Instance variable

            Example(int x) { // Constructor parameter
                this.x = x; // Assigning parameter value to instance variable
            }

            void display() {
                System.out.println("Value of x: " + this.x); // Accessing instance variable using 'this'
            }

            void setX(Example obj, int x) {
                obj.x = x;
            }

            // Using 'this' to refer to the current object the method is called on
            void setX(int x) {
                this.x = x; // Using 'this' to distinguish between instance variable and parameter
            }
        }

        public class Main {
            public static void main(String[] args) {
                Example obj = new Example(10);
                obj.display(); // Outputs: Value of x: 10
                obj.setX(20); // Using 'this' in the setX method
            }
        }
        ```


### `Static` Keyword

???+ note
    - The `static` keyword makes a variable or method belong to the class, not instances. Static members can be accessed without creating an object.

    === "Static Variables"
        - Shared by all instances of a class.
        - Initialized once when the class is loaded.
        - Accessed using the class name.

        ```java
        class Example {
            static int staticVar = 0;
            void increment() {
                staticVar++; // ✅ Accessing static variable within instance method
            }
        }
        public class Main {
            public static void main(String[] args) {
                Example obj1 = new Example();
                Example obj2 = new Example();
                obj1.increment();
                obj2.increment();
                System.out.println(Example.staticVar); // Outputs: 2
                Example.staticVar = 5; // Directly accessing static variable using class name
                System.out.println(obj1.staticVar); // Outputs: 5
            }
        }
        ```

    === "Static Methods"
        - Called without creating an object.
        - Can access static variables but not instance variables directly.
        - Needs object reference to access instance variables.
        

        ```java
        class Example {
            static int staticVar = 0;
            int instanceVar = 0;

            static void staticMethod() {
                System.out.println("Static var: " + staticVar);     // ✅ Accessing static variable in static method
                System.out.println("Instance var: " + instanceVar); // ❌ Accessing instance variable in static method will cause compilation error
            }
            static void staticMethod(Example obj) {
                System.out.println("Instance var: " + obj.instanceVar); // ✅ Accessing instance variable in static method using object reference
            }
        }
        ```

    === "Static Blocks"
        - Used to initialize static variables.
        - Executed once when the class is loaded.

        ```java
        class Example {
            static int staticVar;
            static {
                staticVar = 10;
                System.out.println("Static block executed.");
            }
            static void staticMethod() {
                System.out.println("Static method executed.");
            }
        }
        public class Main {
            public static void main(String[] args) {
                // Any statement which loads the class will execute the static block
                // For example, creating an instance of the class or accessing a static variable or method
                Example obj = new Example(); // This will trigger the static block
                // System.out.println(Example.staticVar); // This will also trigger the static block
                // Example.staticMethod(); // This will also trigger the static block
                // Class.forName("Example"); // This will also trigger the static block

                // If the class is already loaded, the static block won't execute again
                Example obj2 = new Example(); // This won't trigger the static block again
            }
        }
        ```

    === "Static Nested Classes"
        - A static class inside another class.
        - Does not need an instance of the outer class.
        - Can access static members of the outer class.

        ```java
        class OuterClass {
            static int staticVar = 10;

            static class NestedClass {
                void display() {
                    System.out.println("Static var: " + staticVar);
                }
            }
        }
        public class Main {
            public static void main(String[] args) {
                OuterClass.NestedClass nested = new OuterClass.NestedClass();
                nested.display(); // Outputs: Static var from OuterClass: 10
            }
        }
        ```

    === "Order of Execution"
        - Static variables and blocks are executed in the order they appear.
        - They run only once when the class is loaded.

        ```java
        class Example {
            static int staticVar = initializeStaticVar();
            static {
                System.out.println("Static block executed.");
            }

            static int initializeStaticVar() {
                System.out.println("Static variable initialized.");
                return 42;
            }
        }
        public class Main {
            public static void main(String[] args) {
                System.out.println("Static var: " + Example.staticVar);
            }
        }
        // Output:
        // Static variable initialized.
        // Static block executed.
        // Static var: 42
        ```

### Access Modifiers

???+ note
    - Access modifiers define the visibility and accessibility of classes, methods, and variables.
    - The table below summarizes the accessibility of different access modifiers:

    |                                | private  | default | protected | public |
    |:-------------------------------|:--------:|:-------:|:---------:|:------:|
    | Same Class                     |   ✅    |   ✅    |    ✅     |   ✅   |
    | Same Package                   |   ❌    |   ✅    |    ✅     |   ✅   |
    | Same Package Subclass          |   ❌    |   ❌    |    ✅     |   ✅   |
    | Different Package Subclass     |   ❌    |   ❌    |    ✅     |   ✅   |
    | Different Package Non-SubClass |   ❌    |   ❌    |    ❌     |   ✅   |

### Polymorphism

???+ note
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
                System.out.println(calc.add(2.5, 3.5)); // Outputs: 6.0
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
        class Cat extends Animal {
            @Override
            void eat() {
                System.out.println("Cat is eating");
            }
        }
        public class Test {
            public static void main(String[] args) {
                Animal a;
                a = new Dog();
                a.eat(); // Outputs: Dog is eating
                a = new Cat();
                a.eat(); // Outputs: Cat is eating
            }
        }
        ```

### `Final` Keyword

???+ note
    - The `final` keyword is used to restrict modification of variables, methods, and classes.
    - It is categorized into:

    === "Final Variable"
        - A `final` variable is a constant and cannot be reassigned after initialization.
        - Must be initialized during declaration, in a constructor, or in a block (static or instance).

        ```java
        class Example {
            final int constant; // Must be initialized

            // Initializing in constructor
            Example(int value) {
                this.constant = value;
            }

            // Uncommenting the following line will cause a compilation error
            // void modifyConstant() { constant = 10; }
        }
        ```

    === "Final Method"
        - A `final` method cannot be overridden by subclasses.
        - It can still be inherited and overloaded.

        ```java
        class Parent {
            final void display() {
                System.out.println("This is a final method.");
            }
        }

        class Child extends Parent {
            // Uncommenting the following will cause a compilation error
            // void display() {  } // Cannot override final method

            void display(String message) { // Overloading is allowed
                System.out.println(message);
            }
        }

        public class Main {
            public static void main(String[] args) {
                Child child = new Child();
                child.display("Overloaded method."); // Outputs: Overloaded method.
            }
        }
        ```

    === "Final Class"
        - A `final` class cannot be extended by any other class.
        - It can still be instantiated and used as is.

        ```java
        final class FinalClass {
            void display() {
                System.out.println("This is a final class.");
            }
        }

        // Uncommenting the following will cause a compilation error
        // class SubClass extends FinalClass {}

        public class Main {
            public static void main(String[] args) {
                FinalClass obj = new FinalClass();
                obj.display(); // Outputs: This is a final class.
            }
        }
        ```

### Object Class

???+ note
    - The `Object` class is the root class of all classes in Java.
    - It is the default superclass of all classes.
    - Every class in Java implicitly extends the `Object` class unless explicitly specified otherwise.
    - Commonly used methods of the `Object` class include `toString()` and `equals()`.

    === "toString() Method"
        - The `toString()` method returns a string representation of the object.
        - By default, it returns the class name followed by the `@` symbol and the hash code of the object.
        - It is often overridden to provide a meaningful string representation of the object.

        ```java
        class Example {
            int id;
            String name;

            Example(int id, String name) {
                this.id = id;
                this.name = name;
            }

            @Override
            public String toString() {
                return "Example{id=" + id + ", name='" + name + "'}";
            }
        }

        public class Main {
            public static void main(String[] args) {
                Example obj = new Example(1, "John");
                System.out.println(obj); // Outputs: Example{id=1, name='John'}
            }
        }
        ```

    === "equals() Method"
        - The `equals()` method is used to compare two objects for equality.
        - By default, it checks if two references point to the same object (reference equality).
        - It is often overridden to compare the content of objects (value equality).

        ```java
        class Example {
            int id;
            String name;

            Example(int id, String name) {
                this.id = id;
                this.name = name;
            }

            @Override
            public boolean equals(Object obj) {
                if (this == obj) return true; // Check if references are the same
                if (obj == null || getClass() != obj.getClass()) return false; // Check class type
                Example example = (Example) obj;
                return id == example.id && name.equals(example.name); // Compare fields
            }
        }

        public class Main {
            public static void main(String[] args) {
                Example obj1 = new Example(1, "John");
                Example obj2 = new Example(1, "John");
                Example obj3 = new Example(2, "Doe");

                System.out.println(obj1.equals(obj2)); // Outputs: true
                System.out.println(obj1.equals(obj3)); // Outputs: false
            }
        }
        ```

### Upcasting and Downcasting

???+ note
    - Upcasting and Downcasting are used to convert objects between parent and child classes.

    === "Upcasting"
        - Upcasting is casting from a subclass to a superclass.
        - It is done implicitly or explicitly.
        - Upcasting allows a child class object to be treated as a parent class object.

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
                Animal a = new Dog(); // Implicit upcasting same as Animal a = (Animal) new Dog();
                a.sound(); // Outputs: Dog barks
            }
        }
        ```

    === "Downcasting"
        - Downcasting is casting from a superclass to a subclass.
        - It must be done explicitly.
        - Downcasting allows access to methods and fields specific to the subclass.

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

            void fetch() {
                System.out.println("Dog fetches the ball");
            }
        }

        public class Test {
            public static void main(String[] args) {
                Animal a = new Dog(); // Upcasting
                a.sound(); // Outputs: Dog barks

                // Downcasting
                if (a instanceof Dog) {
                    Dog d = (Dog) a;
                    d.fetch(); // Outputs: Dog fetches the ball
                }
            }
        }
        ```

### Wrapper Class

???+ note
    - Wrapper classes in Java convert primitive types into objects and vice versa.
    - Since J2SE 5.0, autoboxing and unboxing automate this conversion.

    === "Boxing and Unboxing"
        - **Boxing**: Converts a primitive type into its corresponding wrapper class object.
        - **Unboxing**: Converts a wrapper class object back into its corresponding primitive type.

        ```java
        public class Main {
            public static void main(String[] args) {
                int x = 10;
                Integer y = Integer.valueOf(x); // Boxing
                int z = y.intValue();          // Unboxing

                System.out.println("Boxed: " + y); // Outputs: Boxed: 10
                System.out.println("Unboxed: " + z); // Outputs: Unboxed: 10
            }
        }
        ```

    === "Autoboxing and Autounboxing"
        - **Autoboxing**: Automatically converts a primitive type into its wrapper class object.
        - **Autounboxing**: Automatically converts a wrapper class object back into its primitive type.

        ```java
        public class Main {
            public static void main(String[] args) {
                int x = 20;
                Integer y = x; // Autoboxing
                int z = y;     // Autounboxing

                System.out.println("Autoboxed: " + y); // Outputs: Autoboxed: 20
                System.out.println("Autounboxed: " + z); // Outputs: Autounboxed: 20
            }
        }
        ```

    === "Tricky Question: Comparing Integer Objects"
        - Comparing two `Integer` objects using `==` depends on whether the values are within the Integer cache range (-128 to 127).

        ```java
        public class Main {
            public static void main(String[] args) {
                Integer i1 = 127;
                Integer i2 = 127;
                System.out.println(i1 == i2); // Outputs: true (within cache range)

                Integer i3 = 128;
                Integer i4 = 128;
                System.out.println(i3 == i4); // Outputs: false (outside cache range)
            }
        }
        ```
        
        - **Explanation**: Java caches `Integer` objects for values between -128 and 127. For values outside this range, new objects are created, so `==` compares references, not values.