# Function Call Resolution



1. We use a static dispatch for function calls. 
2. Also because you cannot have two functions with the same name, it is easier to find what happens with a function call.
3. If `MyInt = int`, you cannot call a function which needs an `int` with a `MyInt` binding.
4. Fucntion resolution is done similar to type name resolution. 
5. Parameter types must be "identical/compatible" to function argument types, or else there will be a compiler error. 
6. For example if function argument type is `int | nothing` and parameter is an `int` it is a valid function call \(But not the other way around\).
7. When you need a function of type `fn(T->U)` any function that can accept T \(or more\) and returns U \(or less\) works fine.

