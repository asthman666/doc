### All these implementations share four common characteristics, however:

* A single constructor, which is private and parameterless. This prevents other classes from instantiating it (which would be a violation of the pattern). Note that it also prevents subclassing - if a singleton can be subclassed once, it can be subclassed twice, and if each of those subclasses can create an instance, the pattern is violated. The **factory pattern** can be used if you need a single instance of a base type, but the exact type isn't known until runtime.
* The class is sealed. This is unnecessary, strictly speaking, due to the above point, but may help the JIT to optimise things more.
* A static variable which holds a reference to the single created instance, if any.
* A public static means of getting the reference to the single created instance, creating one if necessary.

        using System;

        namespace ConsoleApp10
        {
            public sealed class Test
            {
                private Test() { }
                public static Test SingletonInstance => Nested.testSingleton;
                private class Nested
                {
                    internal readonly static Test testSingleton = new Test();
                }
            }

            public sealed class TestLazy
            {
                private readonly static Lazy<TestLazy> singletonInstance = new Lazy<TestLazy>(() => new TestLazy());
                private TestLazy() { }
                public static TestLazy SingletonInstance => singletonInstance.Value;
            }

            class Program
            {
                static void Main(string[] args)
                {
                    Console.WriteLine(Test.SingletonInstance.GetHashCode());
                    Console.WriteLine(Test.SingletonInstance.GetHashCode());

                    Console.WriteLine(TestLazy.SingletonInstance.GetHashCode());
                    Console.WriteLine(TestLazy.SingletonInstance.GetHashCode());
                }
            }
        }

> [implementing-the-singleton-pattern-in-asp-net-core](https://espressocoder.com/2019/01/03/implementing-the-singleton-pattern-in-asp-net-core/)

> [Singleton](https://csharpindepth.com/Articles/Singleton#exceptions)

> [singleton-design-pattern](https://www.dofactory.com/net/singleton-design-pattern)