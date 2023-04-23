---
Title: Julia 1.0 Programming Second Edition (Ivo Balbaert)
Author: 邱彼郑楠
Date: 2023-04-01
Modified: 2023-04-22
---

# Configuration

The code in `.juliarc.jl` will be run whenever you start a Julia session.

* `/home/.juliarc.jl` on Ubuntu.
* `C:\Users\username\.juliarc.jl` on Windows;
* `~/.juliarc.jl` on OS X;

# How does Julia work?

Julia works with an LLVM JIT compiler framework that is used for JIT compiler framework.

* The first time you run a Julia function, it is parsed, and the types are inferred. Then, LLVM code is geneerated by the JIT compiler, which is then optimized and compiled down to native code.
* THe second time you run a Julia function, the native code that's already generated is called.

Julia code is fast because it generates specialized versions of functions for each data type.

## Type-stable

For utmost performance, you need to write **type-stable** code.

* Code is type-stable if the type of every variable does not vary over time.
* A function is type-stable if the return type(s) of all the output variables can be deduced from the types of the inputs.

# Basic

Everything in Julia is an expression.

## Names

Names of variables are case-sensitive. Lowercase is used with multiple words separated by an underscore.

The names of types begin with a capital letter, and if necessary, the word separation is shown with Came-Case, such as BigFloat or AbstractArray.

Function names are in lower-case. They can contain Unicode characters.

## Comments

In Julia, all lines between `#=` and `=#` are treated as a comment.

## Types
### Unsigned Integer

Overflow checking is not automatic, so an explicit check (for example, the result has the wrong sign) is needed when this can occur.

### String

Loop over a string's characters can best be done as an iteration and not bny using the index.

### Arrays

When dealing with large arrays, it is better to indicate the final number of elements from the start for the performance. Suppose you know beforehand that `arr2` will need $10^5$ elements, but not more. If you use `sizehint!(arr2, 10^5)`, you'll be able to `push!` at least $10^5$ elements without Julia having to reallocate and copy the data already added, leading ot a substantial improvement in performance.

A `for ... in ` loop over an array is read-only, and you can not change elements of the array inside it. Instead, use an index i.

Slicing operations create **views** into the original array rather than copying the data, so a change in the slice changes the original array or matrix.

To make an array of arrays (a **jagged** array), use an `Array` initialization, and then `push!` each array in its place, for example,

```julia
jarr = (Vector{Int64})[]
push!(jarr, [1, 2])
push!(jarr, [1, 2, 3, 4])
push!(jarr, [1, 2, 3])
```

When working with arrays that contain arrays, it is important to realize that such an array contains **references** to the contained arrays, not their values. If you want to make a copy of an array, you can use the `copy()` function, but this produces only a **shallow** copy with references to the contained array. In order to make a complete copy of the values, we need to use the `deepcopy()` function.

### Dictionaries

In general, dictionaries that have type `{Any, Any}` tend to lead to lower performance since the JIT compiler does not know the exact type of the elements. Dictionaries used in performance-critical parts of the code should therefore be explicitly typed.

When we get an `KeyError`, use the `get` method and provide a default value that is returned instead of the error, i.e., `get(d, key, 999)` returns 999.

## Function

In Julia, a concrete version of a function for a specific combination of argument types is called a **method**.
    
To define a new method for a function (also called **overloading**), just use the same function name but a different signature, that is, with different argument types.

A list of all the methods is stored in a virtual method table (vtable) on the function itself; methods do not belong to a particular type.

When a function is called, Julia will lookup in vtable at runtime to find which concrete method it should call, based on the types of all its arguments; this is Julia's **multiple dispatch mechanism**.

Note that only positional arguments are taken into account for multiple dispatch, and not keyword arguments.

All arguments to functions (with the exception of plain data such as numbers and chars) are passed by **reference**.

## Anonymous Function

Anonymous functions are mostly used when passing a function as an argument to another function.

## Control Flow

Using short-circuit evaluation, statements with `if...only` are often written as follows:

* `if <cond> <statement> end` is written as `<cond> && <statement>`, which can be read as `<cond>` and then `<statement>`;
* `if !<cond> <statement> end` is written as `<cond> || <statement>`, which can be read as `<cond>` or else `<statement>`.

# Linear Algebra in Julia
## Identity Matrix

Use the `I` function (from the `LinearAlgebra` package), i.e., 

```julia
using LinearAlgebra
idm = Matrix(1.0*I, 3, 3)
```

## Linear Equations

Suppose you want to solve the $AX=B$ equation, where $A,X$ and B are matrices. The obvious solution is `X = inv(A) * B`. However, this is actually not that goog. It is better to use the built-in solver, where `X = A \ B`. If you have to solve the $XA=B$ equation,, use the solution `X = B / A`. Solutions that use `/` and `\` are much more numerically stable, and also much faaster.

# Regular expressions

* use `occursin(regex, string)` in an `if` expression;
* `match(regex, string)` returns nothing when there is no match, otherwise, it returns an object of type RegexMatch.
    * `match` contains the entie substring that matches;
    * `offset` states at what position the matching begins;
    * `line` for each of the captured substrings;
    * `cpatures` ccontains the cpatured substrings as a tuple.
* `matchall(regex, string)` and `eachmatch(regex, string)` for working with all the matches.
