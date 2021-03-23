# Struct



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

