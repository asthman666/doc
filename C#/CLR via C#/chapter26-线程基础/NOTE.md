## windows进程，线程

**进程**实际是应用程序的实例要使用的资源的集合。每个进程都被赋予了一个虚拟的地址空间，确保在一个进程中使用的代码和数据无法由另一个进程访问。

[threads and threading](https://docs.microsoft.com/en-us/dotnet/standard/threading/threads-and-threading)

作为一个Windows概念，**线程**的职责是对CPU进行虚拟化。Windows为每个进程都提供了该进程专用的一个线程（功能相当于一个CPU）。应用程序的代码进入死循环，与那个代码关联的进程会冻结，但其他进程（它们有自己的线程）不会冻结，它们会继续执行

## 线程开销

* 线程

