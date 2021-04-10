# Generics



1. There is a special data type called `type`. Bindings of this value \(which should be named like a type\), can have any possible "type" as their value.
2. Every binding of type `type` must have a compile time literal value.
3. Generic types are defined using module-level functions that accept `type` arguments and return a `type`. 
4. These functions must be compile time \(because anything related to `type` must be\) \(Example A\). 
5. This means that you cannot use any non-literal value as a value for a type binding.
6. You also cannot assign a function that receives or return a type to a function-level lambda.
7. Note that a generic function's input of form `T|U` means caller can provide a union binding which has at least two options for the type, it may have 2 or more allowed types.
8. If a generic type is omitted in a function call \(and it is at the end of argument list\), compiler will infer it \(Example B\). 
9. Generic functions are implemented as functions that accept `type` arguments but their output is not `type` \(Example B\).
10. You can also define generic function types in the same way you define generic data structures. This can be useful when you want to separate generic parameter from non-generic ones.

**Examples**

```perl
#A
LinkedList = fn(T: type -> type)
{
    Node = struct (
        data: T,
        next: Node|nothing
    )
    Node|nothing
}

process = fn(x: LinkedList(int) -> int)
process = fn(T: type, ll: LinkedList(T) -> ...

process = (T: type, data: List(T) -> float) ...
#type of pointer is fn(int, List(int)->float)
pointer = process(int, _) 

process = fn(T: type, x: [T], index: int -> T) { x[index] }

#B
push = fn(data: T, stack: Stack(T), T: type -> Stack(T)) {...}
result = push(int_var, int_stack)

#Below two are the same
MyFunc1 = fn(T: type -> type) { fn(data: T->int) }
MyFunc2 = fn(data: T, T: type -> int)

#Below two are the same
MyType = MyFunc1(int)
MyType = MyFunc2(_, int)
```

## Optional Arguments

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



