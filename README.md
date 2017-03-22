# Cool Java Tricks

Useful snippets, obscure features, etc.

## Enums interfaces and Multiple Bounded Type Parameters

    public interface MarkerInterface { ... }
    
    public enum CoolEnum implements MarkerInterface { FOO, BAR }
    
    public <T extends Enum & MarkerInterface> void func(T param) { .. }
    
    func(CoolEnum.FOO) // compiles
    func(AnotherEnum.FOO) // does not compile
