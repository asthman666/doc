A `delegate` is a type that defines a method signature. 

    public delegate int PerformCalculation(int x, int y);

When you instantiate a delegate, you can associate its instance with any method with a compatible signature. You can invoke (or call) the method through the delegate instance.

    PerformCalculation p = delegate (int x, int y) { return x + y; };
    int i = p(1, 2); // i will be 3

Any method from any accessible class or struct that matches the delegate's signature, which consists of the return type and parameters, can be assigned to the delegate. The method can be either static or an instance method. **This makes it possible to programmatically change method calls, and also plug new code into existing classes**.

**In the context of method overloading, the signature of a method does not include the return value. But in the context of delegates, the signature does include the return value. In other words, a method must have the same return value as the delegate.**

[Anonymous Functions](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-functions)

[Lambda expressions](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)

A lambda expression is an anonymous function that you can use to create "delegates" or "expression tree" types.

Assign expression to a delegate type:

    delegate int del(int i);  
    static void Main(string[] args)  
    {  
        del myDelegate = x => x * x;  
        int j = myDelegate(5); //j = 25  

        Func<int, int> Calculate = x => x + x;
        int i = Calculate(3); //i = 6
    }  

To create an expression tree type:

using System.Linq.Expressions;  
  
    namespace ConsoleApplication1  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                Expression<del> myET = x => x * x;  
                int j = myET.Compile()(5); //j = 25

                Expression<Func<int, int>> Calculate = x => x + x;
                int i = Calculate.Compile()(3); //i = 6
            }  
        }  
    }

[Expression Trees](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/expression-trees/index)

Expression trees represent code in a tree-like data structure, where each node is an expression.

You can compile and run code represented by expression trees.

    // Creating an expression tree.  
    Expression<Func<int, bool>> expr = num => num < 5;  

    // Compiling the expression tree into a delegate.  
    Func<int, bool> result = expr.Compile();  

    // Invoking the delegate and writing the result to the console.  
    Console.WriteLine(result(4));  

Expression trees are also used in the dynamic language runtime (DLR) to provide interoperability between dynamic languages and the .NET Framework and to enable compiler writers to emit expression trees instead of Microsoft intermediate language (MSIL).

