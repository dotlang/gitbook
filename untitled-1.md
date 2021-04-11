# Bindings

## Binding Declaration

1. A binding assigns an identifier to a typed immutable memory location. 
2. A binding's value can be a literal value, a complex expression or another binding.
3. The literal value can be of any valid type \(integer number, function literal, struct literal, ...\). 
4. Binding names must start with a lowercase letter \(except bindings that define a generic type, more in corresponding section\).
5. You can define bindings at module-level or inside a function. 
6. Module-level bindings can only have literals as their value. 
7. Type of a binding can usually be inferred without ambiguity from right side value, but you also have the option to specify the type \(Example A\).
8. If the right side of an assignment is a struct, you can destruct it into its elements by using comma separated values on the left side of `=` \(Example B\). 
9. In destruction, you can also use underscore to indicate you are not interested in one or more of those elements \(Example C\).
10. Binding name resolution is similar to type/function name resolution.

**Syntax**:

1. `identifier = expression`
2. `identifier : type = expression`

**Examples**

```perl
#A
x : int = 12

#type is inferred
g = 19.8 

#B
a,b = Tuple{1, 100}

#C
a,_ = point

a,_ = single_element_struct
```

## Resources

There are different types of resources which needs special handling but we can categorise them into two main groups: Memory and others \(sockets, network connections, DB connections, files, threads, ...\).

The first type is handled via GC and the second type is automatically freed by runtime when the corresponding binding goes out of scope. These are similar to C++ destructors, but implemented only for scarce system resources and handle deallocation of those resources when they are no longer needed.

Any other mechanism to free/cleanup a resource, exposes mutation to the language which causes a lot of confusion.

## Error Handling

1. We have a built-in struct type defined in core called `error` with a binding of the same name representing an empty error.
2. `error = struct (key: type|nothing, message: string|nothing, location: string|nothing, cause: error|nothing)`
3. At operator \(`@`\) is used to check for error and do an early return from current function.
4. At operator is used like `expression@` \(return the error itself if expression evaluates to an error\) or `expression@{expression}` \(return right-hand side expression in case of error in the left-hand side expression\)
5. If early return is of type `error` runtime will automatically populate its `cause` with original error if possible.
6. Note that the expression inside `{}` will not be evaluated unless the expression before `@` evaluates to an error.

Examples:

```perl
process = fn(x:int, y:int -> int|error) ...

result = process(1,2)@ + process(3,4)@

result = process(1,2)@{nothing} + process(3,4)@{nothing}

data = validateInput(a,b)@{getDefaultReturnValue()}
```



