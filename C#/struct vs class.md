# Struct VS Class

* Struct是值类型，在线程栈上分配

* Class是引用类型，在托管堆上分配

* 值类型对象又两种表示形式： 未装箱和已装箱，引用类型总是处于已装箱形式

* 值类型变量赋给另外一个变量，会执行逐字段复制， 引用类型只需复制内存地址

* 未装箱的值类型不在堆上分配，所以不需要垃圾回收

> [classes-and-structs](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/)

> [choosing-between-class-and-struct](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/choosing-between-class-and-struct)