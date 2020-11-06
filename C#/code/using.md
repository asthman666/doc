Code:

    class Program
    {
        static void Main(string[] args)
        {
            using (var file = new FileStream(@"C:\test\aaa.txt", FileMode.Open))
            {
                var zero = returnZero();
                var x = 5 / zero; // will throw exception here

                Console.WriteLine("using inside");  // will no output      
            }

            Console.WriteLine("using outside"); // will no output
        }


        static int returnZero()
        {
            return 0;
        }
    }

Same as:

    var file = new FileStream(@"C:\test\aaa.txt", FileMode.Open);
    try {
        var zero = returnZero();
        var x = 5 / zero; // no catch, so will throw exception here

        Console.WriteLine("using inside");
    }   
    finally {
        file?.Dispose();
    } 

IL Code:

    .method private hidebysig static void  Main(string[] args) cil managed
    {
    .entrypoint
    // Code size       61 (0x3d)
    .maxstack  2
    .locals init (class [System.Runtime]System.IO.FileStream V_0,
            int32 V_1,
            int32 V_2)
    IL_0000:  nop
    IL_0001:  ldstr      "C:\\test\\aaa.txt"
    IL_0006:  ldc.i4.3
    IL_0007:  newobj     instance void [System.Runtime]System.IO.FileStream::.ctor(string,
                                                                                    valuetype [System.Runtime]System.IO.FileMode)
    IL_000c:  stloc.0
    .try
    {
        IL_000d:  nop
        IL_000e:  call       int32 ConsoleApp19.Program::returnZero()
        IL_0013:  stloc.1
        IL_0014:  ldc.i4.5
        IL_0015:  ldloc.1
        IL_0016:  div
        IL_0017:  stloc.2
        IL_0018:  ldstr      "using inside"
        IL_001d:  call       void [System.Console]System.Console::WriteLine(string)
        IL_0022:  nop
        IL_0023:  nop
        IL_0024:  leave.s    IL_0031
    }  // end .try
    finally
    {
        IL_0026:  ldloc.0
        IL_0027:  brfalse.s  IL_0030
        IL_0029:  ldloc.0
        IL_002a:  callvirt   instance void [System.Runtime]System.IDisposable::Dispose()
        IL_002f:  nop
        IL_0030:  endfinally
    }  // end handler
    IL_0031:  ldstr      "using outside"
    IL_0036:  call       void [System.Console]System.Console::WriteLine(string)
    IL_003b:  nop
    IL_003c:  ret
    } // end of method Program::Main

[try-finally](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/try-finally)