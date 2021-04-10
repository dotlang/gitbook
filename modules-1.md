# Modules



1. Modules are source code files. 
2. You can import a module into current module and use their declarations. This can only be done at module level. 
3. You can import modules from local file-system, GitHub or any other external source which the compiler supports.
4. If import path starts with `.` or `..` it is a relative path \(Example A\), if it start with `/` it is based on project root \(Example B\).
5. Project root is where the compiler is executed.
6. If the specific absolute module path does not exist, compiler will look into parent modules \(the module that has imported this module\). If still not found, compiler will try to download it from web. 
7. Compiler will support specifying specific branch/release/commit when importing a module. 
8. Compiler will keep track of current module root and all parent module roots. 
9. The result of importing a module is called a module alias which if named, should be named like a binding and used with `..` notation to access definitons inside module. 
10. You can ignore output of an import to have its definitions inside current namespace. 
11. You can use `..{}` notation to only access some of module's symbols \(Examples C and D\).
12. Absolute paths that start with http or https will be downloaded from the net if not available locally.
13. You can use `@` notation to indicate required tag or branch name. This part allows using `+` and `*` to indicate versions equal or higher to x or any version are acceptable \(Example E\).
14. Module level bindings with literal values \(constants\) must be all caps.
15. Note that the notation to fetch multiple type/bindings from module does not give you an expression usable in a function call. \(Example F\)

**Syntax**

`ModuleName = import("/path/to/module")`

**Examples**

```perl
#A
Socket = import("../core/st/socket")

#B
Socket = import("/core/st/socket")

base_cassandra = "/path/to/cassandra"

#you can use a string literals expression for import path
Module = import(base_cassandra + "/path/module") 

Set = import("/core/set")..SetType
process = fn(x: Set -> int) { ... }

my_customer = import("/data/customer")..Customer(name:"mahdi", id:112)

#E
T = import("/https/github.com/uber/web/@v1.9+.*/request/parser")
T = import("/https/github.com/uber/web/@new_branch/request/parser")
T = import("/https/server.com/web/@v1.9+.*.zip/request/parser")

#C
Set, process, my_data = import("/core/set")..{SetType, processFunc, my_data}
a, b, c = T..{a, b, c}

#D
Set, process, my_data = imported_module..{SetType, processFunc, my_data}

#F - you cannot use ..{} inside an expression
result = processData(T..{a, b, c}) #this is WRONG! 

```



