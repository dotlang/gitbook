# Main Features



1. **Import a module**: `queue = import("/core/std/queue")` \(you can also import from external sources like GitHub\).
2. **Primitive types**: `int`, `float`, `char`, `byte`, `bool`, `string`, `type`, `nothing`. 
3. **Bindings**: `my_var:int = 19` \(type is optional, everything is immutable\).
4. **Sequence**: `my_array = [1, 2, 3]` \(type of `my_array` is `[int]`, sequence of integers\).
5. **HashMap**: `my_map = ["A":1, "B":2, "C":3]` \(type of `my_map` is `[string:int]`, hash map of string to integer\)
6. **Named type**: `MyInt = int` \(Defines a new type `MyInt` with same binary representation as `int`\).
7. **Type alias**: `IntType : int` \(A different name for the same type\).
8. **Struct type**: `Point = struct(x: int, y:int, data: float)` \(Like C `struct`\).
9. **Struct literal**: `location = Point{x:10, y:20, data:1.19}`.
10. **Union type**: `MaybeInt = int | nothing` \(Can store either of two types, note that this is a named type\).
11. **Function**: `calculate = fn(x:int, y:int -> float) { x/y }` \(Functions are all lambdas, the last expression in the body is return value\).
12. **Concurrency**: `my_task := processData(x,y,z)` \(Start a new micro-thread and evaluate an expression in parallel\).
13. **Generics**: `ValueKeeper = fn(T: type -> type) { struct{data: T} }` \(A function that returns a type\)
14. **Generics**: `push = fn(x: T, stack: Stack(T), T: type -> Stack(T)) { ... }`
15. **Enum**: `DayOfWeek = enum [saturday, sunday, monday, tuesday, wednesday, thursday, friday]`
16. **Errors**: `result = validateData(a,b,c)@{makeError(InvalidArgument)}`

