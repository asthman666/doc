How to do DI?

1. Use an interface or base class to abstract the dependency implementation
2. Registration of the dependency in a service container. ASP.NET Core provides a build-in service container, IServiceProvider.
3. Injection of the service into the constructor of the class where it's used. The framework takes on the responsibility of creating an instance of the dependency and disposing of it when it's no longer needed.
   
Service lifetimes

Services can be registered with one of the following lifetimes:

    /// <summary>
    /// Specifies that a single instance of the service will be created.
    /// </summary>
    Singleton,
    /// <summary>
    /// Specifies that a new instance of the service will be created for each scope.
    /// </summary>
    /// <remarks>
    /// In ASP.NET Core applications a scope is created around each server request.
    /// </remarks>
    Scoped,
    /// <summary>
    /// Specifies that a new instance of the service will be created every time it is requested.
    /// </summary>
    Transient

Read Source Code

* **IServiceCollection**

        // 接口的继承, IServiceCollection 就是一个 IList<ServiceDescriptor> 泛型接口
        public interface IServiceCollection : IList<ServiceDescriptor> 
        {

        }

* **ServiceCollection**

        public class ServiceCollection : IServiceCollection 
        {
            // 定义了一个私有只读的 List<ServiceDescriptor> 泛型成员
            // 利用这个成员做了大部分的接口实现
            private readonly List<ServiceDescriptor> _descriptors = new List<ServiceDescriptor>();
            public int Count => _descriptors.Count;

            public bool IsReadOnly => false;

            public ServiceDescriptor this[int index]
            {
                get
                {
                    return _descriptors[index];
                }
                set
                {
                    _descriptors[index] = value;
                }
            }

            public void Clear()
            {
                _descriptors.Clear();
            }

            public bool Contains(ServiceDescriptor item)
            {
                return _descriptors.Contains(item);
            }

            public void CopyTo(ServiceDescriptor[] array, int arrayIndex)
            {
                _descriptors.CopyTo(array, arrayIndex);
            }

            public bool Remove(ServiceDescriptor item)
            {
                return _descriptors.Remove(item);
            }

            public IEnumerator<ServiceDescriptor> GetEnumerator()
            {
                return _descriptors.GetEnumerator();
            }

            void ICollection<ServiceDescriptor>.Add(ServiceDescriptor item)
            {
                _descriptors.Add(item);
            }

            IEnumerator IEnumerable.GetEnumerator()
            {
                return GetEnumerator();
            }

            public int IndexOf(ServiceDescriptor item)
            {
                return _descriptors.IndexOf(item);
            }

            public void Insert(int index, ServiceDescriptor item)
            {
                _descriptors.Insert(index, item);
            }

            public void RemoveAt(int index)
            {
                _descriptors.RemoveAt(index);
            }
        }

* **ServiceCollectionContainerBuilderExtensions**

        // 静态类
        public static class ServiceCollectionContainerBuilderExtensions
        {
            public static ServiceProvider BuildServiceProvider(this IServiceCollection services)
            {
                return BuildServiceProvider(services, ServiceProviderOptions.Default);
            }
        }

* **ServiceProvider**

        public object GetService(Type serviceType) => GetService(serviceType, Root);

        internal ConcurrentDictionary<Type, Func<ServiceProviderEngineScope, object>> RealizedServices { get; }

        internal object GetService(Type serviceType, ServiceProviderEngineScope serviceProviderEngineScope)
        {
            if (_disposed)
            {
                ThrowHelper.ThrowObjectDisposedException();
            }

            Func<ServiceProviderEngineScope, object> realizedService = RealizedServices.GetOrAdd(serviceType, _createServiceAccessor);
            _callback?.OnResolve(serviceType, serviceProviderEngineScope);
            DependencyInjectionEventSource.Log.ServiceResolved(serviceType);
            return realizedService.Invoke(serviceProviderEngineScope);
        }

* **AddSingleton<TService, TImplementation>()**
  
        public static IServiceCollection AddSingleton<TService, [DynamicallyAccessedMembers(DynamicallyAccessedMemberTypes.PublicConstructors)] TImplementation>(this IServiceCollection services)
            where TService : class
            where TImplementation : class, TService
        {
            if (services == null)
            {
                throw new ArgumentNullException(nameof(services));
            }

            return services.AddSingleton(typeof(TService), typeof(TImplementation));
        }

        public static IServiceCollection AddSingleton(
            this IServiceCollection services,
            Type serviceType,
            [DynamicallyAccessedMembers(DynamicallyAccessedMemberTypes.PublicConstructors)] Type implementationType)
        {
            if (services == null)
            {
                throw new ArgumentNullException(nameof(services));
            }

            if (serviceType == null)
            {
                throw new ArgumentNullException(nameof(serviceType));
            }

            if (implementationType == null)
            {
                throw new ArgumentNullException(nameof(implementationType));
            }

            return Add(services, serviceType, implementationType, ServiceLifetime.Singleton);
        }        

        private static IServiceCollection Add(
            IServiceCollection collection,
            Type serviceType,
            [DynamicallyAccessedMembers(DynamicallyAccessedMemberTypes.PublicConstructors)] Type implementationType,
            ServiceLifetime lifetime)
        {
            var descriptor = new ServiceDescriptor(serviceType, implementationType, lifetime);
            collection.Add(descriptor);
            return collection;
        }

My Code:

    using Microsoft.Extensions.DependencyInjection;
    using System;
    using System.Linq;

    namespace ConsoleApp13
    {
        interface ICar
        {
            public void Run();
        }

        class FSDCar : ICar
        {
            public void Run()
            {
                Console.WriteLine("FSD Car");
            }
        }

        class L2Car : ICar
        {
            public void Run()
            {
                Console.WriteLine("L2 Car");
            }
        }

        class Program
        {
            static void Main(string[] args)
            {
                var services = new ServiceCollection();

                services
                    .AddSingleton<ICar, FSDCar>()
                    .AddScoped<ICar, L2Car>()
                    ;
                var serviceProvider = services.BuildServiceProvider();
                var car = serviceProvider.GetServices<ICar>().First(o => o.GetType() == typeof(FSDCar));
                Console.WriteLine("singleton car: " + car.GetHashCode());

                var car2 = serviceProvider.GetServices<ICar>().First(o => o.GetType() == typeof(FSDCar));
                Console.WriteLine("singleton car: " + car2.GetHashCode());


                var car3_0 = serviceProvider.GetServices<ICar>().First(o => o.GetType() == typeof(L2Car));
                Console.WriteLine("scrope car: " + car3_0.GetHashCode());
                using (var scrope = serviceProvider.CreateScope() )
                {
                    var car3_1 = scrope.ServiceProvider.GetServices<ICar>().First(o => o.GetType() == typeof(L2Car));
                    Console.WriteLine("scrope car: " + car3_1.GetHashCode());
                }
                var car3_2 = serviceProvider.GetServices<ICar>().First(o => o.GetType() == typeof(L2Car));
                Console.WriteLine("scrope car: " + car3_2.GetHashCode());
            }
        }
    }


[Framework-provided services](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-5.0#framework-provided-services)

[Services injected into Startup](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-5.0)