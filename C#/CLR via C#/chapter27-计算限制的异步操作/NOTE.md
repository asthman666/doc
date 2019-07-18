## CLR 线程池基础

* 创建和销毁线程是一个昂贵的操作，要耗费大量的时间

* 太多的线程会浪费内存资源

* 操作系统必须调度可运行的线程并执行上下文切换，所以太多的线程还对性能不利

为了改善这些情况，CLR包含了代码来管理它自己的线程池(thread pool)。


## 执行简单的计算限制操作

## 执行上下文

## 协作式取消和超时

## 任务内部揭秘

每个Task对象都有一组字段，这些字段构成了任务的状态

* Int32 ID，Task 的只读的 ID 属性
* 代表 Task 执行状态的一个 Int32
* 对父任务的引用
* 对 Task 创建时指定的 TaskScheduler 的引用
* 对回调方法的引用
* 对要传给回调方法的对象的引用(Task 的只读 AsyncState属性)
* 对 ExecutionContext 的引用以及对 ManualResetEventSlim 对象的引用

### 补充状态

* 一个CancellationToken
* 一个ContinueWithTask对象集合
* 为抛出未处理异常的子任务而准备的一个Task对象集合

如果不需要任务的附加功能，那么使用ThreadPool.QueueUserWorkItem能获得更好的资源利用率

### Status

* Created 任务显示创建，可以手动Start()这个任务
* WaitingForActivation 任务隐式创建，会自动开始
* WaitingToRun 任务已经调度，但尚未运行
* Running 任务正在运行
* WaitingForChildrenToComplete 任务正在等待子任务完成，子任务完成后它才能完成
* RanToCompletion 任务完成
* Canceled 任务取消
* Faulted 任务失败

## 任务调度器

TaskScheduler 将任务调度给线程池的工作者线程

## I/O 线程和工作者线程

