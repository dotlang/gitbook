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

