# try

你可以抛出一个捕获的异常，给这个异常添加一些信息然后再重新抛出，当你debugging的时候，可以看到这个信息

code like this:

    using System;
    using System.IO;

    public class ProcessFile
    {
        public static void Main()
        {
            FileStream fs = null;
            try   
            {
                //Opens a text tile.
                fs = new FileStream(@"C:\temp\data.txt", FileMode.Open);
                StreamReader sr = new StreamReader(fs);
                string line;
                
                //A value is read from the file and output to the console.
                line = sr.ReadLine();
                Console.WriteLine(line);
            }
            catch(FileNotFoundException e)
            {
                Console.WriteLine("[Data File Missing] {0}", e);
                throw new FileNotFoundException(@"[data.txt not in c:\temp directory]",e);
            }
            finally
            {
                if (fs != null) 
                    fs.Close();
            }
        }
    }


[how-to-explicitly-throw-exceptions](https://docs.microsoft.com/en-us/dotnet/standard/exceptions/how-to-explicitly-throw-exceptions)

[how-to-create-user-defined-exceptions](https://docs.microsoft.com/en-us/dotnet/standard/exceptions/how-to-create-user-defined-exceptions)

