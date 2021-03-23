# Error Handling



1. We have a struct type defined in core called `error` with a binding of the same name representing a null-op error.
2. `error = struct (key: type|nothing, message: string|nothing, location: string|nothing, cause: error|nothing)`
3. At operator is used to check for error and do an early return from current function.
4. At operator is used like `expression@` \(return the error itself if expression evaluates to an error\) or `expression@{expression}` \(return right-hand side expression in case of error in the left-hand side expression\)
5. If early return is of type `error` runtime will automatically populate its `cause` with original error.
6. Note that the expression inside `{}` will not be evaluated until the expression before `@` evaluates to an error.

Examples:

```perl
result = process(1,2)@ + process(3,4)@

result = process(1,2)@{nothing} + process(3,4)@{nothing}

data = validateInput(a,b)@{getDefaultReturnValue()}
```

