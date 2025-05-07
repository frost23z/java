# Modifiers

## Access Modifiers

???+ info "Access Modifiers"
    - Access modifiers define the visibility and accessibility of classes, methods, and variables.
    - The table below summarizes the accessibility of different access modifiers:

    |                                | private | default | protected | public |
    |:-------------------------------|:-------:|:-------:|:---------:|:------:|
    | Same Class                     |   ✅    |   ✅    |    ✅     |   ✅   |
    | Same Package                   |   ❌    |   ✅    |    ✅     |   ✅   |
    | Same Package Subclass          |   ❌    |   ❌    |    ✅     |   ✅   |
    | Different Package Subclass     |   ❌    |   ❌    |    ✅     |   ✅   |
    | Different Package Non-SubClass |   ❌    |   ❌    |    ❌     |   ✅   |

## Non-Access Modifiers
???+ info "Non-Access Modifiers"
    - Non-access modifiers provide additional functionality to classes, methods, and variables.
    - Common non-access modifiers include `static`, `final`, `abstract`, `synchronized`, and `volatile`.

### Static Keyword

???+ info "Static Keyword"
    - The `static` keyword makes a variable, method, or block belong to the class rather than instances. It is shared across all instances and can be accessed without creating an object.

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
                obj1.increment();
                System.out.println(Example.staticVar); // Outputs: 1
            }
        }
        ```

    === "Static Methods"
        - Called without creating an object.
        - Can access static variables directly but require an object reference to access instance variables.

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
        - Used to initialize static variables or perform setup tasks.
        - Executed once when the class is loaded, before any object creation or `main()` execution.

        ```java
        class Example {
            static int staticVar;
            static {
                staticVar = 10;
                System.out.println("Static block executed.");
            }
        }
        ```

    === "Static Nested Classes"
        - A static class inside another class.
        - Does not require an instance of the outer class.
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
                nested.display(); // Outputs: Static var: 10
            }
        }
        ```

    === "Order of Execution"
        - Static variables and blocks are executed in the order they appear in the class.
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

### Final Keyword

???+ info "Final Keyword"
    - The `final` keyword restricts modification of variables, methods, and classes.

    === "Final Variable"
        - A `final` variable is a constant and cannot be reassigned after initialization.
        - Must be initialized during declaration, in a constructor, or in a block.

        ```java
        class Example {
            final int constant;

            Example(int value) {
                this.constant = value; // Initialization in constructor
            }

            // Uncommenting the following statement will cause a compilation error
            // void modifyConstant() { constant = 10; }
        }
        ```

    === "Final Method"
        - A `final` method cannot be overridden by subclasses but can be inherited and overloaded.

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
        - A `final` class cannot be extended but can be instantiated and used.

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
