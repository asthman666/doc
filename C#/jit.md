# JIT (Just-In-Time) Compiler IN .NET

在.NET框架中，所有的.NET语言使用一个CLR(Common Language Runtime)，它可以解决对每种编程语言安装单独的运行环境。当.NET CLR安装在一台电脑的时候，它可以执行任何兼容.NET的语言。在MSIL(Miscrosoft Intermediate Language)可以被执行之前，它必须被.NET框架的JIT(Just-In-Time)编译器转化为本地代码，那是一种和JIT编译器运行在同一个计算机体系上的CPU特定代码。

### JIT编译器

一个Web Service或者Web Forms文件必须被编译才可以在CLR上运行。编译可以是隐式的或者显式的。虽然你可以显式的调用合适的编译器来编译你的Web Service或者Web Forms文件，但是让这些文件被隐式的编译会更简单。当你通过HTTP-SOAP, HTTP-GET或者HTTP-POST请求.asmx，隐式编译会发生。分析器(xsp.exe)确定当前程序集的版本在内存还是磁盘中。如果不能使用已经存在的版本，分析器会对个别的编译器做出适当的调整。

当Web Service或者Web Forms文件被隐式的编译，它实际上编译了两次。第一次，它被编译成IL(Intermediate Language)。第二步，Web Service(现在是IL的一个程序集)被编译成机器语言。这个过程被叫做JIT编译，因为直到这个程序集放在目标机器上它才会发生。你不提前编译它以便你的系统和处理器的特定的JIT编译器可以被使用。结果就是这个程序集会被编译成针对特定配置的尽可能最快的机器语言。它也可以让你编译一次并且可以在任意操作系统运行。


### JIT如何工作的?

当MSIL需要被执行时，JIT会把MSIL转化并且把结果存储在本地代码里以便它可以被调用。

CLR还提供另外一种编译模式叫做install-time code generation。install-time code generate 模式会像JIT编译器一样转化MSIL到本地代码，但是它在一个时间转化大型的代码单元，存储本地代码结果以便以后加载调用使用。

### JIT 的类型

在.NET中有三种JIT编译器类型，如下：

- Pre-JIT COMPILER:

  在一次编译周期中编译所有的源码到本地代码。这个会在应用部署的时候完成

- Econo-JIT COMPILER:

  编译那些在运行过程中被调用的方法，但不存储编译结果。
 
- Normal-JIT COMPILER:

  编译那些在运行过程中被调用的方法，这些方法第一次被编译后会存储在缓存中。当下次相同的方法被再次调用，编译后的代码会从缓存中取出来。


> [just in time compiler](http://www.c-sharpcorner.com/uploadfile/nipuntomar/jit-just-in-time-compiler/)