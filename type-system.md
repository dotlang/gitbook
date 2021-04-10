# Type System

Types are blueprints which are used to create values for bindings. They determine a set of possible values that can be assigned to bindings of that types.

Types can be basic \(integer number, character, ...\) or compound \(sequence, map, struct, union\).

## Type name resolution

Order of search to resolve a type name to its declaration:

1. Current function
2. Closure
3. Module level
4. At any level, if there are multiple candidates there will be a compiler error.
5. Two named types are never equal. 
6. Two types T1 and T2 are identical/assignable/exchangeable if they have the same structure \(e.g. `int|string` vs `int|string`\).

## Named Types

1. You can name a type so you will be able to refer to that type later in the code.
2. Type names must start with a capital letter to be distinguished from bindings.
3. You define a named type similar to a binding: `NewType = UnderlyingType`.
4. The new type has same binary representation as the underlying type but it will be treated as a completely different type.

**Examples**

```perl
MyInt = int
IntArray = [int]
StatePopulation = [string:int]
Point = struct {x: int, y: int}
```

## Type Alias

1. You can use `T : X` notation to define `T` as another spelling for type `X`.
2. In this case, `T` and `X` will be exactly the same thing.
3. You can use a type alias to prevent name conflict when importing modules.
4. `X` on the right must be a type name. It cannot be definition of a type.

**Examples**

```perl
MyInt : int
process = fn(x:MyInt -> int) { x }
```



## Type Casting

1. We use `T(value)` notation to cast value to a specific type.
2. Casting can be done for primitive types, named types or unions.
3. Literals \(e.g. `1` or `"Hello world"`\) will get value of the most primitive type inferred by the compiler \(`int`, `string`, ...\). 
4. Based on previous point, you cannot assign an untyped literal to a named type without casting. Because for example `1` literal is an `int` literal not a named type that maps to `int`.

**Examples**

```perl
MyInt = int
myint_var = MyInt(12)
```

