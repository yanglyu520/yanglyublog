---
author: "Yang Lyu"
date: 2024-07-09
title: `new` vs `make`
weight: 10
tags:
  - golang
  - new
  - make
  - pointer
---
# Difference between `new` and `make` in Golang

In Go, `make` and `new` are built-in functions used for memory allocation. 
- `make` not only allocates memory but also initializes the data, which is necessary because the data types supported by make (like slices, maps, and channels) require initialization before use. 
- On the other hand, `new` allocates memory space that is filled with zero values. 
- `new` allocates a single block of memory, while `make` may allocate multiple blocks of memory.

## `new`
- **Usage:** For basic types like integers, structs, and arrays.
- **Returns:** A pointer to the allocated type.

**Example:**
```go
package main

import "fmt"

func main() {
    p := new(int)
    fmt.Println(*p) // 0
    *p = 42
    fmt.Println(*p) // 42

    type Person struct {
        Name string
        Age  int
    }

    person := new(Person)
    fmt.Println(*person) // { 0}
    person.Name = "John"
    person.Age = 30
    fmt.Println(*person) // {John 30}
}
```

## `make`
- **Usage:** For slices, maps, and channels.
- **Returns:** The initialized type itself.

**Example:**
```go
package main

import "fmt"

func main() {
    slice := make([]int, 5)
    fmt.Println(slice) // [0 0 0 0 0]
    for i := range slice {
        slice[i] = i + 1
    }
    fmt.Println(slice) // [1 2 3 4 5]

    m := make(map[string]int)
    fmt.Println(m) // map[]
    m["one"] = 1
    m["two"] = 2
    fmt.Println(m) // map[one:1 two:2]

    ch := make(chan int, 2)
    fmt.Println(len(ch)) // 0
    ch <- 1
    ch <- 2
    fmt.Println(len(ch)) // 2
}
```

## Key Differences
1. **Types:** `new` for any type, `make` for slices, maps, and channels.
2. **Return Value:** `new` returns a pointer, `make` returns an initialized value.
3. **Initialization:** `new` allocates zeroed storage, `make` allocates and initializes.
