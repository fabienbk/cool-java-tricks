# Cool Java Tricks

Useful snippets, obscure features, etc.

## Enums interfaces and Multiple Bounded Type Parameters

```java
    public interface MarkerInterface { ... }
    
    public enum CoolEnum implements MarkerInterface { FOO, BAR }
    
    public <T extends Enum & MarkerInterface> void func(T param) { 
        System.out.prinln(param.name());
    }
    
    func(CoolEnum.FOO) // compiles
    func(AnotherEnum.FOO) // does not compile
```
