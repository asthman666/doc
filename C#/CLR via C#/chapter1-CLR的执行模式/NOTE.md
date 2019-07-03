CLR (Common Language Runtime)是一个可由多种编程语言使用的"运行时"

只要编译器是面向CLR的，就可以用CLR运行

编译器是语法检查器和"正确代码"分析器，并输出托管模块

编译器生成的托管模块是标准的windows可移植执行体（PE32）文件，或者是标准的64位windows可移植体（PE32+）文件，它们都需要CLR才能执行

## 执行程序集的代码

C#编译器开关

`/optimize` 

`/debug` 指定/debug(+full/pdbonly)开关，编译器才会生成Program Database(PDB)文件. PDB文件帮助调试器查找局部变量并将IL指令映射到源代码.

Visual Studio默认是 `+full`，有选项可以配置

