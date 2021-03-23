# Named Type



1. You can name a type so you will be able to refer to that type later in the code.
2. Type names must start with a capital letter to be distinguished from bindings.
3. You define a named type similar to a binding: `NewType = UnderlyingType`.
4. The new type has same binary representation as the underlying type but it will be treated as a completely different type.
5. You have seen examples of named types in previous sections \(Union, enum, ...\).

**Examples**

```perl
MyInt = int
IntArray = [int]
Point = struct (x: int, y: int)
```

