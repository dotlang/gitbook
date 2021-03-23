# Optional Arguments

When defining a function, you can use `:>` instead of `:` between argument name and type to indicate that, if that argument is missing when function is called, compiler or runtime should pass a default value for that argument. This default value is determined based on the type of the argument.

1. If type is union with an option for `nothing`, then nothing is the default value.
2. If type is a number \(int, float, char, byte\), zero is the default value.
3. There are other default values for generic types which are explained in Generics section.

Note that, if caller decides not to pass values for optional function arguments and they are located at the end of argument list, they can be ignored \(Example B below\)

```elixir
#A
process = fn(x:>int, y:int -> string) { ... }

#below are the same
result = process(,100)
result = process(0,100)

#B
process = fn(x:>int|nothing, y:int, z:> int -> string) { ... }

#below are the same
result = process(100, 20,)
result = process(100, 20)

#below are also the same
result = process(,10)
result = process(nothing, 10)
result = process(nothing, 10, 0)
```

