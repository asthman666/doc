# Garbage Collection

## 基本功能

.NET 的垃圾收集管理你的应用的内存的分配和释放。

每次你创建一个新的对象，CLR从管理堆(managed heap)上为这个对象分配内存。

内存不是无限的，垃圾收集器必须工作以便释放内存。

当垃圾收集器工作时，它会检查管理堆上不再被应用使用的对象，释放它们的内存。

## 好处

* 不用手动释放内存

* 更有效的从管理堆上分配内存

* 内存安全，一个对象不能使用另外一个对象的内容

## 垃圾收集的条件

* 系统内存很小。CLR内部使用 Win32 函数 CreateMemoryResourceNotification 和 QueryMemoryResourceNotification 监视系统的总体内存使用情况。如果Windows报告低内存，CLR将强制垃圾回收以释放死对象。

* 托管堆上的内存使用超过了阈值。这个阈值会随着进程的运行不断的调整。CLR在检测第0代超过预算时触发一次GC，这是GC最常见的触发条件。

* 调用 `GC.Collect` 方法。

## 受管理的堆(managed heap)

CLR 初始化垃圾回收器，它会分配一段内存用来存储和管理对象。这段内存就被叫做**受管理的堆**，它和操作系统里的**本机堆**(native heap)是相反的。这段内存的大小是特定实现的，被认为是随时都会改变。

每个受管理的进程有一个受管理的堆。一个进程里的所有的线程，在同一个堆上为对象分配内存。

堆上分配的对象越少(大小和数量)，垃圾收集工作越少。

当垃圾收集被触发，垃圾收集器会回收被死对象占据的内存。这个回收过程会把活对象紧凑的移动到一起，确保分配在受管理堆上的对象在一起。

堆可以被认为堆积成两个堆，**大对象堆**和**小对象堆**。

## Generations

堆被组织成**代**(Generations)，可以处理长活和短活的对象。垃圾收集主要发生在短活对象的回收，这些短活对象一般仅占据堆的一小部分。在堆上一共有3代对象：

1. Generation 0

第零代包含短活对象。例如一些短活的临时变量。 垃圾收集经常在这一代上发生。

新分配的对象隐式的在第零代堆上收集，当它们是大对象是，它们会去大对象堆，大对象堆在第二代收集。

大部分在第零代垃圾收集的对象不会存活到下一代。

2. Generation 1

这一代包含短活对象，是短活和长活对象中间的一个缓冲区。

3. Generation 2

这一代包含长活对象。例如一个长活对象是一个应用中包含静态数据的对象，它在进程中一直存活。

Collecting a generation means collecting objects in that generation and all its younger generations. 

第二代垃圾收集也被叫做全垃圾收集(full garbage collection)，因为它回收所有代上的死对象。

## 一个线程触发垃圾收集会引起其他线程被挂起

<img src='https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/media/gc-triggered.png'>

> [garbage collection fundamentals](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals)

> [large-object-heap](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/large-object-heap)