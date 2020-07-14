    // case 1:
    var line = Console.ReadLine();
    var inputs = System.Text.RegularExpressions.Regex.Split(line, @"\s+");
    foreach ( var input in inputs ) {
        Console.WriteLine(input);
    }

    // case 2:
    var k = Console.ReadKey(true);
    switch (k.Key)
    {
        case ConsoleKey.Enter:
            Console.WriteLine("enter Enter");
            break;
        default:
            Console.WriteLine("default");
            break;
    }

    // case 3:
    while(true)
    {
        var line = Console.ReadLine();
        if (string.IsNullOrEmpty(line)) {
            Console.Write("program exist since no input");
            break;
        }
        else
        {
            Console.WriteLine(line);
        }
    }    

[division](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators#division-operator-)