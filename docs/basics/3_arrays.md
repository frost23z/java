# Arrays

## Quick Reference

!!! example "Array Declaration and Initialization"

    ```java
    int[] arr = new int[5];        // Fixed-size declaration
    int[] arr = {1, 2, 3};         // Initialization
    int[][] matrix = new int[3][]; // Jagged array
    ```

???+ info "When to Use Arrays"
    - Use arrays when you need a fixed-size collection of elements of the same type.
    - Ideal for scenarios where you need fast access to elements using an index.
    - Arrays are memory-efficient and provide better performance for fixed-size data.

???+ warning "Drawbacks of Arrays"
    - **Fixed Size**: Size cannot be changed after declaration.
    - **Homogeneous Data**: Only stores elements of the same type.
    - **Limited Methods**: No built-in methods for resizing, searching, or sorting.

### Jagged Arrays

???+ info "What are Jagged Arrays?"
    Arrays of arrays where sub-arrays can have different sizes, useful for non-rectangular data like triangles or sparse matrices.

    ```java
    int[][] jaggedArray = new int[3][];
    jaggedArray[0] = new int[]{1, 2};
    jaggedArray[1] = new int[]{3, 4, 5};
    jaggedArray[2] = new int[]{6};

    for (int[] row : jaggedArray) {
        for (int num : row) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
    // Output:
    // 1 2
    // 3 4 5
    // 6
    ```

### Arrays of Objects

???+ info "Arrays of Objects"
    - Arrays of objects store **references** to the objects, not the objects themselves.
    - Each object in the array must be manually created and initialized.
    - If an object is not initialized, its reference will be `null`. In this case, trying to access its properties or methods will result in a `NullPointerException`.
    === "Example"

        ```java
        class Person {
            String name;
            Person(String name) {
                this.name = name;
            }
        }

        Person[] people = new Person[3];
        people[0] = new Person("Alice");
        people[1] = new Person("Bob");
        people[2] = new Person("Charlie");

        for (Person person : people) {
            System.out.println(person.name);
        }
        // Output:
        // Alice
        // Bob
        // Charlie
        ```
    === "Exceptions"

        ```java
        Person[] people = new Person[3];
        // people[0] is null, accessing it will throw NullPointerException
        System.out.println(people[0].name); // Throws NullPointerException
        ```