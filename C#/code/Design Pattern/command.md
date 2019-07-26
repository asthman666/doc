# Command

	public interface ICommand
	{
		void Open();
		void Close();
	}

	public class LightCommand : ICommand
	{
		private Light _light;

		public LightCommand(Light light)
		{
			_light = light;
		}

		public void Close()
		{
			_light.Down();
		}

		public void Open()
		{
			_light.On();
		}
	}

	public class ACCommand : ICommand
	{
		private AC _ac;

		public ACCommand(AC ac)
		{
			_ac = ac;
		}

		public void Close()
		{
			_ac.Down();
		}

		public void Open()
		{
			_ac.On();
			_ac.SetTemperature();
			_ac.SetWindSpeed();
			_ac.SetWindDirection();
		}
	}

	public class Light
	{
		public void On()
		{
			Console.WriteLine("turn on light");
		}

		public void Down()
		{
			Console.WriteLine("turn off light");
		}
	}

	public class AC
	{
		public void On()
		{
			Console.WriteLine("turn on ac");
		}

		public void SetTemperature()
		{
			Console.WriteLine("set ac temperature");
		}

		public void SetWindSpeed()
		{
			Console.WriteLine("set ac wind speed");
		}

		public void SetWindDirection()
		{
			Console.WriteLine("set ac wind direction");
		}

		public void Down()
		{
			Console.WriteLine("turn down ac");
		}
	}

	public class Invoker
	{
		private ICommand _command;

		public void SetCommand(ICommand command)
		{
			_command = command;
		}

		public void Open()
		{
			_command.Open();
		}

		public void Close()
		{
			_command.Close();
		}
	}

	class Program
	{
		static void Main(string[] args)
		{
			var ac = new AC();
			var acCommand = new ACCommand(ac);
			var invoker = new Invoker();
			invoker.SetCommand(acCommand);
			invoker.Open();
			invoker.Close();
			Console.ReadKey();
		}
	}

> [design pattern](https://www.dofactory.com/net/command-design-pattern)    