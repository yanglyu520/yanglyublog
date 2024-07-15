---
author: "Yang Lyu"
date: 2024-07-15
title: Basic Golang Interview Questions Part 1
weight: 10
tags:
   - Golang
   - Interview
---
# Basic Golang Interview Questions Part 1

1. What are the pros and cons of using Golang?
* Pros:
   - Efficient Concurrency: 
      - Goroutines and channels make it easy to write concurrent programs, leveraging multi-core processors efficiently.
      - Goroutines: Lightweight threads managed by the Go runtime, making concurrent programming easier and more efficient.
      - Channels: Facilitate safe communication between goroutines, promoting clean concurrency patterns.
   - GC:
      - Automatic memory management reduces the risk of memory leaks and manual memory management errors.
   - Cross-Platform:
      - Go programs can be compiled to run on various operating systems without modification.
   - Strong Typing:
      - Type Safety: Statically typed language with strong type checking, preventing many common programming errors.
   - Strong Standard Library:
      - Rich Libraries: Comprehensive standard library supports tasks like web development, file handling, and cryptography.
      - Built-in Testing: Includes a robust testing framework, making unit testing straightforward.
* cons:
   - GC: Garbage collection, while efficient, can introduce latency, making Go less suitable for real-time systems.
   - Error Handling: Go’s explicit error handling can lead to verbose and repetitive code, compared to exceptions in other languages.
   - Large Binaries: Go binaries can be relatively large due to static linking, which includes all dependencies.
   - Focus on Backend: Go is primarily used for backend services and systems programming, with limited support for frontend or desktop UI development.

2. Difference between slice and array in Golang?
{{</* expand "Custom Label" "..." */>}}
- Array:
    * fixed size at compile time, and cannot be resized
    * memory is allocated at the time of declaration
    * stored continously in memory
- Slice:
    * support dynamic resizing
    * consist of a pointer to the array, length, and capacity
    * Slices are reference types, meaning that multiple slices can refer to the same underlying array.
    * Memory is allocated on demand and can be reallocated when the slice grows.
{{</* /expand */>}}

3. Why static types are good?

{{</* expand "Custom Label" "..." */>}}
Early Error Detection:

* Errors and type mismatches are caught at compile-time rather than at runtime, reducing the chances of bugs in production and improving code reliability.
Enhanced Code Readability and Maintainability:

* Explicit type declarations make the code easier to read and understand, allowing developers to quickly grasp the types of variables and function returns, which simplifies maintenance and collaboration.
Optimized Performance:

* Compilers can optimize code more effectively when types are known at compile-time, leading to potential performance improvements due to better resource management and allocation.
{{</* /expand */>}}

4. What are 2 types of string literals in Golang and what are the differences?
{{</* expand "Custom Label" "..." */>}}
In Go, there are two types of string literals: interpreted string literals and raw string literals.
* Interpreted String Literals:
Enclosed in double quotes `""`.
Special characters like \n (newline) and \t (tab) are interpreted.
Example: "Hello\nWorld" results in a string with a newline between "Hello" and "World".
* Raw String Literals:
Enclosed in backticks \`.
- Special characters are not interpreted, and the string can span multiple lines.
- Example: a :=\`Hello\nWorld\` results in a string with the literal text "Hello\nWorld", including the backslash and 'n' as part of the string.
  {{</* /expand */>}}
7. What is the time complexity of merge sort?
   {{</* expand "Custom Label" "..." */>}}
Time Complexity:
- Best Case: O(nlogn)
- Average Case: O(nlogn)
- Worst Case: O(nlogn)
The time complexity is consistently O(nlogn) because the array is always divided into two halves, and the merging process takes linear time.
Space Complexity:
Auxiliary Space:
O(n)
Mergesort requires additional space proportional to the size of the input array to store the subarrays during the merging process.
```go
// Mergesort function sorts the input array using the mergesort algorithm.
func Mergesort(arr []int) []int {
    // Base case: if the array has 1 or 0 elements, it is already sorted.
    if len(arr) <= 1 {
        return arr
    }

    // Find the middle index to divide the array into two halves.
    mid := len(arr) / 2

    // Recursively sort both halves.
    left := Mergesort(arr[:mid])
    right := Mergesort(arr[mid:])

    // Merge the sorted halves.
    return merge(left, right)
}

// Merge function merges two sorted arrays into a single sorted array.
func merge(left, right []int) []int {
    // Create a new array to hold the merged result.
    result := make([]int, 0, len(left)+len(right))

    // Initialize indices for left and right arrays.
    i, j := 0, 0

    // Iterate through both arrays and merge them into the result array.
    for i < len(left) && j < len(right) {
        if left[i] < right[j] {
            result = append(result, left[i])
            i++
        } else {
            result = append(result, right[j])
            j++
        }
    }

    // Append any remaining elements from the left array.
    result = append(result, left[i:]...)

    // Append any remaining elements from the right array.
    result = append(result, right[j:]...)

    return result
}
```
{{</* /expand */>}}

7. What basic and composite types do we have in Golang?

{{</* expand "Custom Label" "..." */>}}
* Basic Types:
    - Boolean: bool
    - Numeric: int, uint, float32, float64, complex64, complex128, etc.
    - Character: rune
    - String: string
* Composite Types:
    - Array
    - Slice
    - Struct
    - Pointer
    - Function Value
    - Map
    - Channel
    - Interface
{{</* /expand */>}}

9. What design principles can you use if you were to design an app like `What's app`?

- Microservices Architecture:
Decompose the application into independent, loosely coupled services.
Facilitate easier maintenance, scaling, and deployment.

- Data Consistency and Synchronization:
Implement mechanisms for synchronizing messages across multiple devices.
Use eventual consistency models for real-time communication.

- Security:
Encrypt messages end-to-end to protect user privacy.
Secure user authentication and data storage.
