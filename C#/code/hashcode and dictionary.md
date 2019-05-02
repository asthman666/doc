# HashCode and Dictionary

   public class PersonKey
    {
        public int Number;
        public PersonKey(int number)
        {
            Number = number;
        }

        public override bool Equals(object obj)
        {
            return Number == ((PersonKey)obj).Number;
        }

        public override int GetHashCode()
        {
            return Number;
        }
    }

    public class Person {
        public string Name;
        public int Age;
        public Person(string name, int age)
        {
            Name = name;
            Age = age;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Dictionary<PersonKey, Person> d = new Dictionary<PersonKey, Person>();
            PersonKey pk = new PersonKey(19);
            d[pk] = new Person("alex", 30);
            pk.Number = 1;
            Console.WriteLine($"name: {d[pk].Name}, hashcode: {pk.GetHashCode()}");
            Console.ReadKey();
        }
    }