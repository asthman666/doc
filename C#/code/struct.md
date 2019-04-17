# Struct

    public struct Person
    {
        public string Name { get; set; }
        public int Age { get; set; }
        public Person(string n, int a)
        {
            Name = n;
            Age = a;
        }
    }
    class Program
    {

        static void Main(string[] args)
        {
            Person p = new Person("ai", 10);

            Dictionary<string, Person> d = new Dictionary<string, Person>()
            {
                {"a", p },
            };

            // Change the Dictionary Struct Value
            Person dp = d["a"];
            dp.Name = "noob";

            // Change the Original Struct Value
            p.Name = "jobs";

            Console.WriteLine(dp.Name); // "noob"

            Console.WriteLine(p.Name); // "jobs"

            Console.WriteLine(d["a"].Name); // "ai"

            Console.ReadKey();
        }
    }