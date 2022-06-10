## for

The `for` statement executes a statement or a block of statements while a specified Boolean expression evaluates to true. 

    // i < 3 is the specified Boolean expression
    // Console.Write(i) is a statement or a block of statements
    for (int i = 0; i < 3; i++)
    {
        Console.Write(i);
    }    

## foreach

The `foreach` statement executes a statement or a block of statements for each element in an instance of the type that implements the `System.Collections.IEnumerable` or `System.Collections.Generic.IEnumerable<T>` interface

    var fibNumbers = new List<int> { 0, 1, 1, 2, 3, 5, 8, 13 };
    foreach (int element in fibNumbers)
    {
        Console.Write($"{element} ");
    }

## System.Linq Namespace

Provides classes and interfaces that support queries that use Language-Integrated Query (LINQ).

The System.Linq namespace is in the System.Core assembly (in System.Core.dll).

The `Enumerable` class contains LINQ standard query operators that operate on objects that implement `IEnumerable<T>`.

The `Queryable` class contains LINQ standard query operators that operate on objects that implement `IQueryable<T>`.

## indexer

Indexers are a syntactic convenience that enable you to create a class, struct, or interface that client applications can access as an array. Indexers are most frequently implemented in types whose primary purpose is to **encapsulate an internal collection or array**. 

For example, suppose you have a class TempRecord that represents the temperature in Fahrenheit as recorded at 10 different times during a 24-hour period. The class contains a temps array of type float[] to store the temperature values. By implementing an indexer in this class, clients can access the temperature in a TempRecord instance as `float temp = tempRecord[4]` instead of as `float temp = tempRecord.temps[4]`. 

    public class TempRecord
    {
        // Array of temperature values
        float[] temps = new float[10]
        {
            56.2F, 56.7F, 56.5F, 56.9F, 58.8F,
            61.3F, 65.9F, 62.1F, 59.2F, 57.5F
        };

        // To enable client code to validate input
        // when accessing your indexer.
        public int Length => temps.Length;
        
        // Indexer declaration.
        // If index is out of range, the temps array will throw the exception.
        public float this[int index]
        {
            get => temps[index];
            set => temps[index] = value;
        }
    }    

## Using for to iterate the IList

Because of the `IList` interface has the `T this[int index] { get; set; }` method, the class that implements the `IList` can be accessed by the indexer and can be iterated by the `for` keyword.

