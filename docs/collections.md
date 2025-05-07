# Collections

## Introduction to Collections

???+ info "What is the Java Collections Framework?"
    - The Java Collections Framework (JCF) is a set of classes and interfaces that implement commonly reusable collection data structures.
    - It provides a unified architecture for storing, retrieving, and manipulating data.
    - **Key benefits:**
        - Reduces programming effort by providing ready-to-use data structures.
        - Improves performance with efficient algorithms.
        - Increases code reusability and maintainability.
    - **Key Interfaces**:
        - **Collection**: Root interface for most collections.
        - **List**: Ordered, allows duplicates (e.g., `ArrayList`, `LinkedList`).
        - **Set**: No duplicates (e.g., `HashSet`, `TreeSet`).
        - **Queue**: Holds elements for processing (e.g., `PriorityQueue`).
        - **Map**: Key-value pairs (e.g., `HashMap`, `TreeMap`).

## List Interface

???+ info "List Interface"
    - Ordered collection allowing duplicates.
    - **Implementations**:
        - `ArrayList`: Resizable array.
        - `LinkedList`: Doubly-linked list.
        - `Vector`: Synchronized resizable array (legacy).

    === "Example: Using `ArrayList`"

        ```java
        import java.util.ArrayList;

        public class Main {
            public static void main(String[] args) {
                ArrayList<String> list = new ArrayList<>();
                list.add("Apple");
                list.add("Banana");
                list.add("Cherry");

                System.out.println("List: " + list); // Outputs: [Apple, Banana, Cherry]

                list.remove("Banana");
                System.out.println("After removal: " + list); // Outputs: [Apple, Cherry]

                System.out.println("Element at index 1: " + list.get(1)); // Outputs: Cherry
            }
        }
        ```

## Set Interface

???+ info "Set Interface"
    - No duplicate elements.
    - **Implementations**:
        - `HashSet`: Unordered.
        - `TreeSet`: Ordered.
        - `LinkedHashSet`: Maintains insertion order.

    === "Example: Using `HashSet`"

        ```java
        import java.util.HashSet;

        public class Main {
            public static void main(String[] args) {
                HashSet<String> set = new HashSet<>();
                set.add("Apple");
                set.add("Banana");
                set.add("Apple");

                System.out.println("Set: " + set); // Outputs: [Apple, Banana]
            }
        }
        ```

## Map Interface

???+ info "Map Interface"
    - Key-value pairs.
    - **Implementations**:
        - `HashMap`: Unordered.
        - `TreeMap`: Ordered.
        - `LinkedHashMap`: Maintains insertion order.

    === "Example: Using `HashMap`"

        ```java
        import java.util.HashMap;

        public class Main {
            public static void main(String[] args) {
                HashMap<String, Integer> map = new HashMap<>();
                map.put("Apple", 1);
                map.put("Banana", 2);
                map.put("Cherry", 3);

                System.out.println("Map: " + map); // Outputs: {Apple=1, Banana=2, Cherry=3}

                map.remove("Banana");
                System.out.println("After removal: " + map); // Outputs: {Apple=1, Cherry=3}

                System.out.println("Value for 'Apple': " + map.get("Apple")); // Outputs: 1
            }
        }
        ```

## Queue Interface

???+ info "Queue Interface"
    - Holds elements for processing.
    - **Implementations**:
        - `PriorityQueue`: Priority-based.
        - `LinkedList`: Can act as a queue.

    === "Example: Using `PriorityQueue`"

        ```java
        import java.util.PriorityQueue;

        public class Main {
            public static void main(String[] args) {
                PriorityQueue<Integer> queue = new PriorityQueue<>();
                queue.add(10);
                queue.add(5);
                queue.add(20);

                System.out.println("Queue: " + queue); // Outputs: [5, 10, 20]

                System.out.println("Polled element: " + queue.poll()); // Outputs: 5
                System.out.println("Queue after poll: " + queue); // Outputs: [10, 20]
            }
        }
        ```

## Iterator

???+ info "Iterator"
    - Traverses collection elements.
    - **Methods**:
        - `hasNext()`: Checks for more elements.
        - `next()`: Retrieves the next element.
        - `remove()`: Removes the last returned element.

    === "Example: Using `Iterator`"

        ```java
        import java.util.ArrayList;
        import java.util.Iterator;

        public class Main {
            public static void main(String[] args) {
                ArrayList<String> list = new ArrayList<>();
                list.add("Apple");
                list.add("Banana");
                list.add("Cherry");

                Iterator<String> iterator = list.iterator();
                while (iterator.hasNext()) {
                    System.out.println(iterator.next());
                }
            }
        }
        ```

## Comparable and Comparator

???+ info "Comparable and Comparator"
    - Used for sorting collections.

    === "Using `Comparable`"
        - The `Comparable` interface is used to define the natural ordering of objects.
        - It requires implementing the `compareTo()` method.

        ```java
        import java.util.ArrayList;
        import java.util.Collections;

        class Student implements Comparable<Student> {
            String name;
            int age;

            public Student(String name, int age) {
                this.name = name;
                this.age = age;
            }

            @Override
            public int compareTo(Student other) {
                return this.age - other.age; // Sort by age
            }

            @Override
            public String toString() {
                return name + " (" + age + ")";
            }
        }

        public class Main {
            public static void main(String[] args) {
                ArrayList<Student> students = new ArrayList<>();
                students.add(new Student("Alice", 22));
                students.add(new Student("Bob", 20));
                students.add(new Student("Charlie", 25));

                Collections.sort(students);
                System.out.println(students); // Outputs: [Bob (20), Alice (22), Charlie (25)]
            }
        }
        ```

    === "Using `Comparator`"
        - The `Comparator` interface is used to define custom sorting logic.
        - It requires implementing the `compare()` method.

        ```java
        import java.util.ArrayList;
        import java.util.Collections;
        import java.util.Comparator;

        class Student {
            String name;
            int age;

            public Student(String name, int age) {
                this.name = name;
                this.age = age;
            }

            @Override
            public String toString() {
                return name + " (" + age + ")";
            }
        }

        public class Main {
            public static void main(String[] args) {
                ArrayList<Student> students = new ArrayList<>();
                students.add(new Student("Alice", 22));
                students.add(new Student("Bob", 20));
                students.add(new Student("Charlie", 25));

                Collections.sort(students, new Comparator<Student>() {
                    @Override
                    public int compare(Student s1, Student s2) {
                        return s1.name.compareTo(s2.name);
                    }
                });

                System.out.println(students); // Outputs: [Alice (22), Bob (20), Charlie (25)]
            }
        }
        ```
