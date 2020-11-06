# out

	class Program
	{
		static void Main(string[] args)
		{
			if (int.TryParse("a", out int result))
			{
				Console.WriteLine(result);
			}
			else
			{
				Console.WriteLine(result);
			}

			if (int.TryParse("666", out int result2))
			{
				Console.WriteLine(result2);
			}
			else
			{
				Console.WriteLine(result2);
			}

			Console.ReadKey();
		}
	}

    // output:
    // 0
    // 666

NOTE: If you want to write one method that return multiple variables, you can use `out` keyword to implement it.

Example:

	using System;

	namespace ConsoleApp5
	{
		class Program
		{
			static void Main(string[] args)
			{
				var (_, count) = CharInString('a', "Hello");
				Console.WriteLine($"char 'a' in string \"Hello\" count: {count}");

				var (_, hcount) = CharInString('l', "Hello");
				Console.WriteLine($"char 'l' in string \"Hello\" count: {hcount}");

				if (CharInString('e', "Hello", out var testCount))
					Console.WriteLine($"char 'e' in string \"Hello\" count: {testCount}");
			}

			static (bool found, int count) CharInString(char c, string str)
			{
				var totalCount = 0;
				foreach ( var cc in str )
				{
					if (cc == c)
						totalCount++;
				}
				return (totalCount > 0 ? true : false, totalCount);
			}

			static bool CharInString(char c, string str, out int count)
			{
				count = 0;
				foreach (var cc in str)
				{
					if (cc == c)
						count++;
				}
				return count > 0 ? true : false;
			}

		}
	}

	// Output:
	// char 'a' in string "Hello" count: 0
	// char 'l' in string "Hello" count: 2
	// char 'e' in string "Hello" count: 1	

[out](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/out-parameter-modifier)