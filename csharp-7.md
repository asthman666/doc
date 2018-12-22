# csharp-7

1. `out` variables

        if (!int.TryParse(input, out var result))
        {
            return null;
        }

        return result;

2. [Tuple](https://docs.microsoft.com/en-us/dotnet/csharp/tuples)

    Tuples are most useful as return types for private and internal methods. Tuples provide a simple syntax for those methods to return multiple discrete values: You save the work of authoring a class or a struct that defines the type returned. There is no need for creating a new type.

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

[csharp-7](https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-7)