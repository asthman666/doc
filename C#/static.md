[Static class and static class members](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)

### static class 

* A static class is basically the same as a non-static class, but there is one difference: a static class cannot be instantiated.

* A static class can be used as a convenient container for sets of methods that just operate on input parameters and do not have to get or set any internal **instance** fields. For example, `System.Match` class is a static class.

* A static constructor is only called one time, and a static class remains in memory for the lifetime of the application domain in which your program resides.

* Creating a static class is therefore basically the same as creating a class that contains only static members and a private constructor.

  The advantage of using a static class is that the compiler can check to make sure that no instance members are accidentally added.

* Static classes are sealed and therefore cannot be inherited.

* Non-static classes should also define a static constructor if the class contains static members that require non-trivial initialization.

  Contains only static members.

  Cannot contain Instance Constructors. However, they can contain a static constructor.

### Static Members

* Two common uses of static fields are to keep a count of the number of objects that have been instantiated, or to store a value that must be shared among all instances.

* Static methods can be overloaded but not overridden, because they belong to the class, and not to any instance of the class.

* `const` fields can be accessed by using the same ClassName.MemberName

* C# does not support static local variables (variables that are declared in method scope).

* Static members are initialized before the static member is accessed for the first time and before the static constructor, if there is one, is called.

* A call to a static method generates a call instruction in Microsoft intermediate language (MSIL), whereas a call to an instance method generates a `callvirt` instruction, which also checks for a null object references. However, most of the time the performance difference between the two is not significant.

[const](https://stackoverflow.com/questions/408192/why-cant-i-have-public-static-const-string-s-stuff-in-my-class)

* A const object is always **static**. The `static` modifier is not allowed in a constant declaration.

* A constant can participate in a constant expression.

        public const int c1 = 5;
        public const int c2 = c1 + 100;

* The `readonly` keyword differs from the `const` keyword. A `const` field can only be initialized at the declaration of the field. A `readonly` field can be initialized either at the declaration or in a constructor. Therefore, `readonly` fields can have **different values** depending on the constructor used. Also, although a `const` field is a **compile-time** constant, the readonly field can be used for **run-time** constants, as in this line: `public static readonly uint l1 = (uint)DateTime.Now.Ticks;`

[Extension Methods](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)

* Extension methods are a special kind of **static method**, but they are called as if they were instance methods on the extended type.

* Extension methods are only in scope when you explicitly import the namespace into your source code with a `using` directive.

* Extension methods must be defined inside a non-nested, non-generic **static class**.

* The intermediate language (IL) generated by the compiler translates your code into a call on the static method. Therefore, the principle of encapsulation is not really being violated. In fact, extension methods cannot access private variables in the type they are extending.

* You can use extension methods to extend a **class** or **interface**, but not to override them. An extension method with the same name and signature as an interface or class method will never be called. At compile time, extension methods always have lower priority than instance methods defined in the type itself.

### If you do implement extension methods for a given type, remember the following points:

1. An extension method will never be called if it has the same signature as a method defined in the type.

2. Extension methods are brought into scope at the namespace level. For example, if you have multiple static classes that contain extension methods in a single namespace named Extensions, they will all be brought into scope by the `using Extensions;` directive.