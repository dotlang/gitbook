# Overview

## Main Features

1. **Import a module**: `queue = import("/core/std/queue")` \(you can also import from external sources like GitHub\).
2. **Primitive types**: `int`, `float`, `char`, `string`,`byte`, `bool`, `error`, `type`, `nothing`. 
3. **Bindings**: `my_var:int = 19` \(type is optional, everything is immutable\).
4. **Sequence**: `my_array = [1, 2, 3]` \(type of `my_array` is `[int]` which means a sequence of integers\).
5. **HashMap**: `my_map = ["A":1, "B":2, "C":3]` \(type of `my_map` is `[string:int]`, which is a map of string to integer\)
6. **Named type**: `MyInt = int` \(Defines a new type `MyInt` with same binary representation as `int`\).
7. **Type alias**: `IntType : int` \(A different name for the same type\).
8. **Struct type**: `Point = struct{x: int, y:int, data: float}` \(Like C `struct`\).
9. **Struct literal**: `location = Point{x:10, y:20, data:1.19}`.
10. **Union type**: `MaybeInt = int | nothing` \(Can store either of two types, note that this is a named type\).
11. **Function**: `calculate = fn(x:int, y:int -> float) { x/y }` \(Functions are all lambdas, the last expression in the body is return value\).
12. **Concurrency**: `my_data := processData(x,y,z)` \(Start a new micro-thread and evaluate an expression in parallel\).
13. **Generic Types**: `ValueKeeper = fn(T: type -> type) { struct{data: T} }` \(Generic types are represented using functions that returns a type\)
14. **Generic Functions**: `push = fn(x: T, stack: Stack(T), T: type -> Stack(T)) { ... }`
15. **Enum**: `Weekdays = enum [monday, tuesday, wednesday, thursday, friday]`
16. **Errors**: `result = validateData(a,b,c)@{makeError(InvalidArgument)}`\(If call to validateData returns an error, then evaluate the expression inside brackets and return the result immediately\).

##  Symbols

1. `#`   Comment
2. `.`   Access struct members \(`customer.name`\)
3. `()` Function declaration and call \(`process(customer)`\)
4. `{}` Code block, multiple selections from module namespace, error check, struct declaration and literals
5. `[]` Sequence and hashMap \(`data=map["CA"]`\)
6. `|` Union data type \(`x:int|float|string`\)
7. `->` Function declaration \(`process = fn(...->...)`\)
8. `//`  Nothing-check operator \(`result=a//b` evaluates to a if it is not `nothing`,else b\)
9. `:`   Type declaration \(binding, struct field and function inputs\), type alias, struct literal \(`x:int`\)
10. `=`   Binding declaration, named type \(`x=12`\)
11. `_`   Place-holder \(lambda creator and assignment\) \(`partial = process(customer,_,_)`
12. `::`  Function call composition \(`result = id :: findCustomer :: printCustomer`\)
13. `@`   Error check \(`data = process@`\)
14. `?`   If operator \(`x=data==10 ? "A"`  if data is 10, then x will be "A" otherwise `nothing`\)
15. `&`   Type inference for struct literals \(When type can be inferred from context: `&{x:0,y:20}`\)
16. `:=`  Parallel execution
17. `..`  Access inside module \(`data = module1..func1(1,2,3)`\)

## Reserved Keywords

**Primitive data types**: `int`, `float`, `char`, `byte`, `bool`, `string`, `nothing`, `type`,`error`

**Logical Operators**: `and`, `or`, `not`

**Data type identifiers**: `fn`, `struct`, `enum`

**Reserved identifiers**: `true`, `false`, `import`

## Coding Style

1. Use 4 spaces indentation.
2. You must put each statement on a separate line. Newline is the statement separator.
3. Naming: `SomeDataType`, `someFunction`, `some_data_binding`, `some_module_alias`.
4. If a function returns a type \(generic types\) it should be named like a type.
5. If a binding is a reference to a function, it should be named like a function.
6. You can use `0x` prefix for hexadecimal numbers and `0b` for binary.
7. You can use `_` as digit separator in number literals.

## Operators

Operators are mostly similar to C language:

* Conditional operators: `and, or, not, ==, !=, >=, <=`
* Arithmetic: `+, -, *, /, %, %%, >>, <<, **`
* Note that `==` will do a comparison based on contents of its operands.
* `A // B` will evaluate to A if it is not `nothing`, else it will be evaluated to B \(e.g. `y = x // y // z // 0`\).
* `A ? B` will evaluate boolean expression A first, if true will evaluate to B, otherwise will evaluate to `nothing`. This can be mixed with `//` to provide ifElse construct.
* Example: `home_dir = (is_root ? "/root") // (is_default_user ? "/default") // (is_unknown ? "unknown") // "/tmp"`
* Conditional operators return `true` or `false` which are equal to `1` and `0` respectively when used as index of a sequence.
* Comments can appear anywhere in the code and start with `#`. Anything after `#` till end of the line is comment.
* Meta comments start with `##` as first two characters of the line and can be defined for a binding, type or function. These will be scanned with tools to automatically generate documentation. If `##` is the only thing in the line, it starts a block comment until another `##` appears in the file.

  ```elixir
    ## 
    some docs about this function
    x:int - comments about this input
    -> string - comments about the output
    ##
    process = fn(x:int -> string) { ... }

    ##Meta comment in one line
    x = 12

    ## 
    some docs about this type
    x:int - comments about this field
    y: string - comments about the y
    ##
    DataTypeX = struct {x:int, y:string}
  ```

