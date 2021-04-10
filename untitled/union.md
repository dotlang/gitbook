# Union



1. Bindings of union type, can store any of multiple pre-defined types.
2. Union type are shown as `T1|T2|T3|...`. 
3. You can use casting to check what's inside a union binding or cast it to a type.

**Examples**

```perl
int_or_float: int|float = 11
int_or_float: int|float = "ABCD"

my_int = int(int_or_float) #this will fail if input binding does not have an int
maybe_int = int|nothing(int_or_float) #if binding has a float, you will get a nothing as a result of this cast


```

