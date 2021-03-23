# Type Casting



1. We use `T(value)` notation to cast value to a specific type.
2. Casting can be done for primitive types, named types or unions.
3. For union, you can use casting to get underlying type. If you cast a union binding to a wrong type, there will be a runtime error.
4. You can cast a union to `T|nothing` to do a safe cast. You will get `nothing` it type T is not inside the union binding.
5. Literals \(e.g. `1` or `"Hello world"`\) will get value of the most primitive type inferred by the compiler \(`int`, `string`, ...\). 
6. Based on 4, you cannot assign an untyped literal to a named type without casting. Because for example `1` literal is an `int` literal not a named type that maps to `int`.

**Examples**

```perl
MyInt = int
myint_var = MyInt(12)
```

