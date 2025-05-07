# Enum

???+ info "Enum"
    - An **Enum** is a special data type that represents a group of constants.
    - Enums are used to define a fixed set of related constants, such as days of the week, directions, or states.
    - Key characteristics:
        - Enums are implicitly `final` and `static`.
        - Enum constants are `public`, `static`, and `final` by default.
        - Enums can have fields, methods, and constructors.
        - Enums can implement interfaces but cannot extend classes (as they implicitly extend `java.lang.Enum`).

    === "Basic Example"

        ```java
        enum Day {
            MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
        }

        public class Main {
            public static void main(String[] args) {
                Day today = Day.MONDAY;
                System.out.println("Today is: " + today); // Outputs: Today is: MONDAY

                for (Day day : Day.values()) {
                    System.out.println(day);
                }
            }
        }
        ```

    === "With Fields and Methods"
        - Enums can have fields, methods, and constructors to associate additional data with each constant.

        ```java
        enum Planet {
            EARTH(5.97e+24, 6.371e6);

            private final double mass;   // in kilograms
            private final double radius; // in meters

            Planet(double mass, double radius) {
                this.mass = mass;
                this.radius = radius;
            }

            public double surfaceGravity() {
                final double G = 6.67430e-11; // Gravitational constant
                return G * mass / (radius * radius);
            }
        }

        public class Main {
            public static void main(String[] args) {
                System.out.println("Earth's Gravity: " + Planet.EARTH.surfaceGravity());
            }
        }
        ```

    === "With Switch Statement"
        - Enums are often used with `switch` statements for better readability and control.

        ```java
        enum TrafficLight {
            RED, YELLOW, GREEN
        }

        public class Main {
            public static void main(String[] args) {
                TrafficLight signal = TrafficLight.RED;

                switch (signal) {
                    case RED -> System.out.println("Stop!");
                    case YELLOW -> System.out.println("Get Ready!");
                    case GREEN -> System.out.println("Go!");
                }
            }
        }
        ```

    === "Implementing an Interface"
        - Enums can implement interfaces to define behavior for each constant.

        ```java
        interface Operation {
            double apply(double x, double y);
        }

        enum Calculator implements Operation {
            ADD {
                @Override
                public double apply(double x, double y) {
                    return x + y;
                }
            },
            MULTIPLY {
                @Override
                public double apply(double x, double y) {
                    return x * y;
                }
            };
        }

        public class Main {
            public static void main(String[] args) {
                System.out.println(Calculator.ADD.apply(10, 5)); // Outputs: 15.0
            }
        }
        ```