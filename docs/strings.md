# String

### String Creation and Memory

???+ info "String Initialization"
    In Java, `String` is a class, and strings are objects. `String` is a **final class**, meaning it cannot be extended. There are two ways to create strings, each with different memory implications:

    === "String Literal (Recommended)"

        ```java
        String str = "Hello";  // Stored in String Constant Pool
        String str2 = "Hello"; // Reuses the same reference
        ```
        ✅ Preferred for better memory efficiency and performance

    === "String Object"

        ```java
        String str = new String("Hello");  // Stored in Heap Memory
        String str2 = new String("Hello"); // Creates a new object in memory
        ```
        ⚠️ Creates new object even if identical string exists

???+ info "String Modification and Garbage Collection"
    Strings are immutable, so modifying a string creates a new object in the **String Constant Pool** (if using literals) or in the heap (if using `new`). The original string remains unchanged. If the original string is no longer referenced, it becomes eligible for garbage collection.

    === "Example"

        ```java
        String str = "Hello";
        str = "World"; // "Hello" becomes eligible for garbage collection if unreferenced
        System.out.println(str); // Outputs: World
        ```

???+ info "StringBuilder and StringBuffer"
    - **StringBuilder:** Faster, not thread-safe.
    - **StringBuffer:** Thread-safe, slower due to synchronization.

    - Using `StringBuilder` or `StringBuffer` is more efficient in loops because it avoids creating multiple immutable `String` objects. Because strings are immutable, every time you modify a string, a new object is created. This can lead to performance issues, especially in loops or when concatenating many strings.
    === "Example"

        ```java
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < 100000; i++) {
            sb.append(i);  // More efficient than using String
        }
        System.out.println(sb.toString()); // Outputs the concatenated string
        ```

???+ info "String Joiner"
    - Joins strings with a delimiter, prefix, and suffix.

    === "Example"

        ```java
        import java.util.StringJoiner;

        StringJoiner joiner = new StringJoiner(", ", "[", "]");
        joiner.add("Apple").add("Banana").add("Orange");
        System.out.println(joiner); // Outputs: [Apple, Banana, Orange]
        ```