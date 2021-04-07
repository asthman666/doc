The `lock` statement obtains the mutual-exclusion lock for a given object, executes a statement, and then releases the lock.

**IL code:**

    .method private hidebysig static void  Main(string[] args) cil managed
    {
    .entrypoint
    // Code size       45 (0x2d)
    .maxstack  2
    .locals init (object V_0,
            bool V_1)
    IL_0000:  nop
    IL_0001:  ldsfld     object ConsoleApp14.Program::o
    IL_0006:  stloc.0
    IL_0007:  ldc.i4.0
    IL_0008:  stloc.1
    .try
    {
        IL_0009:  ldloc.0
        IL_000a:  ldloca.s   V_1
        IL_000c:  call       void [System.Threading]System.Threading.Monitor::Enter(object,
                                                                                    bool&)
        IL_0011:  nop
        IL_0012:  nop
        IL_0013:  ldstr      "Hello World!"
        IL_0018:  call       void [System.Console]System.Console::WriteLine(string)
        IL_001d:  nop
        IL_001e:  nop
        IL_001f:  leave.s    IL_002c
    }  // end .try
    finally
    {
        IL_0021:  ldloc.1
        IL_0022:  brfalse.s  IL_002b
        IL_0024:  ldloc.0
        IL_0025:  call       void [System.Threading]System.Threading.Monitor::Exit(object)
        IL_002a:  nop
        IL_002b:  endfinally
    }  // end handler
    IL_002c:  ret
    } // end of method Program::Main
