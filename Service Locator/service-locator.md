# Service Locator

A service class defines an abstract interface to a set of operations. A concrete service provider implements this interface. A separate service locator provides access to the service by finding an appropriate provider while hiding both the provider’s concrete type and the process used to locate it.

## Why Service Locator


**Pros:**
- Decoupling

**Keep in mind:**
- The service might not be located
- The service doesn’t know who is locating it

```c#
public interface IGameService
{
}
```

```c#
namespace ServiceLocatorSample.ServiceLocator
{
    /// <summary>
    /// Simple service locator for <see cref="IGameService"/> instances.
    /// </summary>
    public class ServiceLocator
    {
        private ServiceLocator() { }

        /// <summary>
        /// currently registered services.
        /// </summary>
        private readonly Dictionary<string, IGameService> services = new Dictionary<string, IGameService>();

        /// <summary>
        /// Gets the currently active service locator instance.
        /// </summary>
        public static ServiceLocator Current { get; private set; }

        /// <summary>
        /// Initalizes the service locator with a new instance.
        /// </summary>
        public static void Initiailze()
        {
            Current = new ServiceLocator();
        }

        /// <summary>
        /// Gets the service instance of the given type.
        /// </summary>
        /// <typeparam name="T">The type of the service to lookup.</typeparam>
        /// <returns>The service instance.</returns>
        public T Get<T>() where T : IGameService
        {
            string key = typeof(T).Name;
            if (!services.ContainsKey(key))
            {
                Debug.LogError($"{key} not registered with {GetType().Name}");
                throw new InvalidOperationException();
            }

            return (T)services[key];
        }

        /// <summary>
        /// Registers the service with the current service locator.
        /// </summary>
        /// <typeparam name="T">Service type.</typeparam>
        /// <param name="service">Service instance.</param>
        public void Register<T>(T service) where T : IGameService
        {
            string key = typeof(T).Name;
            if (services.ContainsKey(key))
            {
                Debug.LogError($"Attempted to register service of type {key} which is already registered with the {GetType().Name}.");
                return;
            }

            services.Add(key, service);
        }

        /// <summary>
        /// Unregisters the service from the current service locator.
        /// </summary>
        /// <typeparam name="T">Service type.</typeparam>
        public void Unregister<T>() where T : IGameService
        {
            string key = typeof(T).Name;
            if (!services.ContainsKey(key))
            {
                Debug.LogError($"Attempted to unregister service of type {key} which is not registered with the {GetType().Name}.");
                return;
            }

            services.Remove(key);
        }
    }
}
```


```c#
public static class Bootstrapper
    {
        [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.AfterSceneLoad)]
        public static void Initiailze()
        {
            // Initialize default service locator.
            ServiceLocator.Initiailze();

            // Register all your services next.
            ServiceLocator.Current.Register<IMyGameServiceA>(new MyGameServiceA());
            ServiceLocator.Current.Register<IMyGameServiceB>(new MyGameServiceB());
            ServiceLocator.Current.Register<IMyGameServiceC>(new MyGameServiceC());

            // Application is ready to start, load your main scene.
            SceneManager.LoadSceneAsync(1, LoadSceneMode.Additive);
        }
    }
```
