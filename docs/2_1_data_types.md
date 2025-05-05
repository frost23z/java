# Data Types

## Primitive Data Types

| Type      | Size     | Description                                     |
|-----------|----------|-------------------------------------------------|
| `byte`    | 1 byte   | 8-bit signed integer                            |
| `short`   | 2 bytes  | 16-bit signed integer                           |
| `int`     | 4 bytes  | 32-bit signed integer                           |
| `long`    | 8 bytes  | 64-bit signed integer                           |
| `float`   | 4 bytes  | Single-precision 32-bit IEEE 754 floating point |
| `double`  | 8 bytes  | Double-precision 64-bit IEEE 754 floating point |
| `char`    | 2 bytes  | Single 16-bit Unicode character                 |
| `boolean` | 1 bit    | Stores `true` or `false` values                 |

???+ warning "Default Types"
    In Java, the default integer type is `int`, and the default floating-point type is `double`. To use `long` or `float`, you must specify them explicitly. For example:

    ``` java
    long x = 10L;
    float y = 10.5f;
    ```

???+ abstract "Default Values"
    Unlike C/C++, Java initializes variables to default values if not explicitly assigned. Below is a table summarizing the default values for various data types:

    | Type             | Default Value |
    |------------------|---------------|
    | `integer`        | 0             |
    | `floating-point` | 0.0           |
    | `char`           | '\u0000'      |
    | `boolean`        | false         |
    | Reference Types  | null          |

???+ info "Character Data Type"
    The `char` data type is used to store a single 16-bit Unicode character. It can be defined using single quotes, Unicode escape sequences, or decimal values.

    ``` java
    char singleQuoteChar = 'A';     // Represents 'A'
    char unicodeChar = '\u0042';    // Represents 'B'
    char decimalChar = 66;          // Represents 'B'
    ```

???+ warning "Boolean Data Type"
    Only `true` or `false` values are allowed. `[0, 1]` are **not allowed**.

    ``` java
    boolean isTrue = true;          // Represents true
    boolean isFalse = false;        // Represents false
    ```

## Special Features

???+ info "Numeric Literals"
    Numeric literals can be represented in decimal, hexadecimal, octal, or binary formats.

    ``` java
    int decimal = 100;              // Decimal
    int hex = 0x64;                 // Hexadecimal
    int hex = 0x64;                 // Hexadecimal
    int octal = 0144;               // Octal 
    int binary = 0b1100100;         // Binary
    ```

    Use underscores (`_`) in numeric literals for better readability:

    ``` java
    int x = 1_00_000;               // 100000
    ```

## Type Casting

???+ info "Type Casting"
    ### Implicit Casting
    When assigning a smaller data type to a larger data type (no data loss occurs also called **widening conversion**):

    ``` java
    int x = 10;
    long y = x;                     // Implicit casting
    ```
    ### Explicit Casting
    When assigning a larger data type to a smaller data type (may result in data loss):

    ``` java
    long x = 10;
    int y = (int) x;                // Explicit casting
    byte z = (byte) y;              // Further explicit casting
    ```

???+ info "Type Promotion"
    In expressions, Java automatically promotes smaller data types to larger ones to avoid data loss. For example:

    ``` java
    byte a = 10;
    byte b = 30;
    int c = a * b;                  // a and b are promoted to int
    System.out.println(c);          // Output: 300
    ```