**subject** -> an object, maintains a list of its dependents

**observers** -> the dependents

**subject** notifies **observers** automatically of any state changes, usually by calling one of their methods

    using System;
    using System.Collections.Generic;

    namespace ConsoleApp1
    {
        public class WeatherReport
        {
            public string WeatherStatus { get; set; }
            public int MaxTemperature { get; set; }
            public int MinTemperature { get; set; }
        }

        public class WebPage : IObserver<WeatherReport>
        {
            public string WeatherMessage;

            public void OnCompleted()
            {

            }

            public void OnError(Exception error)
            {

            }

            public void OnNext(WeatherReport value)
            {
                WeatherMessage = $"{value.WeatherStatus}, Temperature: {value.MinTemperature} - {value.MaxTemperature}";
            }
        }

        public class Phone : IObserver<WeatherReport>
        {
            public string WeatherMessage;

            public void OnCompleted()
            {
                
            }

            public void OnError(Exception error)
            {

            }

            public void OnNext(WeatherReport value)
            {
                WeatherMessage = $"{value.WeatherStatus}/{value.MinTemperature} - {value.MaxTemperature}";
            }
        }

        public class Subject : IObservable<WeatherReport>
        {
            public IList<IObserver<WeatherReport>> observers = new List<IObserver<WeatherReport>>();
            public IDisposable Subscribe(IObserver<WeatherReport> observer)
            {
                observers.Add(observer);
                return new Unsubscriber(observers, observer);
            }

            public void Notify(WeatherReport value)
            {
                foreach ( var observer in observers )
                {
                    observer.OnNext(value);
                }
            }
        }

        public class Unsubscriber : IDisposable
        {
            private IObserver<WeatherReport> observer;
            private IList<IObserver<WeatherReport>> observers;

            public Unsubscriber(IList<IObserver<WeatherReport>> observers, IObserver<WeatherReport> observer)
            {
                this.observers = observers;
                this.observer = observer;
            }
            
            public void Dispose()
            {
                if (observer != null && observers.Contains(observer))
                {
                    observers.Remove(observer);
                }
            }
        }

        class Program
        {
            static void Main(string[] args)
            {
                var subject = new Subject();
                var webpage = new WebPage();
                var phone = new Phone();
                subject.Subscribe(phone);
                subject.Subscribe(webpage);

                var weatherReport = new WeatherReport { WeatherStatus = "Snow", MinTemperature = -5, MaxTemperature = 7 };

                subject.Notify(weatherReport);

                Console.WriteLine($"update webpage weather to '{webpage.WeatherMessage}'");
                Console.WriteLine($"update phone weather to '{phone.WeatherMessage}'");
                Console.ReadKey();
            }
        }
    }

> [Observer_pattern](https://en.wikipedia.org/wiki/Observer_pattern)