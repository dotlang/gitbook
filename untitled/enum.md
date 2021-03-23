# Enum



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

