# Types

Types are blueprints which are used to create values for bindings.

Types can be basic \(integer number, character, ...\) or compound \(sequence, map, struct, union\).



## Type name resolution

1. Order of search to resolve a type name:
2. Current function
3. Closure
4. Module level
5. At any level, if there are multiple candidates there will be a compiler error.
6. Two named types are never equal. 
7. Two types T1 and T2 are identical/assignable/exchangeable if they have the same structure \(e.g. `int|string` vs `int|string`\).

## Basic Types

**Syntax**: `int, float, byte, char, string, bool, nothing`

**Notes**:

1. `int` type is a signed 8-byte integer data type.
2. `float` is double-precision 8-byte floating point number.
3. `byte` is an unsigned 8-bit number.
4. `char` is a single unicode character.
   * Character literals should be enclosed in single-quote \(e.g. `'a'`\).
5. `string` is a sequence of characters.
   * String literals should be enclosed in double quotes.
   * To represent double quote itself inside a string, you can use `\"`.
6. `bool` type is same as int but with only two valid values. `true` is 1 and `false` is 0.
7. `nothing` is a special type which is used to denote empty/invalid/missing data. This type has only one value which is the same identifier.

**Examples**

```perl
int_val = 12
float_val = 1.918
char_val = 'c'
bool_val = true
str1 = "Hello world!"
str2 = "Hello" + "World!"
n: nothing = nothing
byte_val: byte = 119 #note that it is optional to mention type of a binding after its name
```

### 

## Sequence

1. Sequence is similar to array in other languages. It represents a fixed-size block of memory with elements of the same type, `T`, and is shows with `[T]` notation. 
2. You can initialize a sequence with a sequence literal \(First example\).
3. You refer to elements inside sequence using `x[i]` notation where `i` is index number. 
4. `[]` represents an empty sequence.
5. Referring to an index outside sequence will throw a runtime error.
6. Core defines built-in functions for sequence for common operations: `slice, map, reduce, filter, anyMatch, allMatch, ...`

**Examples**

```perl
x = [1, 2, 3, 4]

#a 2D matrix of integer numbers
x: [[int]] = [ [1, 2], [3, 4], [5, 6] ] 

#merging multiple sequences
x = [1, 2]+[3, 4]+[5, 6] 

int_var = x[10]

#this is definition of string type
string = [char]
```



## Map

1. HashMap is a hash table of key values.
2. You can use `[KeyType:ValueType]` to define a map type. 
3. When reading from a map, you will get runtime error if value does not exist in the map.
4. An empty map can be denoted using `[:]` notation.
5. Core defines built-in functions for maps for common operations: `slice, map, reduce, filter, anyMatch, allMatch, ...`

**Examples**

```perl
pop = ["A":1, "B":2, "C":3]
data = pop["A"]
```



## Enum

1. You can prefix any sequence literal with `enum` keyword and it will be an enum type.
2. Example: `MyEnumType = enum [sequence of literals]`
3. Variables of enum type must accept values of exactly what is specified inside the sequence, nothing else, even if they have equivalent value.
4. You can combine enum with a map to implement execution control. 
5. In case of 4, Compiler will make sure you have covered all possible types, and if not, will issue a warning.
6. Also core will have functions to implement `switch` on enums which make sure all cases are covered.

**Examples**

```perl
saturday=1
sunday=2
...
DayOfWeek = enum [saturday, sunday, ...]

x = [saturday: "A", sunday: "B", ...][my_day_of_week]

#definition of type bool
true=1
false=0
bool = enum [true, false]
```



## Union

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



## Strut

1. A struct, similar to C, represents a set of related named types. 
2. To create a binding based on a struct, you should use a struct literal \(e.g. `Type{field1:value1, field2:value2, ...}`.
3. Optional fields: When creating a value of struct type and don't specify value for fields which can be `nothing`, they will be set to `nothing`.
4. Edit: You can create a new struct value based an existing value. This will merge them all. \(Example A\).
5. If struct literal type can be inferred from context, you can omit type and use `&{...}` notation \(Example B\).

**Examples**

```perl
#defining a struct type
Point = struct {x:int, y:int}

#create a binding of type Point, defined above
point2 = Point{x:100, y:200}
point2new = Point{100, 200}

#update an existing struct binding and save as a new binding
point4 = Point{x:point3.x, y : 101}

process = fn(x: struct {id:int, age:int} -> int) { x.age }

#A
another_point = Point{my_point, x:10}
third_point = Point{point1, z: 10, delta: 9}

#B
switchOnValue(my_number, &{value: 10, handler: AAA}, &{12, BBB}, &{13, CCC})
```



## Named Types

1. You can name a type so you will be able to refer to that type later in the code.
2. Type names must start with a capital letter to be distinguished from bindings.
3. You define a named type similar to a binding: `NewType = UnderlyingType`.
4. The new type has same binary representation as the underlying type but it will be treated as a completely different type.
5. You have seen examples of named types in previous sections \(Union, enum, ...\).

**Examples**

```perl
MyInt = int
IntArray = [int]
Point = struct (x: int, y: int)
```



## Type Alias

1. You can use `T : X` notation to define `T` as another spelling for type `X`.
2. In this case, `T` and `X` will be exactly the same thing.
3. You can use a type alias to prevent name conflict when importing modules.
4. `X` on the right must be a type name. It cannot be definition of a type.

**Examples**

```perl
MyInt : int
process = fn(x:MyInt -> int) { x }
```



## Type Casting

1. We use `T(value)` notation to cast value to a specific type.
2. Casting can be done for primitive types, named types or unions.
3. For union, you can use casting to get underlying type. If you cast a union binding to a wrong type, there will be a runtime error.
4. You can cast a union to `T|nothing` to do a safe cast. You will get `nothing` it type T is not inside the union binding.
5. Literals \(e.g. `1` or `"Hello world"`\) will get value of the most primitive type inferred by the compiler \(`int`, `string`, ...\). 
6. Based on 4, you cannot assign an untyped literal to a named type without casting. Because for example `1` literal is an `int` literal not a named type that maps to `int`.

**Examples**

```perl
MyInt = int
myint_var = MyInt(12)
```
