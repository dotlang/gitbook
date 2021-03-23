# Lambda



## Lambdas

1. All functions are lambdas.
2. Functions are closure. So they have access to bindings in parent contexts \(Module or parent function\).
3. You can use `_` to define a lambda based on an existing function. Just make a normal call and replace the lambda inputs with `_` \(Example A\).
4. If lambda is assigned to a variable, it can invoke itself from the inside \(Example B\). This can be used to implement recursive calls.

**Examples**

```perl
rr = fn(nothing -> int) { x + y } #here x and y are captures from parent function/struct

test = fn(x:int -> PlusFunc) { fn(y:int -> int) { y + x } } #this function returns a lambda

fn(x:int -> int) { x+1} (10) #you can invoke a lambda at the point of declaration
#A
lambda1 = process(10, _, _) #defining a lambda based on existing function
#B
ff = fn(x:int -> int) { ff(x+1) }
```

