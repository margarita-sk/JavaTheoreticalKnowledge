<details>
  <summary>What is thread?</summary>
  In Java, it's a way to execute several tasks simultaneously within one program. It is a single path of execution.
</details>

<details>
  <summary>Tread vs Process</summary>
  
  Process:
- independent program in execution with its own memory space
- runs in its own address space and has its own heap and stack
- isolated from each other, meaning one process cannot directly access the memory or resources of another process
- can run concurrently on separate cores in a multi-core processor, providing true parallelism
- Inter-process communication (IPC) mechanisms like pipes, sockets, shared memory, and message queues are used for communication between processes

  Thread:
- a smaller unit of execution within a process
- threads share the same heap and data segments within a process, but they have their own **stack**
- threads are not isolated from each other - communication between threads is easier and faster
- threads within the same process can run concurrently, and on multi-core processors, they can achieve parallel execution
</details>

<details>
  <summary>Stack vs Heap?</summary>

Stack:
- is used for static memory allocation
- stores primitives, function calls, and references to objects in the heap
- it is thread-safe: each thread has its own stack
- LIFO
- memory is allocated when the method is called and deallocated when it returns
- has limited memory size - StackOverflowError

Heap:
- is used for dynamic memory allocation
- stores objects and arrays
- is not thread-safe - heap is sheared between threads
- memory is allocated when new object/ array is created and is de-allocated when there are no references in the stack to this object and when GC decides
- has larger memory size - OutOfMemoryError
</details>

<details>
  <summary>What is race conditions?</summary>
  It occurs when two or more threads access shared data concurrently and at least one of the threads modifies the data. 
  The result of the program depends on the sequence of the threads' execution, which can lead to inconsistent or incorrect results.
</details>

<details>
  <summary>What is deadlock?</summary>
  Deadlocks in Java occur when two or more threads are permanently blocked, waiting for each other to release resources.

- the resource should be in non-sharable mode
- Thread A holding a resource A is waiting to get resource B held by thread B. Thread B is waiting for resource A.
</details>

<details>
  <summary>What is yield?</summary>
  In Java, yield() is a method in the Thread class. 
  It is used to temporarily pause the execution of the currently running thread and allow other threads of the same priority to execute. 
  Essentially, it suggests to the scheduler that the current thread is willing to yield its current use of the CPU.
</details>

<details>
<summary>What is scheduler?</summary>
The scheduler is typically part of the JVM. Java programs rely on the JVM's scheduler to manage threads and allocate CPU time. 
Java provides mechanisms for developers to influence thread scheduling through methods like Thread.yield(), and synchronization constructs (wait(), notify(), notifyAll()) for thread coordination.
</details>

<details>
  <summary>What is join?</summary>
In Java, the join() method is used to pause the execution of the **current** thread until the thread on which join() is called completes its execution or timeout.
</details>

<details>
  <summary>What is Daemon thread?</summary>

- is used for background non-user tasks like garbage collection, monitoring, and logging
- are managed by the JVM and are automatically terminated when all user threads (non-daemon threads) have finished executing
</details>


<details>
  <summary>How can we create Treads in Java?</summary>

1. By extending Thread class - and then new CustomThread()
2. By implementing the Runnable interface - and then a new Thread(runnable)
(Thread implements Runnable)
</details>

<details>
  <summary>Keywords that help to achieve synchronization in Java</summary>
We can achieve synchronization in Java by using two keywords “synchronized” and “volatile”.

  synchronized:
- for methods and blocks
- **lock-based** concurrent algorithm
- The performance is relatively low
- Variables used inside the synchronized method or block are cached.

volatile:
- variables
- non-blocking algorithm that is more scalable (like atomic)
- they are not cached - each read and write operation on a volatile variable is directly performed to and from the main memory.
</details>

<details>
  <summary>What are atomic operations?</summary>
Operations that are used in concurrent programming, have:
- indivisibility: An atomic operation executes as a single, indivisible unit. It cannot be interrupted or divided into smaller parts by other threads.
- Visibility: Changes made by atomic operations are immediately visible to other threads. This ensures consistent and predictable behavior across threads.
- Atomicity: Either the entire operation completes successfully, or it has no effect at all. There are no intermediate states that can be observed by other threads.
</details>

<details>
  <summary>What is synchronized method?</summary>
  If we are using a synchronized keyword with a method then it will allow only one thread at a time to let its task complete. 
  If multiple threads try to access a method, then the thread that would come first will get the lock and perform its execution. 
  The rest of the thread will wait for the first thread to finish its execution
</details>

<details>
  <summary>What is mutex?</summary>
Special object for synchronizing threads/processes. It can take two states - busy and free. To simplify, a mutex is a boolean variable that takes two values: busy (true) and free (false). 
  When a thread wants to have exclusive ownership of some object, it marks its mutex as occupied, and when it has finished working with it, it marks its mutex as free.
</details>

<details>
  <summary>What is monitor?</summary>
The monitor is a special mechanism - an add-on over a mutex that ensures proper work with it. 
It allows threads to have mutually exclusive access to a section of code or method. Monitors ensure that only one thread at a time can execute the critical section, which helps maintain data consistency and prevents race conditions in shared resources.
</details>

<details>
  <summary>What is semafor?</summary>
  A Semaphore is a synchronization construct that allows multiple threads to access a shared resource concurrently while limiting the number of threads that can access the resource at the same time. 
  Semaphores are used to control access to resources that have a limited capacity, such as a database connection pool, a thread pool, or any resource that can handle a limited number of simultaneous accesses.
</details>

<details>
  <summary>What is the difference between wait() and sleep()?</summary>

- wait - is used for inter-thread communication and synchronization, where a thread voluntarily waits until it is notified by another thread
- sleep - used to pause the execution of a thread for a specified duration without any synchronization or coordination with other threads
</details>

<details>
  <summary>What are Executors?</summary>
  The Concurrency API introduces the concept of an `ExecutorService` as a higher-level replacement for working with threads directly. Executors are capable of running asynchronous tasks and typically manage a pool of threads, so we don’t have to create new threads manually.
Executors have to be stopped explicitly - otherwise, they keep listening for new tasks!
ExecutorService service = Executors.newCachedThreadPool();
var future0 = service.submit(new Runnable(){});
var future1 = service.submit(new Callable());
</details>

<details>
  <summary>Runnable vs Callable?</summary>

- Runnable does not return a result, whereas Callable<V> returns a result of type V.
- Runnable cannot throw checked exceptions directly from run() method, whereas Callable can throw checked exceptions from call() method.
</details>


<details>
  <summary>Future vs Completable future?</summary>
  
  Future:
- represents the result of an asynchronous computation that may not be completed yet
- provides basic operations for checking if the computation is complete, retrieving the result, and canceling the computation.
- get() method of Future blocks until the result is available, which can be problematic if you want to perform other operations while waiting.

  CompletableFuture:
- is an enhanced version of Future that provides a more flexible and powerful programming model for asynchronous computations
- allows chaining and composing multiple asynchronous operations in a fluent and declarative manner.
- supports callback-style completion handlers using methods like thenApply(), thenAccept(), and thenCompose().
</details>

<details>
  <summary>Compare-and-swap</summary>
</details>
