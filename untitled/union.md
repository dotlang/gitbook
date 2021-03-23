# Union



1. Bindings of union type, can store any of multiple pre-defined types.
2. Union type are shown as `T1|T2|T3|...`. 
3. You can use casting to check what's inside a union binding or cast it to a type.
4. You can define a union to be open. This means that other places in the code can add other options for the union \(Example B\). Note that if your code works with a open union, it should take into account that during compilation there might be options for the union, other than ones specified in the same module. 
5. Open unions can be useful when combined with contracts \(Explained in Generics section\).

**Examples**

```perl
int_or_float: int|float = 11
int_or_float: int|float = "ABCD"

my_int = int(int_or_float) #this will fail if input binding does not have an int
maybe_int = int|nothing(int_or_float) #if binding has a float, you will get a nothing as a result of this cast

#B
Shape = || #declare an open union
Shape |= Circle #add a new option to Shape union
#later in the code
Shape |= Triangle
```

