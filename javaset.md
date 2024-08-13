Java 提供了丰富的集合类库，用于存储和操作一组数据。集合框架主要位于 `java.util` 包中，涵盖了各种数据结构，包括列表、集合、映射和队列。以下是 Java 集合框架的基本类库和常见集合类型的详细介绍。

### 1. 集合框架的核心接口
Java 集合框架的核心接口定义了不同类型集合的基本行为。

- **Collection**: 所有集合的根接口，定义了最基本的集合操作。
- **List**: 有序集合，允许重复元素。常见实现类有 `ArrayList`、`LinkedList`、`Vector` 和 `Stack`。
- **Set**: 无序集合，不允许重复元素。常见实现类有 `HashSet`、`LinkedHashSet` 和 `TreeSet`。
- **Queue**: 先进先出的集合，常见实现类有 `LinkedList` 和 `PriorityQueue`。
- **Deque**: 双端队列，常见实现类有 `LinkedList` 和 `ArrayDeque`。
- **Map**: 键值对的集合，不允许键重复。常见实现类有 `HashMap`、`LinkedHashMap`、`TreeMap` 和 `Hashtable`。

### 2. 常见集合类及其实现

#### List 接口的实现类
- **ArrayList**: 基于动态数组实现的列表，支持快速随机访问和插入。
```java
List<String> arrayList = new ArrayList<>();
arrayList.add("Element 1");
arrayList.add("Element 2");
```

- **LinkedList**: 基于链表实现的列表，适合频繁的插入和删除操作。
```java
List<String> linkedList = new LinkedList<>();
linkedList.add("Element 1");
linkedList.add("Element 2");
```

- **Vector**: 类似于 `ArrayList`，但是是同步的。
```java
List<String> vector = new Vector<>();
vector.add("Element 1");
vector.add("Element 2");
```

- **Stack**: 继承自 `Vector`，实现了后进先出的栈。
```java
Stack<String> stack = new Stack<>();
stack.push("Element 1");
stack.push("Element 2");
```

#### Set 接口的实现类
- **HashSet**: 基于哈希表实现的集合，不保证元素的顺序。
```java
Set<String> hashSet = new HashSet<>();
hashSet.add("Element 1");
hashSet.add("Element 2");
```

- **LinkedHashSet**: 继承自 `HashSet`，并维护了元素的插入顺序。
```java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("Element 1");
linkedHashSet.add("Element 2");
```

- **TreeSet**: 基于红黑树实现的集合，保证元素的自然顺序或自定义顺序。
```java
Set<String> treeSet = new TreeSet<>();
treeSet.add("Element 1");
treeSet.add("Element 2");
```

#### Queue 接口的实现类
- **LinkedList**: 既可以作为列表使用，也可以作为队列使用。
```java
Queue<String> queue = new LinkedList<>();
queue.add("Element 1");
queue.add("Element 2");
```

- **PriorityQueue**: 基于优先级堆实现的队列，元素按优先级排序。
```java
Queue<String> priorityQueue = new PriorityQueue<>();
priorityQueue.add("Element 1");
priorityQueue.add("Element 2");
```

#### Deque 接口的实现类
- **LinkedList**: 既可以作为列表使用，也可以作为双端队列使用。
```java
Deque<String> deque = new LinkedList<>();
deque.addFirst("Element 1");
deque.addLast("Element 2");
```

- **ArrayDeque**: 基于数组实现的双端队列，通常比 `LinkedList` 更高效。
```java
Deque<String> arrayDeque = new ArrayDeque<>();
arrayDeque.addFirst("Element 1");
arrayDeque.addLast("Element 2");
```

#### Map 接口的实现类
- **HashMap**: 基于哈希表实现的映射，允许键和值为 null。
```java
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("Key 1", 1);
hashMap.put("Key 2", 2);
```

- **LinkedHashMap**: 继承自 `HashMap`，并维护了键值对的插入顺序。
```java
Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
linkedHashMap.put("Key 1", 1);
linkedHashMap.put("Key 2", 2);
```

- **TreeMap**: 基于红黑树实现的映射，保证键的自然顺序或自定义顺序。
```java
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Key 1", 1);
treeMap.put("Key 2", 2);
```

- **Hashtable**: 类似于 `HashMap`，但不允许键和值为 null，并且是同步的。
```java
Map<String, Integer> hashtable = new Hashtable<>();
hashtable.put("Key 1", 1);
hashtable.put("Key 2", 2);
```

### 3. 并发集合
Java 提供了一些线程安全的集合类，位于 `java.util.concurrent` 包中。

- **ConcurrentHashMap**: 线程安全的哈希表，比 `Hashtable` 更高效。
```java
Map<String, Integer> concurrentHashMap = new ConcurrentHashMap<>();
concurrentHashMap.put("Key 1", 1);
concurrentHashMap.put("Key 2", 2);
```

- **CopyOnWriteArrayList**: 线程安全的 `ArrayList` 实现，适用于读多写少的场景。
```java
List<String> copyOnWriteArrayList = new CopyOnWriteArrayList<>();
copyOnWriteArrayList.add("Element 1");
copyOnWriteArrayList.add("Element 2");
```

- **CopyOnWriteArraySet**: 基于 `CopyOnWriteArrayList` 实现的线程安全的集合。
```java
Set<String> copyOnWriteArraySet = new CopyOnWriteArraySet<>();
copyOnWriteArraySet.add("Element 1");
copyOnWriteArraySet.add("Element 2");
```

- **BlockingQueue**: 支持线程安全的队列操作，适用于生产者-消费者模式。
- **ArrayBlockingQueue**: 基于数组的有界阻塞队列。
```java
BlockingQueue<String> arrayBlockingQueue = new ArrayBlockingQueue<>(10);
arrayBlockingQueue.put("Element 1");
arrayBlockingQueue.put("Element 2");
```

- **LinkedBlockingQueue**: 基于链表的有界或无界阻塞队列。
```java
BlockingQueue<String> linkedBlockingQueue = new LinkedBlockingQueue<>();
linkedBlockingQueue.put("Element 1");
linkedBlockingQueue.put("Element 2");
```

- **PriorityBlockingQueue**: 支持优先级排序的无界阻塞队列。
```java
BlockingQueue<String> priorityBlockingQueue = new PriorityBlockingQueue<>();
priorityBlockingQueue.put("Element 1");
priorityBlockingQueue.put("Element 2");
```

- **DelayQueue**: 支持延迟获取元素的无界阻塞队列。
```java
import java.util.concurrent.Delayed;
import java.util.concurrent.DelayQueue;
import java.util.concurrent.TimeUnit;

class DelayedElement implements Delayed {
private final long delayTime;
private final long expirationTime;
private final String element;

public DelayedElement(String element, long delayTime) {
this.element = element;
this.delayTime = delayTime;
this.expirationTime = System.currentTimeMillis() + delayTime;
}

@Override
public long getDelay(TimeUnit unit) {
long delay = expirationTime - System.currentTimeMillis();
return unit.convert(delay, TimeUnit.MILLISECONDS);
}

@Override
public int compareTo(Delayed o) {
if (this.expirationTime < ((DelayedElement) o).expirationTime) {
return -1;
} else if (this.expirationTime > ((DelayedElement) o).expirationTime) {
return 1;
}
return 0;
}

@Override
public String toString() {
return element;
}
}

public class DelayQueueExample {
public static void main(String[] args) throws InterruptedException {
DelayQueue<DelayedElement> delayQueue = new DelayQueue<>();
delayQueue.put(new DelayedElement("Element 1", 5000));
delayQueue.put(new DelayedElement("Element 2", 10000));

System.out.println("Waiting for elements...");

while (!delayQueue.isEmpty()) {
DelayedElement element = delayQueue.take();
System.out.println("Retrieved: " + element);
}
}
}
```

- **SynchronousQueue**: 每个插入操作必须等待相应的删除操作，反之亦然。
```java
BlockingQueue<String> synchronousQueue = new SynchronousQueue<>();
new Thread(() -> {
try {
synchronousQueue.put("Element 1");
System.out.println("Element 1 put into the queue");
} catch (InterruptedException e) {
e.printStackTrace();
}
}).start();

new Thread(() -> {
try {
String element = synchronousQueue.take();
System.out.println("Element retrieved from the queue: " + element);
} catch (InterruptedException e) {
e.printStackTrace();
}
}).start();
```

### 4. 集合工具类
Java 提供了一些工具类来帮助操作集合。

- **Collections**: 提供静态方法来操作或返回集合，例如排序、搜索、同步集合等。
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
public static void main(String[] args) {
List<String> list = new ArrayList<>();
list.add("Banana");
list.add("Apple");
list.add("Cherry");

Collections.sort(list);
System.out.println("Sorted list: " + list);

Collections.reverse(list);
System.out.println("Reversed list: " + list);
}
}
```

- **Arrays**: 提供静态方法来操作数组，如排序、搜索、转换为列表等。
```java
import java.util.Arrays;
import java.util.List;

public class ArraysExample {
public static void main(String[] args) {
String[] array = {"Banana", "Apple", "Cherry"};

// 排序数组
Arrays.sort(array);
System.out.println("Sorted array: " + Arrays.toString(array));

// 转换数组为列表
List<String> list = Arrays.asList(array);
System.out.println("Array converted to list: " + list);
}
}
```

### 5. 集合的不可变视图
Java 提供了创建不可变集合的机制，确保集合内容在创建后不能被修改。

- **Collections.unmodifiableList**: 返回一个不可变的列表视图。
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class UnmodifiableListExample {
public static void main(String[] args) {
List<String> list = new ArrayList<>();
list.add("Element 1");
list.add("Element 2");

List<String> unmodifiableList = Collections.unmodifiableList(list);
System.out.println("Unmodifiable list: " + unmodifiableList);

// 试图修改不可变列表会抛出 UnsupportedOperationException
// unmodifiableList.add("Element 3");
}
}
```

- **Collections.unmodifiableSet**: 返回一个不可变的集合视图。
```java
import java.util.Collections;
import java.util.HashSet;
import java.util.Set;

public class UnmodifiableSetExample {
public static void main(String[] args) {
Set<String> set = new HashSet<>();
set.add("Element 1");
set.add("Element 2");

Set<String> unmodifiableSet = Collections.unmodifiableSet(set);
System.out.println("Unmodifiable set: " + unmodifiableSet);

// 试图修改不可变集合会抛出 UnsupportedOperationException
// unmodifiableSet.add("Element 3");
}
}
```

- **Collections.unmodifiableMap**: 返回一个不可变的映射视图。
```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class UnmodifiableMapExample {
public static void main(String[] args) {
Map<String, Integer> map = new HashMap<>();
map.put("Key 1", 1);
map.put("Key 2", 2);

Map<String, Integer> unmodifiableMap = Collections.unmodifiableMap(map);
System.out.println("Unmodifiable map: " + unmodifiableMap);

// 试图修改不可变映射会抛出 UnsupportedOperationException
// unmodifiableMap.put("Key 3", 3);
}
}
```

### 6. 集合的同步视图
Java 提供了创建线程安全集合的方法，确保多个线程对集合的访问是安全的。

- **Collections.synchronizedList**: 返回一个同步的列表视图。
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class SynchronizedListExample {
public static void main(String[] args) {
List<String> list = new ArrayList<>();
list.add("Element 1");
list.add("Element 2");

List<String> synchronizedList = Collections.synchronizedList(list);
synchronized (synchronizedList) {
for (String element : synchronizedList) {
System.out.println(element);
}
}
}
}
```

- **Collections.synchronizedSet**: 返回一个同步的集合视图

```java
import java.util.Collections;
import java.util.HashSet;
import java.util.Set;

public class SynchronizedSetExample {
public static void main(String[] args) {
Set<String> set = new HashSet<>();
set.add("Element 1");
set.add("Element 2");

Set<String> synchronizedSet = Collections.synchronizedSet(set);
synchronized (synchronizedSet) {
for (String element : synchronizedSet) {
System.out.println(element);
}
}
}
}
```

- **Collections.synchronizedMap**: 返回一个同步的映射视图。
```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class SynchronizedMapExample {
public static void main(String[] args) {
Map<String, Integer> map = new HashMap<>();
map.put("Key 1", 1);
map.put("Key 2", 2);

Map<String, Integer> synchronizedMap = Collections.synchronizedMap(map);
synchronized (synchronizedMap) {
for (Map.Entry<String, Integer> entry : synchronizedMap.entrySet()) {
System.out.println(entry.getKey() + ": " + entry.getValue());
}
}
}
}
```

### 7. Java 9 及以上版本的新特性
Java 9 引入了一些新的集合工厂方法，用于创建不可变的集合。

- **List.of**: 创建不可变的列表。
```java
import java.util.List;

public class ListOfExample {
public static void main(String[] args) {
List<String> list = List.of("Element 1", "Element 2", "Element 3");
System.out.println("Immutable list: " + list);

// 试图修改不可变列表会抛出 UnsupportedOperationException
// list.add("Element 4");
}
}
```

- **Set.of**: 创建不可变的集合。
```java
import java.util.Set;

public class SetOfExample {
public static void main(String[] args) {
Set<String> set = Set.of("Element 1", "Element 2", "Element 3");
System.out.println("Immutable set: " + set);

// 试图修改不可变集合会抛出 UnsupportedOperationException
// set.add("Element 4");
}
}
```

- **Map.of**: 创建不可变的映射。
```java
import java.util.Map;

public class MapOfExample {
public static void main(String[] args) {
Map<String, Integer> map = Map.of("Key 1", 1, "Key 2", 2, "Key 3", 3);
System.out.println("Immutable map: " + map);

// 试图修改不可变映射会抛出 UnsupportedOperationException
// map.put("Key 4", 4);
}
}
```

### 8. 总结
Java 提供了丰富的集合类库来处理各种数据结构和并发需求。以下是总结的主要集合类型及其常用实现类：

- **List 接口**: `ArrayList`、`LinkedList`、`Vector`、`Stack`
- **Set 接口**: `HashSet`、`LinkedHashSet`、`TreeSet`
- **Queue 接口**: `LinkedList`、`PriorityQueue`
- **Deque 接口**: `LinkedList`、`ArrayDeque`
- **Map 接口**: `HashMap`、`LinkedHashMap`、`TreeMap`、`Hashtable`
- **并发集合**: `ConcurrentHashMap`、`CopyOnWriteArrayList`、`CopyOnWriteArraySet`、`BlockingQueue`（如 `ArrayBlockingQueue`、`LinkedBlockingQueue`、`PriorityBlockingQueue`、`DelayQueue`、`SynchronousQueue`）

### 9. 集合框架的核心概念

#### 泛型（Generics）
Java 集合框架广泛使用了泛型，以提高类型安全性和代码可读性。例如：
```java
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123); // 编译错误，泛型限制了集合中元素的类型
```

#### 遍历集合
Java 提供了多种方式来遍历集合，包括 `for-each` 循环、迭代器和流（Streams）。

- **for-each 循环**
```java
List<String> list = List.of("Element 1", "Element 2", "Element 3");
for (String element : list) {
System.out.println(element);
}
```

- **迭代器（Iterator）**
```java
List<String> list = List.of("Element 1", "Element 2", "Element 3");
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
System.out.println(iterator.next());
}
```

- **流（Streams）**
```java
List<String> list = List.of("Element 1", "Element 2", "Element 3");
list.stream().forEach(System.out::println);
```

#### 集合的排序
Java 提供了多种方式来对集合进行排序。

- **使用 `Collections.sort()`**
```java
List<String> list = new ArrayList<>(List.of("Banana", "Apple", "Cherry"));
Collections.sort(list);
System.out.println("Sorted list: " + list);
```

- **使用 `List.sort()`**
```java
List<String> list = new ArrayList<>(List.of("Banana", "Apple", "Cherry"));
list.sort(Comparator.naturalOrder());
System.out.println("Sorted list: " + list);
```

- **自定义排序**
```java
List<String> list = new ArrayList<>(List.of("Banana", "Apple", "Cherry"));
list.sort((a, b) -> b.compareTo(a)); // 按逆序排序
System.out.println("Sorted list in reverse order: " + list);
```

#### 集合的过滤和转换
Java 8 引入了流（Streams）API，使得集合的过滤和转换更加简洁。

- **过滤**
```java
List<String> list = List.of("Apple", "Banana", "Cherry", "Date");
List<String> filteredList = list.stream()
.filter(s -> s.startsWith("B"))
.collect(Collectors.toList());
System.out.println("Filtered list: " + filteredList);
```

- **转换**
```java
List<String> list = List.of("Apple", "Banana", "Cherry", "Date");
List<Integer> lengths = list.stream()
.map(String::length)
.collect(Collectors.toList());
System.out.println("Lengths of elements: " + lengths);
```
