# Open–closed principle

software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification

开放关闭原则有两种使用方法，继承或者委托。

* 如果一个模块仍然可以扩展，那么它是开放的。
* 如果一个模块被别的模块使用，那么它是关闭的。

一个类是关闭的，因为它可能被编译，存储在程序集，并且被客户端类使用。但是，它也是开放的，因为任何新的类可以继承它，添加新的功能。当一个新的继承类被定义，不需要改东原始类或者分发到它的客户端。

## 多态 open/closed principle

现存接口是关闭的，不许修改的。新的实现必须实现这个接口。

> [Open–closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle)



