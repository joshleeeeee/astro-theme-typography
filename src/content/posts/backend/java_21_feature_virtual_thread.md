---
title: Java21新特性-虚拟线程
categories:
  - 后端
pubDate: 2025-02-05
---

虚拟线程是一种轻量级线程，旨在简化高吞吐量并发应用程序的编写、维护和调试工作。

线程是能够被调度的最小处理单元。它可以与其他线程并发运行，并且基本上独立于其他线程。线程是`java.lang.Thread`类的实例。线程分为两种类型：**平台线程**和**虚拟线程**。

### 什么是平台线程？

平台线程是操作系统（OS）线程的一个轻量级封装。平台线程在其底层的操作系统线程上运行Java代码，并且在平台线程的整个生命周期内，它会占用该操作系统线程。因此，可用的平台线程数量受限于操作系统线程的数量。

平台线程通常具有较大的线程栈和其他由操作系统维护的资源。它们适合运行各种类型的任务，但可能是一种有限的资源。

### 什么是虚拟线程？

虚拟线程（Virtual Thread）是 Java 中的一种线程类型，它是 `java.lang.Thread` 的实例，但与平台线程（Platform Thread）不同，虚拟线程并不绑定到特定的操作系统线程。虚拟线程仍然在操作系统线程上运行代码，但当虚拟线程中的代码调用阻塞的 I/O 操作时，Java 运行时会挂起该虚拟线程，直到它可以恢复。此时，与该虚拟线程关联的操作系统线程可以自由地为其他虚拟线程执行任务。

虚拟线程的实现方式类似于虚拟内存。操作系统通过将较大的虚拟地址空间映射到有限的物理内存来模拟大量内存。类似地，Java 运行时通过将大量虚拟线程映射到少量操作系统线程来模拟大量线程。

与平台线程不同，虚拟线程通常具有较浅的调用栈，可能只执行一个 HTTP 客户端调用或一个 JDBC 查询。尽管虚拟线程支持线程局部变量（Thread-Local Variables）和可继承的线程局部变量，但由于单个 JVM 可能支持数百万个虚拟线程，因此在使用这些变量时需要谨慎考虑。

虚拟线程适合运行大部分时间处于阻塞状态的任务，通常是等待 I/O 操作完成的任务。然而，它们并不适合长时间运行的 CPU 密集型操作。

### 为什么用虚拟线程？

在高吞吐量的并发应用程序中，尤其是那些包含大量并发任务且这些任务大部分时间都在等待的场景下，使用虚拟线程非常合适。服务器应用程序就是高吞吐量应用的典型例子，因为它们通常需要处理许多客户端请求，而这些请求往往涉及阻塞的 I/O 操作（例如获取资源）。

虚拟线程并不是更快的线程，它们运行代码的速度与平台线程相同。虚拟线程的存在是为了提供**规模（更高的吞吐量）**，而不是**速度（更低的延迟）**。通过更高效地管理大量并发任务，虚拟线程可以显著提升应用程序的整体吞吐量。

### 创建和运行虚拟线程

Java 提供了多种方式来创建平台线程和虚拟线程。`Thread` 和 `Thread.Builder` API 可以用于创建线程，而 `java.util.concurrent.Executors` 类也提供了方法来创建 `ExecutorService`，该服务会为每个任务启动一个新的虚拟线程。

#### 1. 使用 `Thread` 类和 `Thread.Builder` 接口创建虚拟线程

通过调用 `Thread.ofVirtual()` 方法，可以创建一个 `Thread.Builder` 实例，用于创建虚拟线程。

**示例 1**：创建并启动一个虚拟线程，打印一条消息。使用 `join()` 方法等待虚拟线程结束。

```java
Thread thread = Thread.ofVirtual().start(() -> System.out.println("Hello"));
thread.join();
```

**示例 2**：使用 `Thread.Builder` 接口创建一个名为 `MyThread` 的虚拟线程。

```java
Thread.Builder builder = Thread.ofVirtual().name("MyThread");
Runnable task = () -> {
    System.out.println("Running thread");
};
Thread t = builder.start(task);
System.out.println("Thread t name: " + t.getName());
t.join();
```

**示例 3**：创建并启动两个虚拟线程，线程名分别为 `worker-0` 和 `worker-1`。

```java
Thread.Builder builder = Thread.ofVirtual().name("worker-", 0);
Runnable task = () -> {
    System.out.println("Thread ID: " + Thread.currentThread().threadId());
};

Thread t1 = builder.start(task);   
t1.join();
System.out.println(t1.getName() + " terminated");

Thread t2 = builder.start(task);   
t2.join();  
System.out.println(t2.getName() + " terminated");
```

输出结果类似于：

```
Thread ID: 21
worker-0 terminated
Thread ID: 24
worker-1 terminated
```

#### 2. 使用 `Executors.newVirtualThreadPerTaskExecutor()` 方法创建和运行虚拟线程

`Executors` 允许你将线程的管理和创建与应用程序的其他部分分离。

**示例**：使用 `Executors.newVirtualThreadPerTaskExecutor()` 方法创建一个 `ExecutorService`。每次调用 `ExecutorService.submit(Runnable)` 时，都会创建一个新的虚拟线程来执行任务。

```java
try (ExecutorService myExecutor = Executors.newVirtualThreadPerTaskExecutor()) {
    Future<?> future = myExecutor.submit(() -> System.out.println("Running thread"));
    future.get();
    System.out.println("Task completed");
}
```

#### 3. 多线程客户端-服务器示例

以下示例包含两个类：`EchoServer` 和 `EchoClient`。`EchoServer` 是一个服务器程序，监听端口并为每个连接启动一个新的虚拟线程。`EchoClient` 是一个客户端程序，连接到服务器并发送从命令行输入的消息。

**EchoServer**：

```java
public class EchoServer {
    public static void main(String[] args) throws IOException {
        if (args.length != 1) {
            System.err.println("Usage: java EchoServer <port>");
            System.exit(1);
        }
         
        int portNumber = Integer.parseInt(args[0]);
        try (ServerSocket serverSocket = new ServerSocket(portNumber)) {                
            while (true) {
                Socket clientSocket = serverSocket.accept();
                Thread.ofVirtual().start(() -> {
                    try (
                        PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);
                        BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
                    ) {
                        String inputLine;
                        while ((inputLine = in.readLine()) != null) {
                            System.out.println(inputLine);
                            out.println(inputLine);
                        }
                    } catch (IOException e) { 
                        e.printStackTrace();
                    }
                });
            }
        } catch (IOException e) {
            System.out.println("Exception caught when trying to listen on port " + portNumber + " or listening for a connection");
            System.out.println(e.getMessage());
        }
    }
}
```

**EchoClient**：

```java
public class EchoClient {
    public static void main(String[] args) throws IOException {
        if (args.length != 2) {
            System.err.println("Usage: java EchoClient <hostname> <port>");
            System.exit(1);
        }
        String hostName = args[0];
        int portNumber = Integer.parseInt(args[1]);
        try (
            Socket echoSocket = new Socket(hostName, portNumber);
            PrintWriter out = new PrintWriter(echoSocket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(new InputStreamReader(echoSocket.getInputStream()));
        ) {
            BufferedReader stdIn = new BufferedReader(new InputStreamReader(System.in));
            String userInput;
            while ((userInput = stdIn.readLine()) != null) {
                out.println(userInput);
                System.out.println("echo: " + in.readLine());
                if (userInput.equals("bye")) break;
            }
        } catch (UnknownHostException e) {
            System.err.println("Don't know about host " + hostName);
            System.exit(1);
        } catch (IOException e) {
            System.err.println("Couldn't get I/O for the connection to " + hostName);
            System.exit(1);
        } 
    }
}
```

### 虚拟线程的调度与固定

操作系统负责调度平台线程（platform thread）的运行，而Java运行时则负责调度虚拟线程（virtual thread）的运行。当Java运行时调度一个虚拟线程时，会将其分配或挂载到一个平台线程上，然后由操作系统像往常一样调度该平台线程。这个平台线程被称为“载体线程”（carrier）。在运行一些代码后，虚拟线程可以从其载体线程上卸载。这种情况通常发生在虚拟线程执行阻塞I/O操作时。卸载后，载体线程变为空闲状态，Java运行时调度器可以将另一个虚拟线程挂载到该载体线程上。

然而，在某些情况下，虚拟线程会被固定（pinned）到其载体线程上，无法在阻塞操作期间卸载。虚拟线程被固定的情况包括：

1. 虚拟线程在同步代码块（synchronized block）或同步方法中运行代码。
2. 虚拟线程运行本地方法（native method）或外部函数（foreign function，参见Foreign Function and Memory API）。

固定并不会导致应用程序出错，但可能会影响其扩展性。为了避免频繁和长时间的固定，可以尝试以下优化：
- 修改频繁运行的同步代码块或方法。
- 使用`java.util.concurrent.locks.ReentrantLock`来保护可能长时间运行的I/O操作。

这样可以减少虚拟线程被固定的情况，从而提升应用程序的并发性能。

### 虚拟线程：使用指南

虚拟线程是由 Java 运行时（而非操作系统）实现的 Java 线程。与传统线程（称为平台线程）的主要区别在于，虚拟线程可以轻松地在同一个 Java 进程中运行大量活动线程，甚至可以达到数百万个。虚拟线程的强大之处在于其数量：它们可以更高效地运行以“每个请求一个线程”风格编写的服务器应用程序，使服务器能够同时处理更多请求，从而提高吞吐量并减少硬件资源的浪费。

由于虚拟线程是 `java.lang.Thread` 的实现，并且遵循自 Java SE 1.0 以来定义的相同规则，开发者无需学习新概念即可使用它们。然而，多年来平台线程（Java 中唯一的线程实现）无法大量创建，导致开发者形成了应对其高成本的编程习惯。这些习惯在虚拟线程中适得其反，必须摒弃。此外，虚拟线程与平台线程在成本上的巨大差异，要求开发者重新思考线程的使用方式。

本指南旨在提供入门级指导，帮助开发者更好地使用虚拟线程。

---

#### 编写简单的同步代码，用阻塞 I/O API

虚拟线程可以显著提高以“每个请求一个线程”风格编写的服务器的吞吐量（而非延迟）。在这种风格中，服务器为每个传入请求分配一个线程，处理整个请求的生命周期。由于虚拟线程数量庞大，阻塞它们是低成本的，因此鼓励编写同步风格的代码并使用阻塞 I/O API。

例如，以下异步风格的代码不会从虚拟线程中获益：

```java
CompletableFuture.supplyAsync(info::getUrl, pool)
   .thenCompose(url -> getBodyAsync(url, HttpResponse.BodyHandlers.ofString()))
   .thenApply(info::findImage)
   .thenCompose(url -> getBodyAsync(url, HttpResponse.BodyHandlers.ofByteArray()))
   .thenApply(info::setImageData)
   .thenAccept(this::process)
   .exceptionally(t -> { t.printStackTrace(); return null; });
```

而以下同步风格的代码会显著受益：

```java
try {
   String page = getBody(info.getUrl(), HttpResponse.BodyHandlers.ofString());
   String imageUrl = info.findImage(page);
   byte[] data = getBody(imageUrl, HttpResponse.BodyHandlers.ofByteArray());   
   info.setImageData(data);
   process(info);
} catch (Exception ex) {
   t.printStackTrace();
}
```

这种代码更易于调试、分析和观察线程转储。要观察虚拟线程，可以使用 `jcmd` 命令生成线程转储：

```bash
jcmd <pid> Thread.dump_to_file -format=json <file>
```

---

#### 将每个并发任务表示为虚拟线程；不要池化虚拟线程

虚拟线程的行为与平台线程相同，但它们不应代表相同的程序概念。平台线程稀缺，需要池化管理；而虚拟线程数量庞大，每个线程应代表一个任务，而非共享资源。

不要使用共享线程池，例如：

```java
Future<ResultA> f1 = sharedThreadPoolExecutor.submit(task1);
Future<ResultB> f2 = sharedThreadPoolExecutor.submit(task2);
```

而应使用虚拟线程执行器：

```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
   Future<ResultA> f1 = executor.submit(task1);
   Future<ResultB> f2 = executor.submit(task2);
}
```

每个任务都会创建一个新的虚拟线程，且 `ExecutorService` 是轻量级的，可以通过 `try-with-resources` 自动关闭。

#### 3. 使用信号量限制并发

如果需要限制某些操作的并发性（例如外部服务只能处理 10 个并发请求），不要使用线程池，而应使用 `Semaphore`：

```java
Semaphore sem = new Semaphore(10);
...
Result foo() {
    sem.acquire();
    try {
        return callLimitedService();
    } finally {
        sem.release();
    }
}
```

信号量会限制并发访问，而不会浪费虚拟线程资源。

#### 4. 不要在 ThreadLocal 中缓存昂贵的可重用对象

虚拟线程支持 `ThreadLocal`，但不应将其用于缓存昂贵的可重用对象（如 `SimpleDateFormat`）。因为虚拟线程不会被池化或重用，每次调用都会创建新实例，导致内存浪费。建议使用线程安全的替代方案（如 `DateTimeFormatter`）。

#### 5. 避免长时间和频繁的“固定”操作

在Java虚拟线程的实现中，存在一个当前限制：当在`synchronized`块或方法内执行阻塞操作时，JDK的虚拟线程调度器会阻塞一个宝贵的操作系统线程，而如果阻塞操作在`synchronized`块或方法外执行，则不会发生这种情况。这种现象被称为“**线程固定（Pinning）**”。如果阻塞操作既耗时又频繁，线程固定可能会对服务器的吞吐量产生负面影响。但对于短暂的（如内存操作）或不频繁的操作，使用`synchronized`块或方法不会有不良影响。

为了检测可能有害的线程固定情况，**JDK Flight Recorder (JFR)** 会在阻塞操作被固定时发出`jdk.VirtualThreadPinned`事件（默认情况下，当操作超过20毫秒时启用）。此外，你可以使用系统属性`jdk.tracePinnedThreads`在线程被固定时打印堆栈跟踪：

- 使用`-Djdk.tracePinnedThreads=full`会打印完整的堆栈跟踪，突出显示本地帧和持有监视器的帧。
- 使用`-Djdk.tracePinnedThreads=short`则只输出有问题的帧。

如果这些机制检测到线程固定既耗时又频繁，可以在这些特定地方用`ReentrantLock`替换`synchronized`（对于短暂或不频繁的操作，无需替换）。例如：

```java
synchronized(lockObj) {
    frequentIO();
}
```

可以替换为：

```java
lock.lock();
try {
    frequentIO();
} finally {
    lock.unlock();
}
```

这样可以避免线程固定对性能的负面影响。