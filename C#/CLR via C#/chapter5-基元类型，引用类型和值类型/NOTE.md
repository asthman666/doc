## 基元类型

int 映射到 System.Int32

## 引用类型

* 总是处于已装箱的状态

## 值类型

### 考虑使用值类型的标准

* 类型具有基元类型的行为。类型不可变。

* 类型不需要从其他任何类型继承

* 类型也不派生出其他任何类型

* 类型实例较小 或者 类型实例较大，但不作为方法传递的参数，也不从方法返回

### 装箱机制

* 在托管堆中分配内存

* 值类型的字段复制到新分配的内存中

* 返回对象的地址

### 拆箱机制

* 获取已装箱的Point对象中的各个字段的地址

* 将字段包含的值从堆复制到基于栈的值类型的实例中

## 对象哈希码

重写Equals之所以还要重写GetHashCode，是由于在System.Collections.Hashtable和System.Collections.Generic.Dictionary等的实现中，要求两个对象必须具有相同的哈希码才被视为相等。

重写Equals就必须重写GetHashCode，确保相等性算法和对象哈希码算法一致。

System.Object实现的GetHashCode方法对派生类型和其中的字段一无所知，所以返回一个在对象生存期保证不变的编号。

## Dynamic

dynamic 其实就是 Object

    dynamic target = arg
    target.Contains("ah")

上段代码编译不会报错，但是执行过程中可能报错，如果arg不是字符串类型

## 引用类型和值类型

* 引用类型总是从托管堆分配
* 堆上分配的每个对象都有一些额外的成员，这些成员必须初始化
* 从托管堆分配对象时，可能强制执行一次垃圾回收

为了提升简单和常用的 类型的性能，CLR 提供了名为**值类型**的轻量级类型。值类型的实例一般在线程栈上分配（也可能作为字段嵌入引用类型的对象中）。值类型实例不受垃圾回收器的控制。

所有的值类型都称为结构或枚举。

### 什么时候使用值类型

* 类型就有基元类型的行为，是十分简单的类型，没有成员会修改类型的任何实例字段。
* 类型不需要从其他任何类型继承
* 类型也不派生出其他任何类型
* 考虑到值类型传参的字段复制，类型的实例较小（16字节或更小）
* 类型的实例较大（大于16个字节），但不作为方法实参传递，也不从方法返回

值类型的主要优势是不作为对象在托管堆上分配

If you instantiate a struct object using the default, parameterless constructor, all members are assigned according to their default values.

When writing a constructor with parameters for a struct, you must explicitly initialize all members; otherwise one or more members remain unassigned and the struct cannot be used, producing compiler error CS0171.

[structs](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/using-structs)