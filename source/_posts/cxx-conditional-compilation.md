---
title: C++ conditional compilation
date: 2022-02-07 23:52:42
tags:
categories:
- coding
---

#### Using g++ only

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

#### Using **CMakeLists.txt** *add_definitions*

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

