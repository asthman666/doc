# catch

* 当一个exception被抛出时，CLR会去寻找`catch`语句块去处理这个exception。 如果当前执行的方法没有包含可以处理这个exception的`catch`语句块，CLR会在调用当前方法的方法中去寻找，一直往调用栈的上层寻找。

* 如果没有`catch`语句块可以处理exception，CLR会显示一个未处理的异常信息给用户并且停止程序的运行。  

* `catch`可以不跟参数来捕获任意的异常，这种用法不推荐。通常，你应该仅仅捕获你知道怎么去恢复的异常。

* `catch`的顺序是优先更具体的exception。如果后面的`catch`永远不会执行，编译器会报错。


[throw](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/throw)

[exception-filters](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-6#exception-filters)