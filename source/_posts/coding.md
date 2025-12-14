---
title: Programming Tricks
date: 2022-02-07 23:52:42
tags:
categories:
- coding
---

## Julia

`parentmodule`:  determine the package a function in Julia originates from

`names`: Get a vector of the public names of a Module, excluding deprecated names

`undef`: undef is a special marker used when constructing arrays (including vectors) to indicate that the elements of the array should not be initialized to any specific value.

`collect`: return an Array of all items in a collection or iterator, `collect(2:5)`, `collect('B':'D')`, `collect("HELLO")`

`!`: a function naming convention to indicate that a function mutates its arguments in place, meaning the changes will be visible outside the function. When a function is designed to modify its arguments, it is good practice to append a `!` (exclamation mark) to its name

`eltype`: To find the type of the elements that are iterated over in a collection

`typeof`: To determine the specific type of any given value

```julia
pizza_tuple = ("hawaiian", 'S', 10.5)
typeof(pizza_tuple) # Tuple{String, Char, Float64}
eltype(pizza_tuple)	# Any

arr = [1,2,3]
typeof(arr)		# Vector{Int64} (alias for Array{Int64, 1})
eltype(arr)		# Int64
```

`Any`: It is used to construct a heterogeneous array that can hold elements of any type, like `Any[1, "hello", 3.14]`

`^`: Repeat a regex `n` times (`s^n` is same with `repeat(s, n)`); Exponentiation operator

`parse`:  convert a text string to anything else. `parse(Int, "42")`, `parse(Float64, "42")`

String `*` : concatenate strings, `"The " * engine *`

String `$`:   string interpolation,  use `$(variable)` instead of `$variable` when there
is no whitespace that can clearly distinguish the variable name from the surrounding text

`vec`: Reshape the array as a *one-dimensional column vector*

`pkg> dev|develop`: add a local package, which not initialized by git

`using|import .MyModule`:  relative import following`include("path/to/MyModule.jl")` custom module

---

***Instantiate the project***

`instantiate` command to download and install all packages and their dependencies listed in `Project.toml` (and `Manifest.toml` if present)



---

***create a new project***

```
$ julia
```

`]`

```
(@v1.12) pkg> generate MyNewProj
```

`;`

```
shell> cd MyNewProj/
```

`]`

```
(@v1.12) pkg> activate .
```



---

***dictionary***

```julia
pizza = Dict("name" => "hawaiian", "size" => 'S', "price" => 10.5)
```

A problem with using a dictionary is that it requires every value to be of the *same type*

```julia
typeof(pizza)	# Dict{String, Any}
```



---

***symbols***

 It is denoted by *`:` (colon), followed by the name of the symbol,* built-in Julia type to represent identifiers



---

 ***named tuples***

```julia
pizza = (name = "hawaiian", size = 'S', price = 10.5)
```

A named tuple only allows you to use *symbols* as keys

All types of tuples are *immutable*, meaning you cannot change them



implicit naming from identifiers

```julia
x = 0
t = (; x) # t is (x = 0,)
u = (; t.x) # u is (x = 0,)
```



---

***composite type*** (`struct`) & ***type annotation***

`::` is used to annotate variables and expressions with their type. `x::T` means variable `x` should have type `T`. It helps Julia figure out how many bytes are needed to hold all fields in a `struct`

```julia
struct Archer
    name::String
    health::Int
    arrows::Int
end
```



---

 ***closure***



---

***varargs***

"varargs" (variable arguments) refers to the ability of a function to accept an arbitrary number of arguments. This is achieved using the *splat operator* (`...`) in the function definition.

```julia
function my_sum(a, b, rest...)
    total = a + b
    for x in rest
        total += x
    end
    return total
end
```

```julia
my_sum(1, 2, 3, 4, 5)	# 15
```

---

***keyword arguments***

a *semicolon* (`;`) separates positional arguments from keyword arguments in the function signature. All arguments to the right of the semicolon are treated as keyword arguments. They can optionally have default values



---

***views***

A `view` is essentially a ***pointer*** to a sub-section of another vector, but not a standalone vector itself

```julia
one2ten = collect(1:10);
println(one2ten)

one2five = one2ten[1:5]
one2five_view = view(one2ten, 1:5)

one2ten[1] = 10
println(one2five)
println(one2five_view)

# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# [1, 2, 3, 4, 5]
# [10, 2, 3, 4, 5]
```

> `@views` is a macro that converts sliced arrays into views (pointers are much cheaper than creating copies of arrays). For more information on how to use the `view` syntax correctly



---

***semicolon after steprange***

placing a semicolon `;` after a step range expression inside square brackets, e.g., `[1:10;]`, changes the resulting object from a `UnitRange` to a `Vector`

```julia
b = [1:2:10]	# Vector{StepRange{Int64, Int64}}
a = [1:2:10;]	# Vector{Int64}

size(b)	# (1)
size(a)	# (5)
```



---

***element-wise operations***

*Dot syntax for operators*: For binary operators like `+`, `-`, `*`, `/`, `^`

*Dot syntax for functions*: For functions, the dot is placed after the function name.

---

***Property destructuring*** 

```julia
julia> (; b, a) = (a=1, b=2, c=3)
(a = 1, b = 2, c = 3)

julia> a
1

julia> b
2
```



---

***One-line functions***

"*one-line function*" also known as the compact "*assignment form*"

```julia
function_name(parameters) = expression
```

---

***Anonymous Functions (Lambda Functions)***

functions without a name `(parameters) -> expression`, often defined inline for use with higher-order functions like `map`, `filter`, or `reduce`

```julia
numbers = [1, 2, 3]
doubled_numbers = map(x -> 2 * x, numbers) # doubled_numbers will be [2, 4, 6]
```



---

***`using` vs `import`***

that’s the difference between using and import - the former brings all exported names into scope, while the latter only brings NiceStuff (the module identifier) into scope.

> [[https://discourse.julialang.org/t/difference-between-include-use-and-import/65918/5](https://discourse.julialang.org/t/difference-between-include-use-and-import/65918/5)]



## Conditional Compilation In C++

### Using g++ only

**conditional.cpp**

```c++
#include <iostream>

#define na 4

int main() {
  int a[na];

  a[0] = 2;
  for (int n = 1; n < na; n++) a[n] = a[n-1] + 1;

#ifdef DEBUG
  // Only kept by preprocessor if DEBUG defined
  for (int n = 0; n < na; n++) {
    std::cout << "a[" << n << "] = " << a[n] << std::endl;
  }
#endif 
  
  return 0;
}
```

---

**-DDEBUG** args

```bash
$ g++ -Wall -Wextra -Wconversion conditional.cpp -o conditional
$ ./conditional
$ g++ -Wall -Wextra -Wconversion conditional.cpp -o conditional -DDEBUG
$ ./conditional
a[0] = 2
a[1] = 3
a[2] = 4
a[3] = 5
```

---

---

### Using **CMakeLists.txt** *add_definitions*

```cmake
cmake_minimum_required(VERSION 3.2)

option(DEBUG "Option description" OFF)

if(DEBUG)
    add_definitions(-DDEBUG)
endif(DEBUG)

add_executable(cond conditional.cpp)
```

---

**without debug**

```bash
$ cmake ..
$ make
$ ./cond
```

**with debug**

```bash
$ cmake -DDEBUG=ON ..
$ make
$ ./cond
a[0] = 2
a[1] = 3
a[2] = 4
a[3] = 5
```

