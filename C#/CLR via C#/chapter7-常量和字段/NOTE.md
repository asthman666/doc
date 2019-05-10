常量的值从不变化，所以常量总是被视为类型定义的一部分，常量总被视为静态成员

[const](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/const)

`const` 修饰的字段的值在编译时就确定了

`const` 修饰的字段是编译传播，相当于在编译阶段提取常量的值，并将值嵌入IL代码中，生成的IL代码如下:

    IL_0001:  ldc.r8     3.1400000000000001

而 `readonly` 生成的IL代码如下：

    IL_0010:  ldsfld     float64 ConsoleApp8.Program::MaxAge


[readonly](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/readonly)

`readonly` 修饰的字段，只能在声明时或者在构造方法中赋值

类中的 `inline` 初始化语法实际是在构造器中对字段进行初始化的，它时一种语法上的简化

静态构造方法 -> 初始化静态字段

构造方法 -> 初始化非静态字段

类型对象是在类型加载到一个AppDomain时创建的