# extern

The extern modifier is used to declare a method that is implemented externally. A common use of the extern modifier is with the **DllImport** attribute when you are using Interop services to call into **unmanaged code**.

    class Program
    {
        [DllImport("User32.dll", CharSet = CharSet.Unicode)]
        public static extern int MessageBox(IntPtr h, string m, string c, int type);

        static int Main()
        {
            string myString;
            Console.Write("Enter your message: ");
            myString = Console.ReadLine();
            return MessageBox((IntPtr)0, myString, "My Message Box", 0);
        }
    }

> [extern](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/extern)