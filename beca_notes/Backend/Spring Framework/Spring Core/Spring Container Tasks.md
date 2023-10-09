## Creating Objects
> Container is responsible for creating obj based on the configuration metadata provided to it.

* The container creates ***singleton*** or ***prototype beans*** based on the scope of the bean.

> [!note] Singleton Beans
> * Created only once and shared across the application.
> * Created when the application context is loaded, and return the same instance of the bean whenever it is requested.
> -> **suitable for objects that are  stateless and can be shared across the application** (Ex: utility classes)

> [!note] Prototype Beans
> * Created each time they are requested from the container.
> * Container creates new instance of the beans every time it is requested.
> -> **suitable for objects that stateful and need to maintain a separate state for each instance** (Ex: web session)

> [!example] 

## Managing Dependencies

## Configuring Objects

## Providing Objects

## Managing the lifecycle