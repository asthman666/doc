# 程序集加载和反射

JIT 编译器将方法的IL 代码编译成本机代码时，会查看IL 代码中引用了哪些类型。JIT 编译器利用程序集的 TypeRef 和 AssemblyRef 元数据表来确定哪一个程序集定义了所引用的类型。

在内部，CLR 使用System.Reflection.Assembly 类的静态Load 方法尝试加载程序集到AppDomain 中。

Load 导致CLR 向程序集应用一个版本绑定重定向策略，并在[GAC](https://docs.microsoft.com/en-us/dotnet/framework/app-domains/gac) 中查找程序集。如果没有找到，就接着去应用程序的基目录，私有路径子目录和codebase位置查找。如果调用的时候传递的是弱命名程序集，Load就不会向程序集应用版本绑定重定向策略，CLR也不会去GAC查找程序集。

