# Struct VS Class

* Struct是值类型，在线程栈上分配

* Class是引用类型，在托管堆上分配

* 值类型对象又两种表示形式： 未装箱和已装箱，引用类型总是处于已装箱形式

* 值类型变量赋给另外一个变量，会执行逐字段复制， 引用类型只需复制内存地址

* 未装箱的值类型不在堆上分配，所以不需要垃圾回收

> [classes-and-structs](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/)

> [choosing-between-class-and-struct](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/choosing-between-class-and-struct)

> [types](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/)

## struct

### Instantiation of a structure type

在C#中，在使用一个声明的变量之前，你必须初始化它。因为structure-type变量不能为null，所以你必须实例化一个相应类型的实例。

和class一样，struct都有一个默认的无参构造器，调用这个无参构造器会产生struct类型的一个default value，例如：

    public struct Point
    {
        public int x;
        public int y;
    }

    var defaultPoint = default(Point);
    var newPoint = new Point();

如果struct类型所有的实例字段都是可以访问的，你也可以不用new初始化它。在你第一次使用这个实例前，你必须初始化所有的实例字段。例如:

    Point p;
    p.x = 1;
    p.y = 2;
    Console.WriteLine(p.x);

如果这样，会报错:

    Point p;
    p.x = 1;
    Console.WriteLine(p.y); // compile error


[struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct)