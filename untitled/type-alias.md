# Type Alias



1. You can use `T : X` notation to define `T` as another spelling for type `X`.
2. In this case, `T` and `X` will be exactly the same thing.
3. You can use a type alias to prevent name conflict when importing modules.
4. `X` on the right must be a type name. It cannot be definition of a type.

**Examples**

```perl
MyInt : int
process = fn(x:MyInt -> int) { x }
```

