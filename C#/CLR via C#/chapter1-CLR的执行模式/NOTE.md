## 将源代码编译成托管模块

[CLR version](https://docs.microsoft.com/en-us/dotnet/standard/clr#clr-versions)

CLR (Common Language Runtime)是一个可由多种编程语言使用的"运行时"

只要编译器是面向CLR的，就可以用CLR运行

编译器是语法检查器和"正确代码"分析器，并输出托管模块

编译器生成的托管模块是标准的windows可移植执行体（PE32）文件，或者是标准的64位windows可移植体（PE32+）文件，它们都需要CLR才能执行

### 托管模块的各个部分

1. PE32或者PE32头

    标准windows PE文件头，如果这个头使用PE32格式，文件能在windows 32位或者64位版本上运行。如果这个头使用PE32+格式，文件只能在windows 的64位版本上运行。

2. CLR 头

    包含要求的CLR版本，托管模块入口方法的MethodDef元数据token以及模块的元数据，资源，强名称等的位置和大小

3. 元数据

    元数据表，一种表描述源代码中定义的类型和成员，另一种描述源代码引用的类型和成员

4. IL 代码

    编译器编译源代码时生成的代码，在运行时，CLR将IL编译成本机的指令

### PE 文件转换出IL语言

[ildasm](/doc/C%23/Develop Command/ildasm.exe)

### IL 语言转为 PE 文件

[ilasm](/doc/C%23/Develop Command/ilasm.exe)

### 元数据的用途

* Visual Studio 的 IntelliSense 技术解析元数据，告诉你一个类型提供了那些方法，属性，事件和字段。对于方法，还能告诉你需要的参数。

* ...

## 将托管模块合并为程序集

CLR实际和程序集工作， assembly是一个或多个模块/资源的逻辑性分组。

C# 编译器生成的是含有清单的托管模块，对于只有一个托管模块而无资源文件的项目，程序集就是托管模块，生成过程中无需执行任何额外的步骤。但是，如果希望将一组文件合并到程序集中，就必须掌握更多的工具（AL.exe）。

程序集可以**自描述**， 也就是说，CLR能判断为了执行程序集中的代码，程序集的直接依赖对象是什么。

程序集可以是可执行应用程序，也可以是DLL

## 加载公共语言运行时

`CLRVer.exe`可以列出机器上安装的所有的CLR的版本，还能列出机器中正在运行的进程使用的CLR的版本

windows检查EXE文件头，决定是创建32位还是64位进程后，会在进程地址空间加载MSCorEE.dll的x86，x64或者ARM版本。然后，进程的主线程调用MSCorEE.dll中定义的一个方法。这个方法初始化CLR，加载EXE程序集，再调用其入口方法（Main）。随即，托管应用程序启动并运行。

## 执行程序集的代码

C#编译器开关

`/optimize`

`/debug` 指定/debug(+full/pdbonly)开关，编译器才会生成Program Database(PDB)文件. PDB文件帮助调试器查找局部变量并将IL指令映射到源代码.

Visual Studio默认是 `+full`，有选项可以配置

为了执行方法，首先必须把方法的IL转换成本机CPU指令，这是CLR的JIT编译器的职责

JIT 编译器将本机CPU指令存储到动态内存中。这意味着一旦应用程序终止，编译好的代码也会被丢弃

## Framework类库

部分常规的FCL的命名空间

* **System**  包含每个应用程序都要用到的所有的基本类型
* **System.Data** 包含用于和数据库通信以及处理数据的类型
* **System.IO** 包含用于执行流I/O以及浏览目录/文件的类型
* **System.Net** 包含进行低级网路通信，并与一些常用的Internet协议协作的类型
* **System.Security** 包含用户保护数据和资源的类型
* **System.Text** 包含处理各种编码文本的类型
* **System.XML** 包含用户处理XML架构和数据的类型
* **System.Threading** 包含用于异步操作和同步资源访问的类型

## 通用类型系统

[CTS Common Type System](https://docs.microsoft.com/en-us/dotnet/standard/base-types/common-type-system)

## 公共语言规范

CLS Common Language Specification

CLR/CTS提供了一个功能集，如果开发人员用IL汇编语言写程序，可以使用CLR/CTS提供的全部功能。但是，其他大多数语言（C#，VB和Fortran）只向开发人员公开了CLR/CTS的一个功能自己。CLS定义了所有语言都必须支持的最小功能集。

`[assembly: CLSCompliant(true)]` 应用于程序集，告诉编译器检查其中的任何公开类型，确保构造的类型可以从其他编程语言中访问

## 与非托管代的互操作性

* 托管代码能调用DLL中的非托管函数

例如，C#应用程序可调用从Kernel32.dll到处的CreateSemapore函数

* 托管代码可以使用现有的COM组件（服务器）

* 非托管代码可以使用托管类型（服务器）
