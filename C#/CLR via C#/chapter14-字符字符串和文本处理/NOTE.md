## 字符

`System.Char` 表示成16位Unicode代码值

`Char.GetUnicodeCategory('a')` 返回字符a的由Unicode标准定义的类型

`Char.TryParse("a", out char c)` 转化字符串到字符

`var c = (Char)65` 数值转化为Char

`unchecked((Char)(65536 + 65))` 显示A, 65536 = 256*256

`Convert.ToChar(65536)` checked转换, 抛出OverflowException，因为65536超出一个字节

## 字符串

一个String代表一个**不可变**的顺序字符集

String直接派生自Object，所以是引用类型，分配在堆上

String是密封类，不能作为基类，因为CLR为String类做了很多的预设

    string s = "Hello, World!";

IL 代码

    ldstr "Hello, World!"

并没有调用ctor，而是使用了ldstr(load string)

    string phoneName = "apple " + "phone";

都是字面值，C#编译器在编译时连接它们，最终只有一个字符串`"apple phone"`生成

运行时的连接会在堆上创建多个字符串，影响性能，应该使用`StringBuilder`

字符串的不可变性，会在执行大量字符串操作的时候在堆上产生大量的字符串，从而影响性能，可以使用`StringBuilder`类

## 字符串留用（string interning）

CLR可通过一个String对象共享多个完全一致的String内容，减少系统中的字符串数量，从而节省内存

C#编译器会初始化一个内部哈希表来实现字符串的留用

## 字符串池

编译源代码时，把每个字面值字符串放入元数据会使生成的文件无谓的增大。所以编译时，如果字符串的字面值相同，元数据中只会写入一次，显著减少模块的大小。

## 比较字符串

## 高效构造字符串

StringBuilder

## 获取对象的字符串表示

