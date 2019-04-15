# Model validation

## Model state

`Model state` 展现的错误来自两个子系统 `model binding` 和 `model validation`.

* `binding` 的错误通常是数据转换的错误。(例如，期望是整数，但是却输入了字符串)

* `Model validation`发生在`model binding`之后，并且当数据不符合商业规则是报错。(例如，期望数据是1-5，但是却输入了0)

* `Model binding and validation` 都发生在执行`controller action` 或者 `Razor Pages handler method` **之前**

> [validation](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation)