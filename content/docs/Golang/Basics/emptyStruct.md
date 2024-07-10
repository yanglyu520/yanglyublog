---
author: "Yang Lyu"
date: 2024-07-09
title: Go Empty Struct
weight: 10
tags:
   - golang
   - struct
---
# Go Empty Struct

## Introduction

In Go, an empty struct `struct{}` can be puzzling. This article explores the empty struct's properties and uses. An empty struct has zero memory allocation, identical addresses for multiple instances, and statelessness.

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

## Identical Addresses

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
type Set[K comparable] map[K]struct{}
func (s Set[K]) Add(val K) { s[val] = struct{}{} }
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
type Person interface { SayHello() }
type CMY struct{}
func (c CMY) SayHello() { fmt.Println("Hello, I'm Chen Mingyong.") }
```

