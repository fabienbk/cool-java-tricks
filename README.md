# Cool Java Tricks

Useful snippets, obscure features, etc.

## Enums, interfaces, and Multiple Bounded Type Parameters

```java
    public interface MarkerInterface { ... }
    
    public enum CoolEnum implements MarkerInterface { FOO, BAR }
    
    public <T extends Enum & MarkerInterface> void func(T param) { 
        System.out.prinln(param.name());
    }
    
    func(CoolEnum.FOO) // compiles
    func(AnotherEnum.FOO) // does not compile
```
## Poor man's async functions

```java
    // Want to parallelize this without any bells and whistles ?
    slowFunction(..);
    slowFunction2(..);
    
    // Try this:
    Stream.<Runnable>of(
            () -> slowFunction(...),
            () -> slowFunction2(...)
    )
    .parallel()
    .forEach(Runnable::run);
    
    // Or this is you need to block until completion
    Stream.<Function>of(
            () -> slowFunction(...),
            () -> slowFunction2(...)
    )
    .parallel()
    .collect(Collectors.toList());
```
