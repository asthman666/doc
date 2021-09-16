## Is the Type or Method Open or Closed?

A generic type or method is closed if instantiable types have been substituted for all its type parameters, including all the type parameters of all enclosing types. You can only create an instance of a generic type if it is closed. 

## Generating Closed Generic Types

Once you have a generic type or method definition, use the MakeGenericType method to create a closed generic type or the MakeGenericMethod method to create a MethodInfo for a closed generic method.

> [reflection-and-generic-types](https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/reflection-and-generic-types)

> [Autofac](https://github.com/autofac/Autofac)