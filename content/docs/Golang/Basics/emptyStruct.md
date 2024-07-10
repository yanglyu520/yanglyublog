---
author: "Yang Lyu"
date: 2024-07-09
title: Empty Struct
weight: 10
tags:
   - golang
   - struct
---
# Go Empty Struct

## Introduction

An empty struct has zero memory allocation, same memory addresses for multiple instances, and stateless.

## Zero Memory Allocation

Empty structs do not occupy memory, making them useful for memory optimization:

```go
package main
import (
    "fmt"
    "unsafe"
)
func main() {
    var e struct{}
    fmt.Println(unsafe.Sizeof(e)) // Output: 0
}
```

## Same Memory Addresses

Multiple empty structs share the same address:

```go
package main
import "fmt"
func main() {
    var e, e2 struct{}
    fmt.Printf("%p", &e)  // Output: 0x90b418
    fmt.Printf("%p", &e2) // Output: 0x90b418
}
```

## Usage Scenarios

1. **Set Implementation:**

```go
set := make(map[int]struct{})
set[1] = struct{}{}
```

2. **Channel Signals:**

```go
quit := make(chan struct{})
go func() {
    time.Sleep(3 * time.Second)
    close(quit)
}()
<-quit
```

3. **Method Receivers:**

```go
type R struct{}
func (r *R) SayHello() { fmt.Println("Hello") }
```

