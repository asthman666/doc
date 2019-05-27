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