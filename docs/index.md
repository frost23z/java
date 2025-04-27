# Introduction

Java is a widely-used, platform-independent programming language known for its simplicity and power. As an object-oriented language similar to C++ and C#, it offers clear structure and code reusability. Its open-source nature, robust security, and extensive community support have secured its position as a leading programming language in the industry.

### JVM, JRE, JDK

???+ note
    Java bytecode is platform independent, but JVM and JRE are platform dependent, requiring specific implementations for each operating system.

| Component | Description | Contains |
|-----------|-------------|-----------|
| JVM | Executes Java bytecode | - Java interpreter<br>- JIT compiler<br>- Garbage collector |
| JRE | Runs Java applications | - JVM<br>- Core classes<br>- Supporting files |
| JDK | Complete development package | - JRE<br>- Development tools<br>- Documentation |

### Run Java Program

???+ info "Compile and Run"
    The `javac` command requires the file name (with `.java` extension) to match the public class name in the file. The `java` command uses the class name (without extension) to execute the program. For example:
    ```bash
    javac HelloWorld.java
    java HelloWorld
    ```

???+ note "Main Method"
    The `main` method is the entry point of a Java program. It must be declared as `public`, `static`, and return `void`. The method signature is:
    ```java
    public static void main(String[] args) {
        // Code goes here
    }
    ```
    The `args` parameter is an array of strings that can be used to pass command-line arguments to the program.