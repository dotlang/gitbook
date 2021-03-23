# Basic Types



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

