# nullable

[nullable types](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/nullable-types/)

* `Nullable<T>` is a struct

    defined:

        public struct Nullable<T> where T : struct

* [C# 7.0 pattern matching](csharp-7#4)

    exmaple:

        int? x = 3;
        int y = 0; 
        if (x is int valueOfX)
            y = valueOfX;

* GetValueOrDefault

    return either the assigned value, or the [default value](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/default-values-table) of the underlying value type if the value of the nullable type is null

    exmaple:

        int? x = 3;
        int y = x.GetValueOrDefault(); // y will be 3

        int? m = null;
        int n = x.GetValueOrDefault(); // n will be 0

* GetValueOrDefault(T) 

    return either the assigned value, or the provided default value if the value of the nullable type is null

    exmaple:

        int? x = 1;
        int y = x.GetValueOrDefault(3); // y will be 1

        int? m = null;
        int y = x.GetValueOrDefault(3); // y will be 3


[default value](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/default-values-table)

* Use the `default` operator to produce the default value of a type

    exmaple:

        int a = default(int);

    Beginning with C# 7.1:

        int a = default;