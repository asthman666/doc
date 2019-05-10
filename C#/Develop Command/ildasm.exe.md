# [ildasm.exe](https://docs.microsoft.com/en-us/dotnet/framework/tools/ildasm-exe-il-disassembler)

`ildasm.exe` takes a portable executable (PE) file that contains intermediate language (IL) code and creates a text file suitable as input to Ilasm.exe.

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise>ildasm C:\Users\nsong\source\repos\ConsoleApp8\ConsoleApp8\bin\Debug\ConsoleApp8.exe

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise>ildasm C:\Users\pig\source\repos\ConsoleApp8\ConsoleApp8\bin\Debug\ConsoleApp8.exe /output:C:\Users\pig\Desktop\M.il

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise>ilasm C:\Users\pig\Desktop\M.il


`Ctrl+M` 查看元数据