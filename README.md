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
## Poor man's async keyword (aka ForkJoin Light^TM)

```java
    // Want to parallelize this without any bells and whistles ?
    slowFunction(..);
    slowFunction2(..);
    
    // Try this:
    private <T> List<T> async(Supplier<T>... o) {
        return Arrays.stream(o).parallel().map(f -> f.get()).collect(Collectors.toList());
    }

    private void async(Runnable... o) {
        Arrays.stream(o).parallel().map(r -> {
            r.run();
            return null;
        }).collect(Collectors.toList());
    }
    
    async(() -> slowFunction(...),
          () -> slowFunction2(...));
```
