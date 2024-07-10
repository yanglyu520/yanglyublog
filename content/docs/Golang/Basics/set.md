---
author: "Yang Lyu"
date: 2024-05-28
title: How to implement set using Greedy in golang?
weight: 10
tags:
  - golang
  - set
  - Greedy
---
# How to Implement Set Using HashMap in Golang

## 1. What is a Set? How is Set Different from HashMap?

A **set** is a data structure that stores a collection of unique elements. 
Sets do not allow duplicate values and do not maintain any particular order of the elements.

A **hashmap** is a data structure that stores key-value pairs. Each key in a hashmap is unique, and it maps to a specific value.

### Differences between Set and HashMap:
- **Structure**: A set can be thought of as a hashmap with only keys and no associated values.
- **Use Case**: Use a set when you need to ensure uniqueness of elements. 
- Use a hashmap when you need to associate values with keys for quick lookup.

## 2. How to Implement Set Using HashMap in Golang?

In Golang, we can implement a set using a hashmap where the keys of the hashmap represent the elements of the set. The values of the hashmap can be of an empty struct type (`struct{}`) because it consumes no memory.

### Example Code:

```go
func main() {
    set := make(map[int]struct{})
    
    set[1] = struct{}{}
    set[2] = struct{}{}
    set[3] = struct{}{}
    
    if _, exists := set[1]; exists {
    fmt.Println("1 exists in set")
    }
    
    fmt.Println(set)
    delete(set, 3)
    fmt.Println(set)
}
```

## 3. Why Not Use `map[int]bool` to Implement Set in Golang?

Using `map[int]bool` is a straightforward way to implement a set, but using `map[int]struct{}` has some advantages:

1. **Memory Efficiency**: The `struct{}` type in Go occupies zero bytes of storage, while the `bool` type requires at least one byte. When dealing with a large number of elements, `map[int]struct{}` can save significant memory.
   
2. **Semantics**: Using `struct{}` as the value type clearly indicates that the map is being used as a set where only the presence of keys matters. This can prevent misuse where the boolean value might be misinterpreted or used incorrectly.

## 4. When Will I Need to Use Set?

Sets are useful in scenarios where you need to maintain a collection of unique elements and frequently check for the presence of elements. Some common use cases include:
- Removing duplicates from a list.
- Checking for membership.
- Performing set operations like union, intersection, and difference.

### 5. Solution Example for LeetCode 349: Intersection of Two Arrays

Here's an example of how to use sets to solve LeetCode problem 349, which requires finding the intersection of two arrays:

```go
func intersection(nums1 []int, nums2 []int) (intersection []int) {
    set1 := map[int]struct{}{}
    for _, v := range nums1 {
        set1[v] = struct{}{}
    }
    set2 := map[int]struct{}{}
    for _, v := range nums2 {
        set2[v] = struct{}{}
    }
	
    if len(set1) > len(set2) {
        set1, set2 = set2, set1
    }
    for v := range set1 {
        if _, has := set2[v]; has {
            intersection = append(intersection, v)
        }
    }
    return
}
```

### Explanation:
1. **Create Sets**: Create two sets, `set1` and `set2`, to store the unique elements from `nums1` and `nums2` respectively.
2. **Fill Sets**: Populate the sets with elements from the arrays.
3. **Optimize Search**: Swap sets if `set1` is larger than `set2` to minimize the number of lookups.
4. **Find Intersection**: Iterate through the smaller set and check if each element is present in the larger set. If it is, add it to the intersection result.

### 6. Template for finding intersections between 2 sets

```go
if len(set1) > len(set2) {
        set1, set2 = set2, set1
    }
for v := range set1 {
    if _, has := set2[v]; has {
        intersection = append(intersection, v)
    }
}
```

This approach ensures that the intersection contains only unique elements that are present in both arrays, leveraging the efficiency of sets implemented using hashmaps.
