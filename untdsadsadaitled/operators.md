# Operators



Operators are mostly similar to C language:

* Conditional operators: `and, or, not, ==, !=, >=, <=`
* Arithmetic: `+, -, *, /, %, %%, >>, <<, **`
* Note that `==` will do a comparison based on contents of its operands.
* `A // B` will evaluate to A if it is not `nothing`, else it will be evaluated to B \(e.g. `y = x // y // z // 0`\).
* `A ? B` will evaluate boolean expression A first, if true will evaluate to B, otherwise will evaluate to `nothing`. This can be mixed with `//` to provide ifElse construct.
* Example: `home_dir = (is_root ? "/root") // (is_default_user ? "/default") // (is_unknown ? "unknown") // "/tmp"`
* Conditional operators return `true` or `false` which are equal to `1` and `0` respectively when used as index of a sequence.
* Comments can appear anywhere in the code and start with `#`. Anything after `#` till end of the line is comment.
* Meta comments start with `##` as first two characters of the line and can be defined for a binding, type or function. These will be scanned with tools to automatically generate documentation. If `##` is the only thing in the line, it starts a block comment until another `##` appears in the file.

  ```elixir
    ## 
    some docs about this function
    x:int - comments about this input
    -> string - comments about the output
    ##
    process = fn(x:int -> string) { ... }

    ##Meta comment in one line
    x = 12

    ## 
    some docs about this type
    x:int - comments about this field
    y: string - comments about the y
    ##
    DataTypeX = struct {x:int, y:string}
  ```

