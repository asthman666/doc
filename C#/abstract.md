# Abstract

## 抽象类的特性:

* 抽象类不能被实例化

* 抽象类**可能**包含抽象方法和属性

* 抽象类不能用sealed修饰，因为sealed表明这个类不能被继承

* 一个非抽象类继承抽象类必须实现所有的继承的抽象方法和属性

System.Web.Mvc 命名空间 中的 Controller 类就是一个抽象类，但是它没有抽象成员，这样做的目的是你不能实例化这个类

## 抽象方法和属性

* 抽象方法默认是一个 `virtual` 方法

* 抽象方法只能在抽象类中声明

* 抽象方法没有实现，所以没有方法体， 例如：

    public abstract void MyMethod();  

* 抽象属性的定义

    public abstract string MyProperty { get; }

> [code example](code/abstract)    

* 实现抽象方法用 `override`

* 抽象方法不能用 `static` 或者 `virtual` 修饰

## 抽象类和接口

选择抽象类而不是接口的原因是你可以提供一些基本的实现

> [abstract](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/abstract)

> [abstract-class-without-any-abstract-method](https://stackoverflow.com/questions/3439158/abstract-class-without-any-abstract-method)