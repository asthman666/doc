## .NET 5 = .NET Core vNext

.NET 5 is the next step forward with .NET Core. The project aims to improve .NET in a few key ways:

* 创建一个单独的.NET运行时和框架，可以在任何地方使用，并且有统一的运行行为和开发体验
* 通过使用 .NET Core, .NET Framework, Xamarin和Mono来扩展.NET的能力
* 微软和社区的开发人员可以一起在a single code-base(.NET 5)上工作，可以提升所有的方案

每个APP都有相同的工程文件，相同的运行时，API和语言能力

## 版本

### Release Candidate (RC)

发布候选

### Release to manufacturing (RTM)

The term release to manufacturing (RTM), also known as "going gold", is a term used when a software product is ready to be delivered.

### General availability (GA)

General availability (GA) is the marketing stage at which all necessary commercialization activities have been completed and a software product is available for purchase, depending, however, on language, region, electronic vs. media availability.

### Release to web (RTW)

Release to the web (RTW) or web release is a means of software delivery that utilizes the Internet for distribution.

### Long Term Support (LTS)

2019.7 => .NET Core 3.0(RC)

2019.9 => .NET Core 3.0(GA)

2019.11 => .NET Core 3.1(LST)

2020.11 => .NET 5.0(GA)

2021.11 => .NET 6.0(LTS)

2022.11 => .NET 7.0(GA)

2023.11 => .NET 8.0(LTS)

每年十一月发布一个.NET主要版本

大部分 .NET 5的工作默认还是使用JIT-based CoreCLR运行时

**CoreFX** is the foundational class libraries for .NET Core. It includes types for collections, file systems, console, JSON, XML, async and many others. 

All .NET 5 applications will use the CoreFX framework. 

**.NET Framework 4.8** will be the **last major version** of **.NET Framework**

> [introducing-net-5](https://devblogs.microsoft.com/dotnet/introducing-net-5/)

> [net-core-is-the-future-of-net](https://devblogs.microsoft.com/dotnet/net-core-is-the-future-of-net/)

> [corefx](https://github.com/dotnet/corefx)