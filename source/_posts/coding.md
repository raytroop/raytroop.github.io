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





---

***UnitRange to Array***

a `UnitRange` is a specific type of range that represents a sequence of integers with a step of 1

`UnitRange` objects are "lazy" and efficient. They do not allocate memory for all elements in the range until explicitly converted to a concrete array (e.g., using `collect()`)

![image-20251012081440009](coding/image-20251012081440009.png)

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

