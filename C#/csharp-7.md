# csharp-7

1. `out` variables

        if (!int.TryParse(input, out var result))
        {
            return null;
        }

        return result;

2. [Tuple](https://docs.microsoft.com/en-us/dotnet/csharp/tuples)

    Tuples are most useful as return types for **private** and **internal** methods. Tuples provide a simple syntax for those methods to return multiple discrete values: You save the work of authoring a class or a struct that defines the type returned. There is no need for creating a new type.

    Using tuples in this way offers several advantages:

    You save the work of authoring a class or a struct that defines the type returned.
    You do not need to create new type.
    The language enhancements removes the need to call the Create<T1>(T1) methods.

    class Program
    {
        static (int Min, int Max) getMinMax(int[] numbers)
        {
            int min = int.MaxValue;
            int max = int.MinValue;
            foreach (var n in numbers)
            {
                min = (n < min) ? n : min;
                max = (n > max) ? n : max;
            }
            return (min, max);
        }

        static void Main(string[] args)
        {
            var letters = ("a", "b");
            Console.WriteLine($"{letters.Item1}");
            Console.WriteLine($"{letters.Item2}");

            var named = (Answer: 42, Message: "The meaning of life");
            Console.WriteLine($"{named.Answer}");
            Console.WriteLine($"{named.Message}");

            (string Alpha, string Beta) namedLetters = ("a", "b");
            Console.WriteLine($"{namedLetters.Alpha}");
            Console.WriteLine($"{namedLetters.Beta}");

            (int A, string M) = named;
            var minMax = getMinMax(new int[] { 1,2,3 });
            (int min, int max) = getMinMax(new int[] { 1,2,3 });

            Console.ReadKey();
        }
    }

3. [Discard](https://docs.microsoft.com/en-us/dotnet/csharp/discards)

        var named = (Answer: 42, Message: "The meaning of life");
        var (_,  M) = named;
        Console.WriteLine(M);
 
4. Pattern matching

5. Ref locals and returns

rel locals和ref returns避免了拷贝值或者多次的解除引用的操作，可以让算法更有效。

    public static (int i, int j) Find(int[,] matrix, Func<int, bool> predicate)
    {
        for (int i = 0; i < matrix.GetLength(0); i++)
            for (int j = 0; j < matrix.GetLength(1); j++)
                if (predicate(matrix[i, j]))
                    return (i, j);
        return (-1, -1); // Not found
    }

    var indices = MatrixSearch.Find(matrix, (val) => val == 42);
    Console.WriteLine(indices);
    matrix[indices.i, indices.j] = 24;

优化为：

    public static ref int Find3(int[,] matrix, Func<int, bool> predicate)
    {
        for (int i = 0; i < matrix.GetLength(0); i++)
            for (int j = 0; j < matrix.GetLength(1); j++)
                if (predicate(matrix[i, j]))
                    return ref matrix[i, j];
        throw new InvalidOperationException("Not found");
    }
    
    ref var item = ref MatrixSearch.Find3(matrix, (val) => val == 42);
    Console.WriteLine(item);
    item = 24;
    Console.WriteLine(matrix[4, 2]);    

6. Local functions

7. More expression-bodied members

        // Expression-bodied constructor
        public ExpressionMembersExample(string label) => this.Label = label;

        // Expression-bodied finalizer
        ~ExpressionMembersExample() => Console.Error.WriteLine("Finalized!");

        private string label;

        // Expression-bodied get / set accessors.
        public string Label
        {
            get => label;
            set => this.label = value ?? "Default label";
        }
8. Throw expressions

        private ConfigResource loadedConfig = LoadConfigResourceOrDefault() ?? 
            throw new InvalidOperationException("Could not load config");

    Previously：

        public ApplicationOptions()
        {
            loadedConfig = LoadConfigResourceOrDefault();
            if (loadedConfig == null)
                throw new InvalidOperationException("Could not load config");
        }    

9. Generalized async return types

10. Numeric literal syntax improvements

    误读数字常量会使第一次阅读时更难理解代码。C＃7.0包含两个新功能，可以更容易地以最易读的方式编写数字以用于预期用途。

    binary literals

        public const int One =  0b0001;
        public const int Two =  0b0010;
        public const int Four = 0b0100;

    digit separators

        public const int Sixteen =   0b0001_0000;
        public const int ThirtyTwo = 0b0010_0000;        
        public const long BillionsAndBillions = 100_000_000_000;
        public const double AvogadroConstant = 6.022_140_857_747_474e23;

[csharp-7](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-7)