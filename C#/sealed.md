
[sealed](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/sealed)

* When applied to a class, the sealed modifier prevents other classes from inheriting from it. For example, `System.String` class is a sealed class.

* You can also use the `sealed` modifier on a method or property that overrides a `virtual` method or property in a base class. This enables you to allow classes to derive from your class and prevent them from overriding specific virtual methods or properties. When you define new methods or properties in a class, you can prevent deriving classes from overriding them by not declaring them as virtual.

* It is an error to use the abstract modifier with a sealed class, because an abstract class must be inherited by a class that provides an implementation of the abstract methods or properties.

* When applied to a method or property, the `sealed` modifier must always be used with `override`.

* Because structs are implicitly sealed, they cannot be inherited.
