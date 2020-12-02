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

[Framework-provided services](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-5.0#framework-provided-services)

[Services injected into Startup](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-5.0)