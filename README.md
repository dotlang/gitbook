# Introduction

> _Perfection is finally attained not when there is no longer anything to add, but when there is no longer anything to take away.  
> **\(Antoine de Saint-Exupéry, translated by Lewis Galantière.\)**_

**dotLang** is a general-purpose programming language which is built upon a small set of consistent rules and a minimum number of exceptions.

### Why dotLang?

Because it is:

1. **Simple**: There are a few key concepts and features that you need to learn. With a very smooth learning curve, you will not need to keep in mind an endless array of rules and exceptions. This helps developers write code easily and more importantly, understand a written code better. Which results in a maintainable and high quality software. We avoid hidden, behind the scene stuff where only compiler or runtime know about. Most of the stuff that happens is explicitly declared by the developer.
2. **Powerful**: The fact that dotLang is simple, combined with orthogonality of the tools that the language gives you, makes it an immensely powerful tool. You can easily mix and match different tools that the language offers and all the way, compiler is with you to do as much as possible.
3. **Fast**: dotLang is a compiled language. Because of its simplicity, compiler is able to quickly compile a large source code set in a short period of time. Additionally, runtime performance is taken into consideration in compiler design and implementation.

dotLang is very similar to C but with some significant improvements:

1. Module system \(no header files!\)
2. First-class functions
3. Support for generics
4. Full immutability
5. No reference types, no pointers, no manual memory management
6. Support for sum types and map types
7. Powerful concurrency model
8. And much more!

### A bit of history

After having worked with a lot of different languages \(C\#, Java, Scala, Perl, Javascript, C, C++, Go and Python\) and getting familiar with some others \(including D, Swift, Erlang, Rust, Zig, Crystal, Fantom, OCaml, Nim and Haskell\) it still irritates me that most of these languages sometimes seem to _intend_ to be overly complex with a lot of rules and exceptions to keep in mind. This doesn't mean I don't like them or I cannot develop software using them, but it also doesn't mean I should not be looking for a programming language which is simple, powerful and fast.

That's why I am creating a new programming language: **dotLang**.

dot programming language \(or dotLang for short\) is an imperative, static-typed, garbage collected, functional, general-purpose language based on author's experience and doing research on many programming languages \(namely [Go](https://golang.org/), [Java](https://docs.oracle.com/javase/tutorial/), [C\#](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/), [C](https://en.cppreference.com/w/c), [C++](https://en.cppreference.com/w/), [Scala](https://www.scala-lang.org/), [Rust](https://www.rust-lang.org/), [Objective-C](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html), [Swift](https://swift.org/), [Python](https://python.org/), [Perl](https://www.perl.org/), [Smalltalk](https://en.wikipedia.org/wiki/Smalltalk), [Ruby](https://www.ruby-lang.org/en/), [Haskell](https://www.haskell.org/), [Clojure](https://clojure.org/), [Eiffel](https://www.eiffel.org/), [Erlang](https://www.erlang.org/), [Elixir](https://elixir-lang.org/), [Elm](https://elm-lang.org/), [Falcon](http://www.falconpl.org/), [Julia](https://julialang.org/), [Zig](https://ziglang.org/), [F\#](https://fsharp.org/) and [Oberon-2](https://cseweb.ucsd.edu/~wgg/CSE131B/oberon2.htm)\). I call the paradigm of this language "Data-oriented". This is an imperative language which is also very similar to Functional approach and it is designed to work with data. There are no objects or classes. Only data structures and functions. We have first-class and higher-order functions borrowed from the functional approach.

Two main objectives are pursued in the design and implementation of this programming language:

1. **Simplicity**: The code written in dotLang should be consistent, easy to write, read and understand. There has been a lot of effort to make sure there are as few exceptions and rules as possible. Software development is complex enough. Let's keep the language as simple as possible and save complexities for when we really need them. Very few \(but essential\) things are done implicitly and transparently by the compiler or runtime system. Also, I have tried to reduce the need for nested blocks and parentheses, as much as possible. Another aspect of simplicity is minimalism in the language. It has very few keywords and rules to remember.
2. **Performance**: The source will be compiled to native code which will result in higher performance compared to interpreted languages. The compiler tries to do as much as possible \(optimizations, dereferencing, in-place mutation, sending by copy or reference, type checking, phantom types, inlining, disposing, reference counting GC, ...\) so runtime performance will be as high as possible. Where performance is a concern, the corresponding functions in core library will be implemented in a lower level language.

Achieving both of the above goals at the same time is impossible, so there will definitely be trade-offs and exceptions. The underlying rules of design of this language are [Principle of least astonishment](https://en.wikipedia.org/wiki/Principle_of_least_astonishment), [KISS rule](https://en.wikipedia.org/wiki/KISS_principle) and [DRY rule](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

As a 10,000 foot view of the language, the code is written in files \(called modules\) organized in directories \(called packages\). We have bindings \(immutable data which can be functions or values\) and types \(Blueprints to create bindings\). Type system includes primitive data types, sequence, map, enum, struct and union. Concurrency and lambda expression are also provided.

### Comparison

| Language | First-class functions | Sum types | Full Immutability | Garbage Collector | Module System | Concurrency\* | Generics | built-in data types | Number of keywords |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| C | No | Partial | No | No | No | No | No | 14 | 32 |
| Scala | Yes | Yes | No | Yes | Yes | Yes | Yes | 9 | ~27 |
| Go | Yes | No | No | Yes | Yes | Yes | No | 19 | 25 |
| Java | Yes | No | No | Yes | Yes | No | Yes | 8 | 50 |
| Haskell | Yes | Yes | No | Yes | Yes | No | Yes | 63 | 28 |
| dotLang | Yes | Yes | Yes | Yes | Yes | Yes | Yes | 8 | 9 |

* Concurrency means built-in language level support.

### Components

dotLang consists of these components:

1. The language manual \(this website\).
2. `dot`: A command line tool to compile, debug and package source code.
3. `core` library: This package is used to implement some built-in, low-level features which can not be simply implemented using pure dotLang. This will be a built-in feature of the compiler/runtime.
4. `std` library: A layer above core which contains some general-purpose and common functions and data structures. This is optional to use by developers.

## Grammar

Grammar of dotLang in a notation similar to EBNF can be found [here](./grammar.md)

### 

