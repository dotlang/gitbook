# Sequence



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

