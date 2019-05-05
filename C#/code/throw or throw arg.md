# throw or throw arg

    class Program
    {
        static void Method1(int i)
        {
            try
            {
                Method2(i);
            }
            catch ( Exception e)
            {
                throw;
                // throw e;
            }
        }

        static int Method2(int i)
        {
            return 5 / i;
        }


        static void Main(string[] args)
        {
            try
            {
                Method1(0);
            }
            catch (Exception e)
            {
                Console.WriteLine(e.StackTrace);
            }
        }
    }

当使用 `throw` 时，可以跟踪到 `5 / i`, 打印出:

    at ConsoleApp6.Program.Method2(Int32 i) in C:\Users\nsong\source\repos\ConsoleApp6\ConsoleApp6\Program.cs:line 25
    at ConsoleApp6.Program.Method1(Int32 i) in C:\Users\nsong\source\repos\ConsoleApp6\ConsoleApp6\Program.cs:line 19
    at ConsoleApp6.Program.Main(String[] args) in C:\Users\nsong\source\repos\ConsoleApp6\ConsoleApp6\Program.cs:line 33

当使用 `throw e` 时，不可以跟踪到 `5 / i`, 打印出:

    at ConsoleApp6.Program.Method1(Int32 i) in C:\Users\nsong\source\repos\ConsoleApp6\ConsoleApp6\Program.cs:line 19
    at ConsoleApp6.Program.Main(String[] args) in C:\Users\nsong\source\repos\ConsoleApp6\ConsoleApp6\Program.cs:line 33

> [CA2200 rethrow preserve stack details](https://docs.microsoft.com/en-us/visualstudio/code-quality/ca2200-rethrow-to-preserve-stack-details?)    