# Binding Declaration



1. A binding assigns an identifier to a typed immutable memory location. 
2. A binding's value can be a literal value, an expression or another binding.
3. The literal value can be of any valid type \(integer number, function literal, struct literal, ...\). 
4. Binding names must start with a lowercase letter \(except bindings that define a generic type, more in Advanced section\).
5. You can define bindings at module-level or inside a function. 
6. Module-level bindings can only have literals as their value. 
7. Type of a binding can be inferred without ambiguity from right side value, but you also have the option to specify the type \(Example A\).
8. If the right side of an assignment is a struct, you can destruct it into its elements by using comma separated values on the left side of `=` \(Example B\). 
9. In destruction, you can also use underscore to indicate you are not interested in one or more of those elements \(Example C\).
10. Binding name resolution is similar to type/function name resolution.

**Syntax**:

1. `identifier = expression`
2. `identifier : type = expression`

**Examples**

```perl
#A
x : int = 12

#type is inferred
g = 19.8 

#B
a,b = Tuple{1, 100}

#C
a,_ = point

a,_ = single_element_struct
```

