---
author: "Yang Lyu"
date: 2024-05-28
title: fmt package
weight: 10
tags:
  - golang
  - fmt
---

## formatting verbs
1. `%s` vs `%q`?
- Answer:
    - `%s` prints the string without enclosing it in quotes.
    - `%q` prints the **string enclosed in double quotes**, %q can print string, byte slice, runes and int.
2. `%v` vs `%+v` vs `%#v`?
- Answer:
    - `%v`: Default format, prints the value as is. For structs, it prints only the field values.
    - `%+v`: Detailed format, includes field names in structs.
    - `%#v`: Go-syntax representation, includes type information and can be used to recreate the value in Go code.
3. What to use to print slice, maps and structs(composite data types)?
- Answer:
    - %v, %+v, and %#v is mostly used
    - %p prints the pointer of the complex data types

## scan function for user input

- Scan, Scanf and Scanln read from **os.Stdin**
- Fscan, Fscanf and Fscanln read from a specified **io.Reader**
- Sscan, Sscanf and Sscanln read from **an argument string**
- **Most importantly, remember to pass pointer instead of the variable as it needs to be written to the same variable space, not the value itself.**
- **Also, remember to handle errors with fmt.Scan functions**
- **If we want to do an endless input, we can use the for loop and break the loop if there is any error with the fmt.Scan**

1. Difference between fmt.Scan, fmt.Scanf and fmt.Scanln?
   Answer:
    - fmt.Scan:
      Reads space-separated values from standard input.
      Stops reading at the first whitespace.
```go
var a int
var b string
fmt.Scan(&a, &b)
fmt.Printf("a: %d, b: %s\n", a, b)
```
- fmt.Scanf:
  Reads input according to a format specifier.
  Allows more control over the input format.
```go
var a int
var b string
fmt.Scanf("%d %s", &a, &b)
fmt.Printf("a: %d, b: %s\n", a, b)
```
- fmt.Scanln
  Reads input until a newline is encountered.
  Useful for reading a whole line of text or multiple values until the newline.
```go
var b string
fmt.Scanln(&b)
```
     
