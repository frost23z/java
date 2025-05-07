# Wrapper Class

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

    === "Integer Cache"
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
