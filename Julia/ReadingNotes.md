---
Title: Julia 语言读书笔记
Author: 邱彼郑楠
Date: 2023-04-01
Modified: 2023-04-15
---

# Julia 1.0 Programming Second Edition (Ivo Balbaert)

1. The code in `.juliarc.jl` will be run whenever you start a Julia session.
    * `C:\Users\username\.juliarc.jl` on Windows;
    * `~/.juliarc.jl` on OS X;
    * `/home/.juliarc.jl` on Ubuntu.

2. Julia works with an LLVM JIT compiler framework that is used for JIT compiler framework.
    * The first time you run a Julia function, it is parsed, and the types are inferred. Then, LLVM code is geneerated by the JIT compiler, which is then optimized and compiled down to native code.
    * THe second time you run a Julia function, the native code that's already generated is called.

3. Julia code is fast because it generates specialized versions of functions for each data type.

4. Everything in Julia is an expression.

5. Names of variables are case-sensitive. Lowercase is used with multiple words separated by an underscore.

    The names of types begin with a capital letter, and if necessary, the word separation is shown with Came-Case, such as BigFloat or AbstractArray.

    Function names are in lower-case. They can contain Unicode characters.

6. In Julia, all lines between `#=` and `=#` are treated as a comment.

7. For utmost performance, you need to write type-stable code. Code is type-stable if the type of every variable does not vary over time.

8. Overflow checking is not automatic, so an explicit check (for example, the result has the wrong sign) is needed when this can occur.

9. Loop over a string's characters can best be done as an iteration and not bny using the index.

10. Regular expressions
* use `occursin(regex, string)` in an `if` expression;
* `match(regex, string)` returns nothing when there is no match, otherwise, it returns an object of type RegexMatch.
    * `match` contains the entie substring that matches;
    * `offset` states at what position the matching begins;
    * `line` for each of the captured substrings;
    * `cpatures` ccontains the cpatured substrings as a tuple.
* `matchall(regex, string)` and `eachmatch(regex, string)` for working with all the matches.

11. When dealing with large arrays, it is better to indicate the final number of elements from the start for the performance. Suppose you know beforehand that `arr2` will need $10^5$ elements, but not more. If you use `sizehint!(arr2, 10^5)`, you'll be able to `push!` at least $10^5$ elements without Julia having to reallocate and copy the data already added, leading ot a substantial improvement in performance.

12. A `for ... in ` loop over an array is read-only, and you can not change elements of the array inside it. Instead, use an index i.

13. All arguments to functions (with the exception of plain data such as numbers and chars) are passed by **reference**.

14. **Anonymous functions** are mostly used when passing a function as an argument to another function.

15. In Julia, a concrete version of a function for a specific combination of argument types is called a **method**.
    
    To define a new method for a function (also called **overloading**), just use the same function name but a different signature, that is, with different argument types.

    A list of all the methods is stored in a virtual method table (vtable) on the function itself; methods do not belong to a particular type.

    When a function is called, Julia will lookup in vtable at runtime to find which concrete method it should call, based on the types of all its arguments; this is Julia's **multiple dispatch mechanism**.

    Note that only positional arguments are taken into account for multiple dispatch, and not keyword arguments.

# Interactive Visualization and Plotting with Julia (Diego Javier Zea)

1. Julia defines project environments using two files.
    * `Project.toml` file that stores the set of dependencies.
    * `Manifest.toml` file that stores the exact version of all the packages and their dependencies.

While the former is mandatory for any environment, the latter is optional.

2. There are multiple options for dealing with project environments.
    * start `julia` in a given environment by using the `--project` argument.
    * change between environments using the `activate` command in `Pkg` mode.
    * run the `instantiate` command of `Pkg` mode to get all the needed packages when you first activate a non-empty environment on your system.
