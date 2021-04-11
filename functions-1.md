# Functions

## Function Definition

Functions \(or lambdas\) are a type of binding which can accept a set of inputs and gives an output.

For example `fn(int,int -> int)` defines a function type \(which accepts two integer numbers and gives an integer number\) and `fn(x:int, y:int -> int) { x+y }` is a function literal which given two numbers, returns their sum.

### Declaration

1. `functionName = fn(name1: type1, name2: type2... -> OutputType1, OutputTyp2, ...) { code block }`
2. Function names must be camelCased.
3. Functions contain a set of bindings and the last expression in the code block determines function output \(except for errors which can be returned early using at operator\).
4. If calling a function that returns multiple bindings, you can use `_` to ignore some of them.
5. There is no function overloading. Functions should have unique names in their container module.
6. You can alias a function by defining another binding pointing to it \(example A\). 
7. If a function has no input, you can can eliminate input/output type declaration part \(Example B\). In this case, compiler will infer output type.
8. If a function is being called with literals \(compile time known values\), compiler will try to evaluate it during compilation \(e.g. generics\). 
9. Module level functions that start with `_test` and have no input/output are considered unit test functions. You can later instruct compiler to run them \(Example D\).
10. There is `assert` core function that can be used for checking assertions. You can disable assertions with a compiler flag.
11. You can chain multiple nested function calls in reverse order via `::` operator \(Example E\).
12. If a function returns multiple outputs you can simply send its output to another function if they match \(Example F\).

**Examples**

```objectivec
myFunc = fn(x:int, y:int -> int) { 6+y+x }

tester = fn(x:int -> int, string) {x+1, "a"}
int1, str1 = tester(100)
int1, _ = tester(100)
_, str1 = tester(100)

#this function returns nothing, pun not intended
log = fn(s: string -> nothing) { print(s) } 

process2 = fn(pt: Point -> int,int) { pt.x, pt.y } #this function returns a struct

process = fn(x: int|Point -> int) { ... } #this function can accept either int or Point or int|Point as input

process = fn(x:int -> int) 
{ 
  #if x<10 return 100, otherwise return 200
  [x<10: 100, x>=10: 200][true]
}

#A
process = fn(x:int -> int) { x+1 }
process2 = process

sorted = sort(my_sequence, fn(x,y -> int) { x-y })

Adder = fn(int,int->int) #defining a named type based on a function type

sort = fn(x: [int], comparer: fn(int,int -> bool) -> [int]) {...} #this function accepts a function

map = fn(input: [int], mapper: fn(int -> string) -> [string]) ...

#B
process = fn{ 100 }

#D
_testProcessWithInvalidInput = fn{...}

#E
resut = f(g(x)) 
result = x :: g :: f
# calculate average score for new good students
student :: filter(isGoodStudent, _) :: map(createNewStudent, _) :: calculateAverage

#F
average3Integers(get3numbers())
```

## Lambdas

1. All functions are lambdas.
2. Functions are closure. So they have access to bindings in parent contexts \(Module or parent function\).
3. You can use `_` to create a lambda based on an existing function. Just make a normal call and replace the lambda inputs with `_` \(Example A\).
4. If lambda is assigned to a variable, it can invoke itself from the inside \(Example B\). This can be used to implement recursive calls.

**Examples**

```objectivec
#here x and y are captures from parent function/struct
rr = fn(nothing -> int) { x + y } 

#this function returns a lambda
test = fn(x:int -> PlusFunc) { fn(y:int -> int) { y + x } } 

#you can invoke a lambda at the point of declaration
fn(x:int -> int) { x+1} (10) 

#A
#defining a lambda based on existing function
lambda1 = process(10, _, _) 

#B
ff = fn(x:int -> int) { ff(x+1) }


```

## Optional Arguments

When defining a function, you can use `:>` instead of `:` between argument name and type to indicate that, if that argument is missing when function is called, compiler or runtime should pass a default value for that argument. This default value is determined based on the type of the argument.

1. If type is union with an option for `nothing`, then nothing is the default value.
2. If type is a number \(int, float, char, byte\), zero is the default value.
3. There are other default values for generic types which are explained in Generics section.

Note that optional arguments should be placed at the end of argument list.

```elixir
#A
process = fn(x:int, y:>int -> string) { ... }

#below are the same
result = process(100)
result = process(100, 0)

#B
process = fn(y:int, x:>int|nothing, z:> int -> string) { ... }

result = process(100, 20)

#below are also the same
result = process(10, nothing, 0)
result = process(10)

```

## Function Call Resolution

1. We use a static dispatch for function calls. So the target function in a function call is determined at compile time.
2. Also because you cannot have two functions with the same name, it is easier to find what happens with a function call.
3. If `MyInt = int`, you cannot call a function which needs an `int` with a `MyInt` binding. Because as mentioned before, these two are completely different types.
4. Function resolution is done similar to type name resolution. 
5. Parameter types must be "identical, exchangeable or compatible" to function argument types, or else there will be a compiler error. 
6. For example if function argument type is `int | nothing` and parameter is an `int` it is a valid function call \(But not the other way around\).
7. When you need a function of type `fn(T->U)` any function that can accept T \(or more, like `T|Y`\) and returns U \(or less\) works fine.

