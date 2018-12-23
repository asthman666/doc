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

    模式匹配支持 `is` expressions和 `switch` expressions. 它们会激活分析一个对象及对象的属性来决定这个对象是否满足查找的对象。你可以使用`when`关键字来给这个匹配指定更多的规则。

        class Program
        {
            public static int DiceSum2(IEnumerable<object> values)
            {
                var sum = 0;
                foreach (var item in values)
                {
                    if (item is int val)
                        sum += val;
                    else if (item is IEnumerable<object> subList)
                        sum += DiceSum2(subList);
                }
                return sum;
            }

            static void Main(string[] args)
            {
                var sum = DiceSum2(new object[] { 1, 2, new object[] { 3, 4 } });
                Console.WriteLine(sum);
                Console.ReadKey();
            }
        }

        当你需要扩展DiceSum2时，你可能会用更多的`if`和`else if`语句。这样不是很好。所以我们可以使用`switch`。

        public static int DiceSum3(IEnumerable<object> values)
        {
            var sum = 0;
            foreach (var item in values)
            {
                switch (item)
                {
                    case int val:
                        sum += val;
                        break;
                    case IEnumerable<object> subList:
                        sum += DiceSum3(subList);
                        break;
                }
            }
            return sum;
        }

        我们可以继续改进：

        public static int DiceSum4(IEnumerable<object> values)
        {
            var sum = 0;
            foreach (var item in values)
            {
                switch (item)
                {
                    case 0:
                        break;
                    case int val:
                        sum += val;
                        break;
                    case IEnumerable<object> subList when subList.Any():
                        sum += DiceSum4(subList);
                        break;
                    case IEnumerable<object> subList:
                        break;
                    case null:
                        break;
                    default:
                        throw new InvalidOperationException("unknown item type");
                }
            }
            return sum;
        }        

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

    Many designs for classes include methods that are called from only one location. These additional private methods keep each method small and focused. However, they can make it harder to understand a class when reading it the first time. These methods must be understood outside of the context of the single calling location.

    For those designs, local functions enable you to declare methods inside the context of another method. This makes it easier for readers of the class to see that the local method is only called from the context in which is it declared.

    There are two very common use cases for local functions: public iterator methods and public async methods. Both types of methods generate code that reports errors later than programmers might expect. In the case of iterator methods, any exceptions are observed only when calling code that enumerates the returned sequence. In the case of async methods, any exceptions are only observed when the returned Task is awaited.

        public static IEnumerable<char> AlphabetSubset(char start, char end)
        {
            if (start < 'a' || start > 'z')
                throw new ArgumentOutOfRangeException(paramName: nameof(start), message: "start must be a letter");
            if (end < 'a' || end > 'z')
                throw new ArgumentOutOfRangeException(paramName: nameof(end), message: "end must be a letter");

            if (end <= start)
                throw new ArgumentException($"{nameof(end)} must be greater than {nameof(start)}");
            for (var c = start; c < end; c++)
                yield return c;
        }

    改变为：

        public static IEnumerable<char> AlphabetSubset3(char start, char end)
        {
            if (start < 'a' || start > 'z')
                throw new ArgumentOutOfRangeException(paramName: nameof(start), message: "start must be a letter");
            if (end < 'a' || end > 'z')
                throw new ArgumentOutOfRangeException(paramName: nameof(end), message: "end must be a letter");

            if (end <= start)
                throw new ArgumentException($"{nameof(end)} must be greater than {nameof(start)}");

            return alphabetSubsetImplementation();

            IEnumerable<char> alphabetSubsetImplementation()
            {
                for (var c = start; c < end; c++)
                    yield return c;
            }
        }        

    `async` method:

        public Task<string> PerformLongRunningWork(string address, int index, string name)
        {
            if (string.IsNullOrWhiteSpace(address))
                throw new ArgumentException(message: "An address is required", paramName: nameof(address));
            if (index < 0)
                throw new ArgumentOutOfRangeException(paramName: nameof(index), message: "The index must be non-negative");
            if (string.IsNullOrWhiteSpace(name))
                throw new ArgumentException(message: "You must supply a name", paramName: nameof(name));

            return longRunningWorkImplementation();

            async Task<string> longRunningWorkImplementation()
            {
                var interimResult = await FirstWork(address);
                var secondResult = await SecondStep(index, name);
                return $"The results are {interimResult} and {secondResult}. Enjoy.";
            }
        }    

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

    Returning a Task object from async methods can introduce performance bottlenecks in certain paths. Task is a reference type, so using it means allocating an object. In cases where a method declared with the async modifier returns a cached result, or completes synchronously, the extra allocations can become a significant time cost in performance critical sections of code. It can become very costly if those allocations occur in tight loops.

    The new language feature means that async methods may return other types in addition to Task, Task<T> and void. The returned type must still satisfy the async pattern, meaning a GetAwaiter method must be accessible. As one concrete example, the ValueTask type has been added to the .NET framework to make use of this new language feature:

        public async ValueTask<int> Func()
        {
            await Task.Delay(100);
            return 5;
        }

    A simple optimization would be to use ValueTask in places where Task would be used before. However, if you want to perform extra optimizations by hand, you can cache results from async work and reuse the result in subsequent calls. The ValueTask struct has a constructor with a Task parameter so that you can construct a ValueTask from the return value of any existing async method:

        public ValueTask<int> CachedFunc()
        {
            return (cache) ? new ValueTask<int>(cacheResult) : new ValueTask<int>(LoadCache());
        }
        private bool cache = false;
        private int cacheResult;
        private async Task<int> LoadCache()
        {
            // simulate async work:
            await Task.Delay(100);
            cacheResult = 100;
            cache = true;
            return cacheResult;
        }    

    As with all performance recommendations, you should benchmark both versions before making large scale changes to your code.

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