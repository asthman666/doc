# Reflection

    using System;

    namespace Study
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
                Console.WriteLine(Assembly.GetExecutingAssembly());

                // get current assembly types
                Assembly currentAssembly = Assembly.GetExecutingAssembly();
                foreach (Type type in currentAssembly.GetTypes())
                {
                    Console.WriteLine(type.FullName);
                }

                Console.WriteLine(typeof(String).Assembly.FullName);
                Console.WriteLine(typeof(String).Namespace);

                string name = "noah";
                Console.WriteLine(name.GetType().Assembly.Location);

                var p = new Person("noah", 15);
                foreach (  var pp in p.GetType().GetProperties() )
                {
                    Console.WriteLine(String.Format("property: {0}, value: {1}", pp.Name, pp.GetValue(p)));                
                }
                
                foreach ( var ff in p.GetType().GetFields() ) {
                
                }

                var p2 = (Person)Activator.CreateInstance(p.GetType()); // Person class must has the no params construct
                p2.Name = "beata";
                p2.Age = 16;
                p.GetType().InvokeMember("SayHello", System.Reflection.BindingFlags.InvokeMethod, null, p2, null);

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