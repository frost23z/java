# Conditionals

### `&` vs `&&` and `|` vs `||`

???+ warning "Key Differences"
    - `&` and `|`: Bitwise operators (for numbers) or Logical operators (for booleans, **no short-circuit**).
    - `&&` and `||`: Logical operators (only for booleans, **with short-circuiting**).

???+ bug "Common Bug"
    Using `&` or `|` instead of `&&` or `||` can cause hidden bugs:
    === "Incorrect Usage with `&`"

        ```java
        int number = 0;
        if (number != 0 & (10 / number) > 1) { // Crashes
            System.out.println("Safe division!");
        }
        ```
        ❌ This crashes with a `Division by zero` error because `&` evaluates both sides.

    === "Correct usage with `&&`"

        ```java
        int number = 0;
        if (number != 0 && (10 / number) > 1) {
            System.out.println("Safe division!");
        }
        ```
        ✅ No error, as `&&` skips the second condition if the first is false.

???+ tip "Rule of Thumb"
    - Use `&&` and `||` for logical conditions (better for safety and performance).
    - Use `&` and `|` only when both sides **must** be evaluated (rare cases).

### Ternary Operator (`? :`)

???+ info "What is the Ternary Operator?"
    The ternary operator is a shorthand for `if-else` statements. It has the syntax:

    ```java
    condition ? value_if_true : value_if_false;
    ```
    Example:

    ```java
    int a = 10, b = 20;
    int max = (a > b) ? a : b; // Assigns the larger value to max
    System.out.println("Max: " + max); // Output: Max: 20
    ```
    

???+ tip "When to Use"
    - Use the ternary operator for simple conditional assignments.
    - Avoid using it for complex logic as it can reduce code readability.

### Enhanced `switch` Expression (Java 12+)

???+ info "What is the Enhanced `switch`?"
    The enhanced `switch` expression simplifies the syntax by removing the need for `break` statements and allows returning values directly. Example:
    === "Traditional `switch`:"

        ```java
        int day = 2;
        String dayName;
        switch (day) {
            case 1:
                dayName = "Monday";
                break;
            case 2:
                dayName = "Tuesday";
                break;
            default:
                dayName = "Unknown";
        }
        System.out.println(dayName); // Output: Tuesday
        ```
    === "Enhanced `switch`:"

        ```java
        int day = 2;
        String dayName = switch (day) {
            case 1 -> "Monday";
            case 2 -> "Tuesday";
            default -> "Unknown";
        };
        System.out.println(dayName); // Output: Tuesday
        ```

        - The `->` operator is used to define the case actions, eliminating the need for `break` statements.

???+ tip "When to Use"
    - Use the enhanced `switch` for cleaner and more concise code.
    - It is especially useful when returning values directly from a `switch`.
