1. There is a method return `Task<T>`. Why sometimes can return `T` directly, sometimes have to return `Task.FromResult()`

    When use the `async` modifier to specify that a method. The body of the method will be passed into `System.Runtime.CompilerServices.AsyncTaskMethodBuilder::Create()` and return `System.Runtime.CompilerServices.AsyncTaskMethodBuilder<T>::get_Task()`, the method will return a `Task<T>`, `Task` or `void` and you just need to `return T` in the method.

    If a method return `Task<T>` but don't use `async` modifier, it means you need to manually return `Task<T>`, we can use `Task.FromResult()` to return a completed task.

NOTE: 
    If the method that the async keyword modifies doesn't contain an `await` expression or statement, the method executes synchronously. A compiler warning alerts you to any async methods that don't contain `await` statements, because that situation might indicate an error.

> [async](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/async)

> [no await warning cs4014](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-messages/cs4014)

> [async and await](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await)

> [async-main](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-7.1/async-main)

> [async main console app](https://stackoverflow.com/questions/9208921/cant-specify-the-async-modifier-on-the-main-method-of-a-console-app)

> [await](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/await)