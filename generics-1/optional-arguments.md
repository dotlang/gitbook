# Optional Arguments

We discussed optional arguments in the function section. They are also very useful with generics. Using this feature we can provide automatic type inference and a special kind of polymorphism.

### Type inference

You can use `T :> type` notation to indicate compiler should infer type T when function is being called.

```elixir
process = fn(data: T, T:> type -> string) { ... }

#Here compiler will infer T using type of 'data' which is int
#so below two calls are the same
process(100) 
process(100, int)
```

This means:

1. If call is made for a non union type, then compile time of T will be inferred and used.
2. If call is being for a union type and there is no function to infer, compiler will infer the union type.
3. If call is for a union type and there are functions that need to be inferred, if we have an implementation for the union type it will be used. Otherwise, compiler will make sure we have impl for each case of the union, and delegate actual infer to runtime to use dynamic type inside the argument and use it for inference.

### Polymorphism and Contracts

You can also use `:>` notation when using a function of a generic type, which indicates compiler or runtime \(depending on the situation\) should find a correct function for you. This can be used to write different implementations of logic for each different type and let language decide which implementation to use at compile time or runtime.

A simple example:

```elixir
ToString = fn(T: type -> type) { fn(data: T -> string) }
intToString: ToString(int) = fn(x: int -> string) ...

myFunction = fn(item: T, stringer:> ToString(T), T:> type -> int) {
  ... result = stringer(data) ... 
}
```

In the above example, we define a generic type `ToString` which is a function. This type can have different implementations for each type. We have specialized it for integers in `intToString` function. Note that this function has explicitly set its type to `ToString(int)` to tell compiler that this is an implementation of ToString for integers.

Generic functions like `ToString` are called contracts because they define a behavior based on one or more types. Note that you are not limited to single typed contracts. Functions that are explicitly defined as that type are "implementations of that contract".

Below is another example of contracts:

```elixir
Hasher = fn(T: type -> type) { fn(data: T, T: type -> int) }
intHasher: Hasher(int) = fn...
stringHasher: Hasher(string) = fn...
...
process = fn(data: T, hasher:> Hasher(T), ... 
```

Another example of drawing different shapes:

```elixir
Draw = fn(S: type, C: type -> type) { 
    fn(shape: S, canvas: C, color: float -> string) 
}
drawCircleOnSolidCanvas: Draw(Circle, SolidCanvas) = 
    fn(shape: Circle, canvas: SolidCanvas, color: float -> string) { ... }
drawSquareOnAnyCanvas: Draw(Circle, Canvas) = 
    fn(shape: Circle, canvas: Canvas, color: float -> string) { ... }
process = fn(item: T, canvas: S, S: type, T: type, 
        drawFunction:> Draw(S,T) -> int) { 
        ... result = drawFunction(item, canvas) ... 
}
```

Above examples have all been compile time examples where compiler has all the information needed to determine what needs to be used for the contract function argument. But in case of using union bindings, this can be a runtime issue. If there is no implementation for the actual union type, then the compiler will just make sure we have implementations that can be used for all possible union options, and then delegate the actual value to be determined at runtime, based on the runtime type inside the union binding.

Note that contracts \(used with dynamic union\) can be used to implement solutions for expression problem. New types means new data types in the code and implementation of contracts for them. New operations, mean new contracts.



