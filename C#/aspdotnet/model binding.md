# Model binding

MVC 会从request的不同的部分binding数据，并且按照以下顺序：

1. Form values: These are form values that go in the HTTP request using the POST method. (including jQuery POST requests).

2. Route values: The set of route values provided by Routing

3. Query strings: The query string part of the URI.

当一个参数被绑定，`model binding` 停止绑定这个参数并且继续帮顶下一个参数。

为了使模块可以绑定，这个类必须有一个公开的默认构造函数和公开的可写的属性。当`model binding`发生，使用类的公开的默认构造函数实例化，然后设置属性。

> [model binding](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/model-binding)