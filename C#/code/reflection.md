# Reflection

    using System;
    using System.IO;
    using System.Reflection;

    namespace ConsoleApp5
    {
        public class Person
        {
            public Person()
            {

            }
            public Person(string name, int age)
            {
                this.Name = name;
                this.Age = age;
            }
            public string Name { get; set; }
            public int Age { get; set; }

            public void SayHello()
            {
                Console.WriteLine("Hello, I'm " + this.Name);
            }
        }

        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine(string.Format("ExecutingAssembly {0}", Assembly.GetExecutingAssembly())); // ExecutingAssembly ConsoleApp5, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null

                // get current assembly types
                Assembly currentAssembly = Assembly.GetExecutingAssembly();
                foreach (Type type in currentAssembly.GetTypes())
                {
                    Console.WriteLine(string.Format("Assembly Type FullName: {0}", type.FullName));
                    // Assembly Type FullName: ConsoleApp5.Person
                    // Assembly Type FullName: ConsoleApp5.Program
                }

                Console.WriteLine($"Assembly FullName: {typeof(String).Assembly.FullName}"); // Assembly FullName: System.Private.CoreLib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e
                Console.WriteLine($"Type of String Namespace: {typeof(String).Namespace}"); // Type of String Namespace: System

                string name = "noah";
                Console.WriteLine($"Type of String Location: {name.GetType().Assembly.Location}"); // Type of String Location: C:\Program Files\dotnet\shared\Microsoft.NETCore.App\3.1.8\System.Private.CoreLib.dll

                var p = new Person("noah", 15);
                foreach (var pp in p.GetType().GetProperties())
                {
                    Console.WriteLine(String.Format("Person class Property: {0}, Value: {1}", pp.Name, pp.GetValue(p)));
                    // Person class Property: Name, Value: noah
                    // Person class Property: Age, Value: 15
                }

                foreach (var ff in p.GetType().GetFields())
                {

                }

                var p2 = (Person)Activator.CreateInstance(p.GetType()); // Person class must has the no params construct
                p2.Name = "beata";
                p2.Age = 16;
                p.GetType().InvokeMember("SayHello", System.Reflection.BindingFlags.InvokeMethod, null, p2, null); // Hello, I'm beata

                Console.ReadKey();
            }
        }
    }


> [find the publickeytoken for a dll](https://stackoverflow.com/questions/1710935/how-do-i-find-the-publickeytoken-for-a-particular-dll)

> [loading dlls at runtime](https://stackoverflow.com/questions/18362368/loading-dlls-at-runtime-in-c-sharp)

> [create an instance of a class from a string](https://stackoverflow.com/questions/223952/create-an-instance-of-a-class-from-a-string)

> [list all classes in assembly](https://stackoverflow.com/questions/1315665/c-list-all-classes-in-assembly)

> [type get typename return null](https://stackoverflow.com/questions/1825147/type-gettypenamespace-a-b-classname-returns-null)

> [get current method namespace](https://stackoverflow.com/questions/18485469/how-can-i-retrieve-the-namespace-to-a-string-c-sharp)

> [how to pass parameters to activator create instance](https://stackoverflow.com/questions/2451336/how-to-pass-parameters-to-activator-createinstancet)