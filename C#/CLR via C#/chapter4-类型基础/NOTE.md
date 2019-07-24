class Employee { ... }

class Employee : System.Object { ... }

每个类型对象都有一个字段引用了它的基类型，方法调用回溯可用

## System.Object类提供的方法：

1. Equals 虚方法

2. GetHashCode 虚方法

    如果某个类型要在哈希表中作为键，应该重写该方法。

3. ToString 虚方法

        public virtual string ToString()
        {
            return this.GetType().ToString();
        }

4. GetType [extern](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/extern)方法

    返回Type类型的一个实例。

### 受保护的两个方法

1. MemberwiseClone `extern`方法

2. Finalize 虚方法

    对象的内存实际被回收之前，会调用这个方法

## New 操作符所做的事

1. 计算所有实例字段所需要的字节数

2. 从托管堆中分配类型要求的字节数

3. 初始化“类型对象指针”和“同步块索引”

    “类型对象指针”用来引用和对象对应的类型对象，可以用来调用静态方法。

4. 调用类型的构造器

`new` 执行了所有这些操作之后，返回指向新建对象的一个引用（或指针）。

**NOTE:**

如果一个引用类型，没有使用`new`初始化，就不会从托管堆上分配内存，例如：

    sting str = null

> [null](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/null)    

## 类型转换

CLR最重要的特性之一是**类型安全**

### 类型安全的优势

1. 程序员犯的许多错误都能在编译时检测到，确保代码在尝试执行前是正确的。

2. 能编译出更小，更快的代码，因为能在编译时进行更多的预设，并在生成的IL和元数据中落实预设。

## 运行时的相互关系

类型，对象，线程栈和托管堆

1. 线程创建时会分配到1MB的栈

2. 静态方法的调用

3. 虚方法的调用

4. 实例方法的调用

    找到“发出调用的那个变量的类型”对应的类型变量，若没有正在调用的方法，往上回溯调用

5. 栈堆的作用

6. 垃圾回收
