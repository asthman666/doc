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