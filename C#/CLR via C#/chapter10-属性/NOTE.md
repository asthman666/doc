## 匿名类型

    static void Main(string[] args)
    {
        var o = new { Name = "Noah", Age = 12 };

        string Name = "Beata";
        int Age = 12;
        var o2 = new { Name, Age };

        o = o2;
        Console.WriteLine(o.Name);
        Console.ReadKey();
    }

IL 代码:

    .method private hidebysig static void  Main(string[] args) cil managed
    {
    .entrypoint
    // Code size       52 (0x34)
    .maxstack  2
    .locals init ([0] class '<>f__AnonymousType0`2'<string,int32> o,
            [1] string Name,
            [2] int32 Age,
            [3] class '<>f__AnonymousType0`2'<string,int32> o2)
    IL_0000:  nop
    IL_0001:  ldstr      "Noah"
    IL_0006:  ldc.i4.s   12
    IL_0008:  newobj     instance void class '<>f__AnonymousType0`2'<string,int32>::.ctor(!0,
                                                                                            !1)
    IL_000d:  stloc.0
    IL_000e:  ldstr      "Beata"
    IL_0013:  stloc.1
    IL_0014:  ldc.i4.s   12
    IL_0016:  stloc.2
    IL_0017:  ldloc.1
    IL_0018:  ldloc.2
    IL_0019:  newobj     instance void class '<>f__AnonymousType0`2'<string,int32>::.ctor(!0,
                                                                                            !1)
    IL_001e:  stloc.3
    IL_001f:  ldloc.3
    IL_0020:  stloc.0
    IL_0021:  ldloc.0
    IL_0022:  callvirt   instance !0 class '<>f__AnonymousType0`2'<string,int32>::get_Name()
    IL_0027:  call       void [mscorlib]System.Console::WriteLine(string)
    IL_002c:  nop
    IL_002d:  call       valuetype [mscorlib]System.ConsoleKeyInfo [mscorlib]System.Console::ReadKey()
    IL_0032:  pop
    IL_0033:  ret
    } // end of method Program::Main

相同结构，不同写法的匿名类型经过编译以后只创建了一个匿名类型:

    class '<>f__AnonymousType0`2'<string,int32>

匿名类型的的实例可以视为`Object`，但没法将`Object`的变量转型回匿名类型，因为不知道匿名类型在编译时的名称。

属性有别于字段，它其实是一个方法。

Automatically Implemented Property(AIP)

属性的编译时inline的?


	class Person
	{
		public string Name { get; set; } = "World";
		public string Age { get; set; }

		public static string Type { get; set; } = "mammal";
	}

<img src="property IL.PNG">

## 有参属性

