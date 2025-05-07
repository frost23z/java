# String

## String Creation and Memory

???+ info "String Initialization"
    In Java, `String` is a **final class**, meaning it cannot be extended. Strings are objects and can be created in two ways:

    - **String Literal (Recommended):** Stored in the String Constant Pool, reuses references for identical strings.

      ```java
      String str = "Hello";  // Reuses reference
      ```
    - **String Object:** Stored in Heap Memory, creates a new object even if identical string exists.

      ```java
      String str = new String("Hello");
      ```

???+ info "String Immutability and Garbage Collection"
    Strings are immutable. Modifying a string creates a new object, leaving the original eligible for garbage collection if unreferenced.

    ```java
    String str = "Hello";
    str = "World"; // "Hello" becomes eligible for garbage collection
    System.out.println(str); // Outputs: World
    ```

## Mutable Strings

???+ info "Mutable Strings"
    - **StringBuilder:** Faster, not thread-safe.
    - **StringBuffer:** Thread-safe, slower due to synchronization.
    
    > Use `StringBuilder` for performance in single-threaded scenarios and `StringBuffer` for thread-safe operations.

    ```java
    StringBuilder sb = new StringBuilder("Hello");
    sb.append(" World"); // Modifies the original object
    System.out.println(sb); // Outputs: Hello World
    ```

    > Use these classes in loops or for frequent string modifications to avoid creating multiple immutable objects.

    ```java
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 100000; i++) {
        sb.append(i); // Efficient thanks to mutable nature. If strings were used, it would create 100,000 objects.
    }
    System.out.println(sb.toString());
    ```

## String Joiner

???+ info "Joining Strings"
    - Joins strings with a delimiter, prefix, and suffix.

    ```java
    import java.util.StringJoiner;

    StringJoiner joiner = new StringJoiner(", ", "[", "]");
    joiner.add("Apple").add("Banana").add("Orange");
    System.out.println(joiner); // Outputs: [Apple, Banana, Orange]
    ```