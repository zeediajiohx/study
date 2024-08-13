## 一、Java IO
Java 的 IO（输入/输出）系统用于处理数据的读写操作，Java 提供了丰富的类和接口来支持文件和数据流的操作。以下是一些主要的基础类库和它们的功能描述：
### 1. java.io 包
`java.io` 包是 Java 中处理输入输出的主要包，包括了处理字节流和字符流的类。

#### 字节流类（用于处理二进制数据）
- **InputStream**: 字节输入流的抽象类，用于读取字节数据。
- **FileInputStream**: 从文件中读取字节数据。
- **ByteArrayInputStream**: 从字节数组中读取数据。
- **BufferedInputStream**: 为另一个输入流添加缓冲功能，提高读取效率。
- **DataInputStream**: 用于读取基本数据类型（如 int、float 等）的输入流。

- **OutputStream**: 字节输出流的抽象类，用于写入字节数据。
- **FileOutputStream**: 写字节数据到文件。
- **ByteArrayOutputStream**: 写字节数据到字节数组。
- **BufferedOutputStream**: 为另一个输出流添加缓冲功能，提高写入效率。
- **DataOutputStream**: 用于写入基本数据类型（如 int、float 等）的输出流。

#### 字符流类（用于处理文本数据）
- **Reader**: 字符输入流的抽象类，用于读取字符数据。
- **FileReader**: 从文件中读取字符数据。
- **CharArrayReader**: 从字符数组中读取数据。
- **BufferedReader**: 为另一个字符输入流添加缓冲功能，提高读取效率。
- **InputStreamReader**: 将字节输入流转换为字符输入流。

- **Writer**: 字符输出流的抽象类，用于写入字符数据。
- **FileWriter**: 写字符数据到文件。
- **CharArrayWriter**: 写字符数据到字符数组。
- **BufferedWriter**: 为另一个字符输出流添加缓冲功能，提高写入效率。
- **OutputStreamWriter**: 将字符输出流转换为字节输出流。

#### 对象流类（用于对象的序列化）
- **ObjectInputStream**: 反序列化从流中读取的对象。
- **ObjectOutputStream**: 序列化对象并将其写入流中。

### 2. java.nio 包
`java.nio`（New IO）包提供了面向缓冲区的 IO 操作，通常用于高性能 IO 操作。

#### 主要类和接口
- **Buffer**: 缓冲区的抽象类，用于存储不同类型的数据（ByteBuffer、CharBuffer、IntBuffer 等）。
- **Channel**: 通道接口，用于 IO 操作（FileChannel、SocketChannel 等）。
- **Selector**: 多路复用选择器，用于非阻塞 IO 操作。

### 使用示例
下面是一个简单的示例，演示如何使用字节流和字符流来读取和写入文件。

#### 使用 FileInputStream 和 FileOutputStream
```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamExample {
public static void main(String[] args) {
try (FileInputStream fis = new FileInputStream("input.txt");
FileOutputStream fos = new FileOutputStream("output.txt")) {

int byteData;
while ((byteData = fis.read()) != -1) {
fos.write(byteData);
}

} catch (IOException e) {
e.printStackTrace();
}
}
}
```

#### 使用 FileReader 和 FileWriter
```java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class CharStreamExample {
public static void main(String[] args) {
try (FileReader fr = new FileReader("input.txt");
FileWriter fw = new FileWriter("output.txt")) {

int charData;
while ((charData = fr.read()) != -1) {
fw.write(charData);
}

} catch (IOException e) {
e.printStackTrace();
}
}
}
```

### 使用 BufferedReader 和 BufferedWriter
```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedCharStreamExample {
public static void main(String[] args) {
try (BufferedReader br = new BufferedReader(new FileReader("input.txt"));
BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {

String line;
while ((line = br.readLine()) != null) {
bw.write(line);
bw.newLine(); // 写入行分隔符
}

} catch (IOException e) {
e.printStackTrace();
}
}
}
```

### 使用 ObjectOutputStream 和 ObjectInputStream
```java
import java.io.*;

class Person implements Serializable {
private static final long serialVersionUID = 1L;
private String name;
private int age;

public Person(String name, int age) {
this.name = name;
this.age = age;
}

@Override
public String toString() {
return "Person{name='" + name + "', age=" + age + "}";
}
}

public class ObjectStreamExample {
public static void main(String[] args) {
Person person = new Person("John Doe", 30);

try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"));
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {

// 序列化对象
oos.writeObject(person);

// 反序列化对象
Person deserializedPerson = (Person) ois.readObject();
System.out.println(deserializedPerson);

} catch (IOException | ClassNotFoundException e) {
e.printStackTrace();
}
}
}
```

### 使用 java.nio 包中的 FileChannel
```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

public class NIOExample {
public static void main(String[] args) {
try (FileChannel sourceChannel = new FileInputStream("input.txt").getChannel();
FileChannel destChannel = new FileOutputStream("output.txt").getChannel()) {

ByteBuffer buffer = ByteBuffer.allocate(1024);

while (sourceChannel.read(buffer) != -1) {
buffer.flip(); // 准备写入
destChannel.write(buffer);
buffer.clear(); // 准备读取
}

} catch (IOException e) {
e.printStackTrace();
}
}
}
```
## 二、 Java 多线程
Java 提供了多种机制来实现多线程编程，并且提供了丰富的类库来管理和控制并发操作。以下是 Java 多线程编程的实现方式、基础类库和涉及的技术栈。

### 1. 线程的基本实现方式
在 Java 中，可以通过以下几种方式来创建和运行线程：

#### 继承 Thread 类
```java
public class MyThread extends Thread {
@Override
public void run() {
System.out.println("Thread is running");
}

public static void main(String[] args) {
MyThread thread = new MyThread();
thread.start();
}
}
```

#### 实现 Runnable 接口
```java
public class MyRunnable implements Runnable {
@Override
public void run() {
System.out.println("Thread is running");
}

public static void main(String[] args) {
Thread thread = new Thread(new MyRunnable());
thread.start();
}
}
```

#### 使用 Callable 和 Future
```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class MyCallable implements Callable<String> {
@Override
public String call() {
return "Task completed";
}

public static void main(String[] args) {
ExecutorService executor = Executors.newSingleThreadExecutor();
Future<String> future = executor.submit(new MyCallable());

try {
System.out.println(future.get());
} catch (InterruptedException | ExecutionException e) {
e.printStackTrace();
} finally {
executor.shutdown();
}
}
}
```

### 2. 基础类库

#### java.lang.Thread
`Thread` 类是 Java 中表示线程的基本类。它提供了线程的基本操作，如启动、睡眠、中断等。

#### java.lang.Runnable
`Runnable` 接口只有一个方法 `run()`，任何实现该接口的类都可以作为线程的任务。

#### java.util.concurrent 包
`java.util.concurrent` 包提供了更高级的并发工具和类，包括线程池、同步工具、并发集合等。

- **Executor、ExecutorService**: 线程池的基本接口和实现类，用于管理一组线程。
- **Future、Callable**: 支持异步任务的处理和返回结果。
- **CountDownLatch**: 用于同步一组线程，等待其他线程完成。
- **CyclicBarrier**: 用于让一组线程互相等待，直到到达一个公共的屏障点。
- **Semaphore**: 用于控制对资源的访问。
- **ConcurrentHashMap**: 线程安全的哈希表。
- **BlockingQueue**: 支持线程安全的队列操作。

### 3. 线程同步和加锁机制
Java 提供了多种方式来实现线程同步和加锁，以确保共享资源的正确访问。

#### synchronized 关键字
`synchronized` 关键字用于同步方法或代码块，确保同一时刻只有一个线程能够执行。

```java
public class Counter {
private int count = 0;

public synchronized void increment() {
count++;
}

public int getCount() {
return count;
}
}
```

#### ReentrantLock
`ReentrantLock` 提供了更灵活的锁机制，可以显式地加锁和解锁。

```java
import java.util.concurrent.locks.ReentrantLock;

public class Counter {
private final ReentrantLock lock = new ReentrantLock();
private int count = 0;

public void increment() {
lock.lock();
try {
count++;
} finally {
lock.unlock();
}
}

public intgetCount() {
lock.lock();
try {
return count;
} finally {
lock.unlock();
}
}
}
```

### 4. 共享内存和线程间通信

Java 提供了几种机制来实现线程间的通信和共享内存。

#### volatile 关键字
`volatile` 关键字用于声明变量，使其在多个线程之间可见，保证变量的可见性。

```java
public class VolatileExample {
private volatile boolean running = true;

public void stop() {
running = false;
}

public void run() {
while (running) {
// 执行一些任务
}
}
}
```

#### wait()、notify() 和 notifyAll()
这些方法用于线程之间的通信，通常与 `synchronized` 关键字结合使用。

```java
public class WaitNotifyExample {
private final Object lock = new Object();

public void doWait() {
synchronized (lock) {
try {
System.out.println("Waiting...");
lock.wait();
System.out.println("Woke up!");
} catch (InterruptedException e) {
e.printStackTrace();
}
}
}

public void doNotify() {
synchronized (lock) {
System.out.println("Notifying...");
lock.notify();
}
}

public static void main(String[] args) throws InterruptedException {
WaitNotifyExample example = new WaitNotifyExample();

Thread thread1 = new Thread(example::doWait);
Thread thread2 = new Thread(example::doNotify);

thread1.start();
Thread.sleep(1000); // 确保 thread1 先执行
thread2.start();
}
}
```

### 5. 管道（Pipes）
Java 提供了管道类，用于线程间的字节流或字符流通信。

#### PipedInputStream 和 PipedOutputStream
用于字节流通信。

```java
import java.io.PipedInputStream;
import java.io.PipedOutputStream;
import java.io.IOException;

public class PipeExample {
public static void main(String[] args) {
try (PipedInputStream pis = new PipedInputStream();
PipedOutputStream pos = new PipedOutputStream(pis)) {

Thread writerThread = new Thread(() -> {
try {
pos.write("Hello, Pipe!".getBytes());
} catch (IOException e) {
e.printStackTrace();
}
});

Thread readerThread = new Thread(() -> {
try {
int data;
while ((data = pis.read()) != -1) {
System.out.print((char) data);
}
} catch (IOException e) {
e.printStackTrace();
}
});

writerThread.start();
readerThread.start();
writerThread.join();
readerThread.join();

} catch (IOException | InterruptedException e) {
e.printStackTrace();
}
}
}
```

#### PipedReader 和 PipedWriter
用于字符流通信。

```java
import java.io.PipedReader;
import java.io.PipedWriter;
import java.io.IOException;

public class PipeCharExample {
public static void main(String[] args) {
try (PipedReader pr = new PipedReader();
PipedWriter pw = new PipedWriter(pr)) {

Thread writerThread = new Thread(() -> {
try {
pw.write("Hello, Pipe!");
} catch (IOException e) {
e.printStackTrace();
}
});

Thread readerThread = new Thread(() -> {
try {
int data;
while ((data = pr.read()) != -1) {
System.out.print((char) data);
}
} catch (IOException e) {
e.printStackTrace();
}
});

writerThread.start();
readerThread.start();
writerThread.join();
readerThread.join();

} catch (IOException | InterruptedException e) {
e.printStackTrace();
}
}
}
```

### 6. 高级并发工具

Java 提供了一些高级并发工具来简化多线程编程。

#### 线程池（Thread Pools）
使用 `ExecutorService` 来管理线程池，可以更高效地管理一组线程的生命周期。

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
public static void main(String[] args) {
ExecutorService executor = Executors.newFixedThreadPool(5);

for (int i = 0; i < 10; i++) {
executor.submit(() -> {
System.out.println("Task executed by " + Thread.currentThread().getName());
});
}

executor.shutdown();
}
}
```

#### CountDownLatch
用于一个或多个线程等待其他线程完成操作。

```java
import java.util.concurrent.CountDownLatch;

public class CountDownLatchExample {
public static void main(String[] args) {
CountDownLatch latch = new CountDownLatch(3);

Runnable task = () -> {
System.out.println(Thread.currentThread().getName() + " completed task");
latch.countDown();
};

for (int i = 0; i < 3; i++) {
new Thread(task).start();
}

try {
latch.await();
System.out.println("All tasks completed");
} catch (InterruptedException e) {
e.printStackTrace();
}
}
}
```

#### CyclicBarrier
用于一组线程互相等待，直到到达一个公共的屏障点。

```java
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierExample {
public static void main(String[] args) {
int parties = 3;
CyclicBarrier barrier = new CyclicBarrier(parties, () -> {
System.out.println("All parties have reached the barrier");
});

Runnable task = () -> {
try {
System.out.println(Thread.currentThread().getName() + " is waiting at the barrier");
barrier.await();
System.out.println(Thread.currentThread().getName() + " has crossed the barrier");
} catch (InterruptedException | BrokenBarrierException e) {
e.printStackTrace();
}
};

for (int i = 0; i < parties; i++) {
new Thread(task).start();
}
}
}
```

#### Semaphore
用于控制对资源的访问量。

```java
import java.util.concurrent.Semaphore;

public class SemaphoreExample {
public static void main(String[] args) {
Semaphore semaphore = new Semaphore(3);

Runnable task = () -> {
try {
semaphore.acquire();
System.out.println(Thread.currentThread().getName() + " acquired the permit");
Thread.sleep(2000);
System.out.println(Thread.currentThread().getName() + " released the permit");
semaphore.release();
} catch (InterruptedException e) {
e.printStackTrace();
}
};

for (int i = 0; i < 6; i++) {
new Thread(task).start();
}
}
}
```

### 7. 并发集合
Java 提供了一些线程安全的集合类来简化并发编程。

#### ConcurrentHashMap
线程安全的哈希表。

```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ConcurrentHashMapExample {
public static void main(String[] args) {
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
ExecutorService executor = Executors.newFixedThreadPool(3);

Runnable task = () -> {
for (int i = 0; i < 10; i++) {
String key = Thread.currentThread().getName() + "-" + i;
map.put(key, i);
System.out.println(key + " added to the map");
}
};

for (int i = 0; i < 3; i++) {
executor.submit(task);
}

executor.shutdown();
while (!executor.isTerminated()) {
// 等待所有线程完成
}

System.out.println("Final map: " + map);
}
}
```

#### CopyOnWriteArrayList
线程安全的 ArrayList 实现。

```java
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class CopyOnWriteArrayListExample {
public static void main(String[] args) {
List<String> list = new CopyOnWriteArrayList<>();
ExecutorService executor = Executors.newFixedThreadPool(3);

Runnable task = () -> {
for (int i = 0; i < 10; i++) {
String element = Thread.currentThread().getName() + "-" + i;
list.add(element);
System.out.println(element + " added to the list");
}
};

for (int i = 0; i < 3; i++) {
executor.submit(task);
}

executor.shutdown();
while (!executor.isTerminated()) {
// 等待所有线程完成
}

System.out.println("Final list: " + list);
}
}
```

#### BlockingQueue
线程安全的队列，用于生产者-消费者模式。

```java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class BlockingQueueExample {
public static void main(String[] args) {
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);
ExecutorService executor = Executors.newFixedThreadPool(2);

Runnable producer = () -> {
for (int i = 0; i < 10; i++) {
try {
String element = "Element-" + i;
queue.put(element);
System.out.println("Produced: " + element);
} catch (InterruptedException e) {
e.printStackTrace();
}
}
};

Runnable consumer = () -> {
for (int i = 0; i < 10; i++) {
try {
String element = queue.take();
System.out.println("Consumed: " + element);
} catch (InterruptedException e) {
e.printStackTrace();
}
}
};

executor.submit(producer);
executor.submit(consumer);

executor.shutdown();
while (!executor.isTerminated()) {
// 等待所有线程完成
}

System.out.println("All tasks completed");
}
}
```

### 8. 使用 ForkJoinPool
ForkJoinPool 是一种用于并行处理任务的框架，适用于递归任务的分治策略。

```java
import java.util.concurrent.RecursiveTask;
import java.util.concurrent.ForkJoinPool;

public class ForkJoinExample {
static class SumTask extends RecursiveTask<Long> {
private static final int THRESHOLD = 1000;
private final long[] numbers;
private final int start;
private final int end;

public SumTask(long[] numbers, int start, int end) {
this.numbers = numbers;
this.start = start;
this.end = end;
}

@Override
protected Long compute() {
int length = end - start;
if (length <= THRESHOLD) {
long sum = 0;
for (int i = start; i < end; i++) {
sum += numbers[i];
}
return sum;
} else {
int middle = start + length / 2;
SumTask leftTask = new SumTask(numbers, start, middle);
SumTask rightTask = new SumTask(numbers, middle, end);
leftTask.fork();
long rightResult = rightTask.compute();
long leftResult = leftTask.join();
return leftResult + rightResult;
}
}
}

public static void main(String[] args) {
long[] numbers = new long[10000];
for (int i = 0; i < numbers.length; i++) {
numbers[i] = i;
}

ForkJoinPool forkJoinPool = new ForkJoinPool();
SumTask task = new SumTask(numbers, 0, numbers.length);
long result = forkJoinPool.invoke(task);
System.out.println("Sum: " + result);
}
}
```

### 9. 异步编程
Java 提供了 `CompletableFuture` 类来进行异步编程。

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

public class CompletableFutureExample {
public static void main(String[] args) {
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
try {
Thread.sleep(1000);
} catch (InterruptedException e) {
e.printStackTrace();
}
return "Hello, World!";
});

future.thenAccept(result -> {
System.out.println("Result: " + result);
});

try {
future.get(); // 阻塞，直到任务完成
} catch (InterruptedException | ExecutionException e) {
e.printStackTrace();
}
}
}
```

### 10. 总结
Java 提供了丰富的工具和类库来支持多线程编程和并发控制。通过理解和使用这些工具，你可以编写高效且线程安全的程序。以下是一些常用技术和类库的概述：

- **基础类**: `Thread`、`Runnable`、`Callable`、`Future`
- **高级并发工具**: `ExecutorService`、`CountDownLatch`、`CyclicBarrier`、`Semaphore`
- **同步与锁**: `synchronized`、`ReentrantLock`
- **线程间通信**: `volatile`、`wait()`、`notify()`、`notifyAll()`
- **管道**: `PipedInputStream`、`PipedOutputStream`、`PipedReader`、`PipedWriter`
- **并发集合**: `ConcurrentHashMap`、`CopyOnWriteArrayList`、`BlockingQueue`
- **ForkJoin框架**: `ForkJoinPool`、`RecursiveTask`
- **异步编程**: `CompletableFuture`
