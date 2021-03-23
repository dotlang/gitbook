# Function Definition

Functions \(or lambdas\) are a type of binding which can accept a set of inputs and gives an output.

For example `fn(int,int -> int)` is a function type \(which accepts two integer numbers and gives an integer number\) and `fn(x:int, y:int -> int) { x+y }` is a function literal.

For generics \(types and functions\) see Advanced section.

### Declaration

1. `functionName = fn(name1: type1, name2: type2... -> OutputType1, OutputTyp2, ...) { code block }`
2. Function names are camelCased.
3. Functions contain a set of bindings and the last expression in the code block determines function output.
4. If calling a function that returns multiple bindings, you can use `_` to ignore one of them.
5. There is no function overloading. Functions should have unique names in their context.
6. You can alias a function by defining another binding pointing to it \(example A\). 
7. If a function has no input, you can can eliminate input/output type declaration part \(Example B\). In this case, compiler will infer output type.
8. If a function is being called with literals \(compile time known values\), compiler will try to evaluate it during compilation \(e.g. generics\). 
9. Module level functions that start with `_test` and have no input/output are considered unit test functions. You can later instruct compiler to run them \(Example D\).
10. There is `assert` core function that can be used for checking assertions. You can disable assertions with a compiler flag.
11. You can chain multiple nested function calls in reverse order via `::` operator \(Example E\).
12. If a function returns multiple outputs you can simply send its output to another function if they match \(Example F\).

**Examples**

```perl
myFunc = fn(x:int, y:int -> int) { 6+y+x }

tester = fn(x:int -> int, string) {x+1, "a"}
int1, str1 = tester(100)
int1, _ = tester(100)
_, str1 = tester(100)

log = fn(s: string -> nothing) { print(s) } #this function returns nothing, pun not intended

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

## 

