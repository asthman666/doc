    using System;

    namespace ConsoleApp11
    {
        public interface ICar
        {
            int RechargeMileage { get; set; }
            void Recharge();
        }

        public class BEVCar : ICar
        {
            public int RechargeMileage { get; set; }
            public void Recharge()
            {
                Console.WriteLine($"use electricity, can run {RechargeMileage} km if full charge");
            }
        }

        public class HEVCar : ICar
        {
            public int RechargeMileage { get; set; }
            public void Recharge()
            {
                Console.WriteLine($"use gasoline, can run {RechargeMileage} km if full charge");
            }
        }

        public interface IFactory
        {
            ICar ProduceCar();
        }

        public class BEVCarFactory : IFactory
        {
            public ICar ProduceCar()
            {
                return new BEVCar();
            }
        }

        public class HEVCarFactory : IFactory
        {
            public ICar ProduceCar()
            {
                return new HEVCar();
            }
        }

        public interface ICarFactory
        {
            ICar ProduceCar(string carType);
        }

        public class CarFactory : ICarFactory
        {
            public ICar ProduceCar(string carType)
            {
                switch (carType)
                {
                    case "BEV":
                        return new BEVCar();
                    case "HEV":
                        return new HEVCar();
                    default:
                        throw new NotImplementedException($"This factory can not produce {carType} car");
                }
            }
        }

        class Program
        {
            static void Main(string[] args)
            {
                new BEVCar() { RechargeMileage = 500 }.Recharge();
                new HEVCar() { RechargeMileage = 700 }.Recharge();

                new BEVCarFactory().ProduceCar().Recharge();
                new HEVCarFactory().ProduceCar().Recharge();

                new CarFactory().ProduceCar("BEV").Recharge();
                new CarFactory().ProduceCar("HEV").Recharge();
            }
        }
    }
