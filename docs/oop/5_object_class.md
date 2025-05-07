# Object Class

???+ abstract "`Object` Class"
    - The `Object` class is the root class of all classes in Java.
    - Every class in Java implicitly extends the `Object` class unless explicitly specified otherwise.
    - Commonly used methods include `toString()` and `equals()`.

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