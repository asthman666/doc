## Bridge pattern 

### What problems can the Bridge design pattern solve?

* An abstraction and its implementation should be defined and extended independently from each other.

* A compile-time binding between an abstraction and its implementation should be avoided so that an implementation can be selected at run-time.

Example (C#):

    public interface ICarShift
    {
        public void Shift();
    }

    public class ManualCar : ICarShift
    {
        public void Shift()
        {
            Console.WriteLine("Manual Car Shift");
        }
    }

    public class AutoCar : ICarShift
    {
        public void Shift()
        {
            Console.WriteLine("Auto Car Shift");
        }
    }

    public interface IPerson
    {
        public void Drive();
    }

    public class Person : IPerson
    {
        public ICarShift _carShift;

        public Person(ICarShift carShift)
        {
            _carShift = carShift;
        }

        public void Drive()
        {
            _carShift.Shift();
            Console.WriteLine("Car Run");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var manualCar = new ManualCar();
            var autoCar = new AutoCar();

            var p1 = new Person(manualCar);
            var p2 = new Person(autoCar);

            p1.Drive();
            p2.Drive();
        }
    }