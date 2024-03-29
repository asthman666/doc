# C# 中的类

    Object -> System.String(sealed class)
    Object -> System.Console(static class)
    Object -> System.Random(class)
    Object -> System.Exception(class)
    Object -> System.Array(abstract class)
    
    Object -> ValueType(abstract class)
    
    Object -> ValueType -> System.Char(struct)
    Object -> ValueType -> System.Enum(class)
    Object -> ValueType -> Boolean(struct)
    Object -> ValueType -> System.Byte(struct)
    Object -> ValueType -> System.Int32(struct)
    Object -> ValueType -> System.Guid(struct)
    Object -> ValueType -> System.DateTime(struct)
    Object -> ValueType -> System.TimeSpan(struct)
    Object -> ValueType -> System.ValueTuple(struct)
    Object -> ValueType -> KeyValuePair<TKey,TValue>(struct)


* 所有的结构都是System.ValueType的直接派生类， System.ValueType又直接从System.Object派生

* 所有值类型都必须从System.Value派生

* 所有的枚举都从System.Enum派生

* 所有的数组继承System.Array，System.Array是类，所以int[], string[]继承System.Array，所以它们都是引用类型


> [Object](https://docs.microsoft.com/en-us/dotnet/api/system.object?view=netframework-4.7.2)
> [ValueType](https://docs.microsoft.com/en-us/dotnet/api/system.valuetype)
