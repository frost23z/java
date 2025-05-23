# Threads

## Introduction to Threads

???+ info "What are Threads?"
    - Threads are lightweight sub-processes enabling concurrent task execution.
    - Java supports multithreading via the `Thread` class and `Runnable` interface.

    === "Key Points"
    - Threads share memory but have individual stacks.
    - States: `NEW`, `RUNNABLE`, `BLOCKED`, `WAITING`, `TIMED_WAITING`, `TERMINATED`.

## Creating Threads

???+ info "Ways to Create Threads"
    - Extend `Thread` class or implement `Runnable` interface.

    === "Extending `Thread` Class"

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

    === "Implementing `Runnable` Interface"

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

## Thread Lifecycle

???+ info "Thread Lifecycle"
    - A thread in Java goes through the following states:
        1. **NEW**: The thread is created but not yet started.
        2. **RUNNABLE**: The thread is ready to run and waiting for CPU time.
        3. **RUNNING**: The thread is executing.
        4. **BLOCKED/WAITING/TIMED_WAITING**: The thread is waiting for a resource or signal.
        5. **TERMINATED**: The thread has completed execution.

    === "Lifecycle Example"

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
                System.out.println("State: " + thread.getState()); // NEW
                thread.start();
                System.out.println("State: " + thread.getState()); // RUNNABLE

                try {
                    thread.join(); // Wait for the thread to finish
                } catch (InterruptedException e) {
                    System.out.println("Main thread interrupted: " + e.getMessage());
                }
                System.out.println("State: " + thread.getState()); // TERMINATED
            }
        }
        ```

## Thread Methods

???+ info "Common Thread Methods"
    - `start()`: Starts the thread.
    - `run()`: Contains the code to be executed by the thread.
    - `sleep(milliseconds)`: Pauses the thread for a specified time.
    - `join()`: Waits for a thread to finish execution.
    - `isAlive()`: Checks if the thread is still running.
    - `setPriority(priority)`: Sets the thread's priority.
    - `getPriority()`: Gets the thread's priority.

    === "Example: `sleep` and `join`"

        ```java
        class MyThread extends Thread {
            @Override
            public void run() {
                for (int i = 1; i <= 5; i++) {
                    System.out.println("Thread: " + i);
                    try {
                        Thread.sleep(500); // Pause for 500ms
                    } catch (InterruptedException e) {
                        System.out.println("Interrupted: " + e.getMessage());
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
                    System.out.println("Main interrupted: " + e.getMessage());
                }
                System.out.println("Main finished.");
            }
        }
        ```

## Synchronization

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
                    for (int i = 0; i < 1000; i++) counter.increment();
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) counter.increment();
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // Outputs: 2000
            }
        }
        ```

## Deadlock

???+ info "Deadlock"
    - Occurs when threads wait indefinitely for each other to release resources.

    === "Example"

        ```java
        class Resource {
            void methodA(Resource other) {
                synchronized (this) {
                    System.out.println(Thread.currentThread().getName() + " locked this");
                    synchronized (other) {
                        System.out.println(Thread.currentThread().getName() + " locked other");
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
    - Use consistent resource acquisition order.
    - Use `tryLock` from `java.util.concurrent.locks`.

## Thread Pool

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

## Concurrency Utilities

???+ info "Concurrency Utilities"
    - Java provides utilities in the `java.util.concurrent` package for advanced multithreading and concurrency control.

    === "Common Utilities"
    - `ReentrantLock`: A lock with more control than `synchronized`.
    - `CountDownLatch`: A synchronization aid that allows threads to wait for a set of operations to complete.
    - `CyclicBarrier`: A synchronization aid that allows threads to wait for each other at a common barrier point.
    - `Semaphore`: A counting semaphore for controlling access to a resource.
    - `ExecutorService`: A framework for managing thread pools.

    === "Example: `CountDownLatch`"

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

## Race Condition

???+ info "What is a Race Condition?"
    - A race condition occurs when two or more threads access shared data and try to modify it simultaneously.
    - The final outcome depends on the order in which the threads execute, leading to unpredictable behavior.

    === "Example"

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
                    for (int i = 0; i < 1000; i++) counter.increment();
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) counter.increment();
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // May not be 2000 due to race condition
            }
        }
        ```

    === "Prevention"
    - Use `synchronized` or thread-safe classes like `AtomicInteger`.

    === "Example: `AtomicInteger`"

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
                    for (int i = 0; i < 1000; i++) counter.increment();
                });

                Thread t2 = new Thread(() -> {
                    for (int i = 0; i < 1000; i++) counter.increment();
                });

                t1.start();
                t2.start();

                try {
                    t1.join();
                    t2.join();
                } catch (InterruptedException e) {
                    System.out.println("Interrupted: " + e.getMessage());
                }

                System.out.println("Final count: " + counter.getCount()); // Outputs: 2000
            }
        }
        ```