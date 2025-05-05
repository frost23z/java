# Threads

### Introduction to Threads

???+ info "What are Threads?"
    - A thread is a lightweight sub-process, the smallest unit of processing.
    - Threads allow a program to perform multiple tasks concurrently.
    - Java provides built-in support for multithreading through the `java.lang.Thread` class and the `Runnable` interface.

    === "Key Points"
    - Threads share the same memory space but have their own stack.
    - Multithreading improves performance by utilizing CPU resources efficiently.
    - Threads can be in one of several states: `NEW`, `RUNNABLE`, `BLOCKED`, `WAITING`, `TIMED_WAITING`, or `TERMINATED`.

### Creating Threads

???+ info "Ways to Create Threads"
    - There are two main ways to create threads in Java:
        1. By extending the `Thread` class.
        2. By implementing the `Runnable` interface.

    === "Extending the `Thread` Class"
        ```java
        class MyThread extends Thread {
            @Override
            public void run() {
                System.out.println("Thread is running...");
            }
        }

        public class Main {
            public static void main(String[] args) {
                MyThread thread = new MyThread();
                thread.start(); // Starts the thread
            }
        }
        ```

    === "Implementing the `Runnable` Interface"
        ```java
        class MyRunnable implements Runnable {
            @Override
            public void run() {
                System.out.println("Thread is running...");
            }
        }

        public class Main {
            public static void main(String[] args) {
                Thread thread = new Thread(new MyRunnable());
                thread.start(); // Starts the thread
            }
        }
        ```

### Thread Lifecycle

???+ info "Thread Lifecycle"
    - A thread in Java goes through the following states:
        1. **NEW**: The thread is created but not yet started.
        2. **RUNNABLE**: The thread is ready to run and waiting for CPU time.
        3. **RUNNING**: The thread is executing.
        4. **BLOCKED/WAITING/TIMED_WAITING**: The thread is waiting for a resource or signal.
        5. **TERMINATED**: The thread has completed execution.

    === "Thread Lifecycle Example"
        ```java
        class MyThread extends Thread {
            @Override
            public void run() {
                System.out.println("Thread is running...");
            }
        }

        public class Main {
            public static void main(String[] args) {
                MyThread thread = new MyThread();
                System.out.println("Thread state: " + thread.getState()); // NEW
                thread.start();
                System.out.println("Thread state: " + thread.getState()); // RUNNABLE
            }
        }
        ```

### Thread Methods

???+ info "Common Thread Methods"
    - `start()`: Starts the thread.
    - `run()`: Contains the code to be executed by the thread.
    - `sleep(milliseconds)`: Pauses the thread for a specified time.
    - `join()`: Waits for a thread to finish execution.
    - `isAlive()`: Checks if the thread is still running.
    - `setPriority(priority)`: Sets the thread's priority.
    - `getPriority()`: Gets the thread's priority.

    === "Example: Using `sleep` and `join`"
        ```java
        class MyThread extends Thread {
            @Override
            public void run() {
                for (int i = 1; i <= 5; i++) {
                    System.out.println("Thread: " + i);
                    try {
                        Thread.sleep(500); // Pause for 500ms
                    } catch (InterruptedException e) {
                        System.out.println("Thread interrupted: " + e.getMessage());
                    }
                }
            }
        }

        public class Main {
            public static void main(String[] args) {
                MyThread thread = new MyThread();
                thread.start();
                try {
                    thread.join(); // Wait for the thread to finish
                } catch (InterruptedException e) {
                    System.out.println("Main thread interrupted: " + e.getMessage());
                }
                System.out.println("Main thread finished.");
            }
        }
        ```

### Synchronization

???+ info "Thread Synchronization"
    - Synchronization is used to control access to shared resources in multithreaded environments.
    - It prevents thread interference and ensures data consistency.

    === "Using `synchronized` Keyword"
        ```java
        class Counter {
            private int count = 0;

            public synchronized void increment() {
                count++;
            }

            public int getCount() {
                return count;
            }
        }

        public class Main {
            public static void main(String[] args) {
                Counter counter = new Counter();

                Thread t1 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Thread interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // Outputs: 2000
            }
        }
        ```

### Deadlock

???+ info "Deadlock"
    - A deadlock occurs when two or more threads are waiting for each other to release resources, causing a cycle of dependency and halting execution.

    === "Example of Deadlock"
        ```java
        class Resource {
            void methodA(Resource other) {
                synchronized (this) {
                    System.out.println(Thread.currentThread().getName() + " locked this resource");
                    synchronized (other) {
                        System.out.println(Thread.currentThread().getName() + " locked other resource");
                    }
                }
            }
        }

        public class Main {
            public static void main(String[] args) {
                Resource r1 = new Resource();
                Resource r2 = new Resource();

                Thread t1 = new Thread(() -> r1.methodA(r2), "Thread-1");
                Thread t2 = new Thread(() -> r2.methodA(r1), "Thread-2");

                t1.start();
                t2.start();
            }
        }
        ```

    === "Avoiding Deadlock"
    - Use a consistent order of resource acquisition.
    - Use `tryLock` from `java.util.concurrent.locks` to avoid indefinite blocking.

### Thread Pool

???+ info "Thread Pool"
    - A thread pool is a collection of pre-created threads that can be reused for executing tasks.
    - It improves performance by reducing the overhead of thread creation and destruction.

    === "Using `ExecutorService`"
        ```java
        import java.util.concurrent.ExecutorService;
        import java.util.concurrent.Executors;

        public class Main {
            public static void main(String[] args) {
                ExecutorService executor = Executors.newFixedThreadPool(3);

                for (int i = 1; i <= 5; i++) {
                    int taskId = i;
                    executor.execute(() -> {
                        System.out.println("Task " + taskId + " is running on " + Thread.currentThread().getName());
                    });
                }

                executor.shutdown(); // Shut down the executor
            }
        }
        ```

### Concurrency Utilities

???+ info "Concurrency Utilities"
    - Java provides utilities in the `java.util.concurrent` package for advanced multithreading and concurrency control.

    === "Common Utilities"
    - `ReentrantLock`: A lock with more control than `synchronized`.
    - `CountDownLatch`: A synchronization aid that allows threads to wait for a set of operations to complete.
    - `CyclicBarrier`: A synchronization aid that allows threads to wait for each other at a common barrier point.
    - `Semaphore`: A counting semaphore for controlling access to a resource.
    - `ExecutorService`: A framework for managing thread pools.

    === "Example: Using `CountDownLatch`"
        ```java
        import java.util.concurrent.CountDownLatch;

        public class Main {
            public static void main(String[] args) throws InterruptedException {
                CountDownLatch latch = new CountDownLatch(3);

                Runnable task = () -> {
                    System.out.println(Thread.currentThread().getName() + " completed.");
                    latch.countDown(); // Decrement the latch count
                };

                Thread t1 = new Thread(task, "Thread-1");
                Thread t2 = new Thread(task, "Thread-2");
                Thread t3 = new Thread(task, "Thread-3");

                t1.start();
                t2.start();
                t3.start();

                latch.await(); // Wait for all threads to complete
                System.out.println("All threads completed.");
            }
        }
        ```

### Race Condition

???+ info "What is a Race Condition?"
    - A race condition occurs when two or more threads access shared data and try to modify it simultaneously.
    - The final outcome depends on the order in which the threads execute, leading to unpredictable behavior.

    === "Example of Race Condition"
        ```java
        class Counter {
            private int count = 0;

            public void increment() {
                count++;
            }

            public int getCount() {
                return count;
            }
        }

        public class Main {
            public static void main(String[] args) {
                Counter counter = new Counter();

                Thread t1 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Thread interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // May not be 2000 due to race condition
            }
        }
        ```

    === "How to Prevent Race Conditions"
    - Use synchronization to ensure that only one thread can access the critical section at a time.
    - Use thread-safe classes like `AtomicInteger` or `ConcurrentHashMap`.

    === "Example: Using Synchronization"
        ```java
        class Counter {
            private int count = 0;

            public synchronized void increment() {
                count++;
            }

            public int getCount() {
                return count;
            }
        }

        public class Main {
            public static void main(String[] args) {
                Counter counter = new Counter();

                Thread t1 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Thread interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // Outputs: 2000
            }
        }
        ```

    === "Using Atomic Variables"
        ```java
        import java.util.concurrent.atomic.AtomicInteger;

        class Counter {
            private AtomicInteger count = new AtomicInteger(0);

            public void increment() {
                count.incrementAndGet();
            }

            public int getCount() {
                return count.get();
            }
        }

        public class Main {
            public static void main(String[] args) {
                Counter counter = new Counter();

                Thread t1 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) {
                        counter.increment();
                    }
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Thread interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // Outputs: 2000
            }
        }
        ```
