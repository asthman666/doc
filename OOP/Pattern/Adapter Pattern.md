## Adapter pattern (also known as wrapper)

The **key idea** in this pattern is to work through a separate adapter that adapts the interface of an (already existing) class without changing it.

### The adapter design pattern describes how to solve such problems:

* Define a separate adapter class that converts the (incompatible) interface of a class (adaptee) into another interface (target) clients require.

* Work through an adapter to work with (reuse) classes that do not have the required interface.

Example (C#):

    // client required interface
    public interface IRemoteControl
    {
        void Open();
        void Close();
    }

    // existing class interface
    public interface IRobot
    {
        void Run();
        void Stop();
    }

    // existing class
    public class CarRobot : IRobot
    {
        public void Run()
        {
            Console.WriteLine("CarRobot Run");
        }

        public void Stop()
        {
            Console.WriteLine("CarRobot Stop");
        }
    }

    // adaptor class implement client required interface
    public class RobotRemoteControl : IRemoteControl
    {
        private IRobot _robot;
        public RobotRemoteControl(IRobot robot)
        {
            _robot = robot;
        }
        public void Open()
        {
            _robot.Run();
        }

        public void Close()
        {
            _robot.Stop();
        }
    }


    class Program
    {
        static void Main(string[] args)
        {
            var robot = new CarRobot();
            var adaptor = new RobotRemoteControl(robot);
            adaptor.Open();
            adaptor.Close();
        }
    }