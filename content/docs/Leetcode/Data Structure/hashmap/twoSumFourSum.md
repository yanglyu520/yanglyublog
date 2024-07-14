---
author: "Yang Lyu"
date: 2024-07-09
title: Leetcode 1 Two sum, Leetcode 454 four sum
weight: 10
tags:
  - hashmap
---
## Leetcode 1 two sum 

```go
func twoSum(nums []int, target int) []int {
    m := map[int]int{}
    for i, v := range nums{
        another := target - v
        if index, found := m[another]; found{
            return []int{i,index}
        }
        m[v]=i
    }
    return nil
}
```
## Leetcode 454. 4Sum II
## Problem Description
Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4` all of length `n`, return the number of tuples `(i, j, k, l)` such that:
- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

## Approach
To solve this problem efficiently, we can use a hashmap (hashmap) to store the sums of pairs of elements from `nums1` and `nums2`, and then check if the negative of the sums of pairs from `nums3` and `nums4` exists in the hashmap.

## Time Complexity
1. **Building the Hashmap**:
    - We iterate over all pairs of elements from `nums1` and `nums2` to calculate their sums and store these sums in a hashmap.
    - There are `n * n` pairs, and each insertion in the hashmap takes `O(1)` time on average.
    - Thus, the time complexity for this step is \( O(n^2) \).

2. **Checking Pairs from `nums3` and `nums4`**:
    - We iterate over all pairs of elements from `nums3` and `nums4` to calculate their sums and check if the negative of these sums exists in the hashmap.
    - There are `n * n` pairs, and each lookup in the hashmap takes `O(1)` time on average.
    - Thus, the time complexity for this step is \( O(n^2) \).

Combining both steps, the overall time complexity is:
\[ O(n^2) + O(n^2) = O(n^2) \]

## Space Complexity
1. **Hashmap Storage**:
    - The hashmap stores sums of all pairs of elements from `nums1` and `nums2`.
    - There are `n * n` pairs, and each pair's sum is stored in the hashmap.
    - Thus, the space complexity for the hashmap is \( O(n^2) \).

2. **Auxiliary Space**:
    - Apart from the hashmap, we use a constant amount of extra space for variables and the output count.

Combining these, the overall space complexity is: \[ O(n^2) \]

## Summary
- **Time Complexity**: \( O(n^2) \)
- **Space Complexity**: \( O(n^2) \)

## Code Example

```go
func fourSumCount(nums1 []int, nums2 []int, nums3 []int, nums4 []int) int {
    map1 := make(map[int]int) // index is sum of nums1+nums2; vaule is times
    for _,v1 :=range nums1{
        for _, v2 := range nums2{
            map1[v1+v2]++
        }
    }
   
    sum := 0
    for _,v3 :=range nums3{
        for _, v4:= range nums4{
            if count, exists := map1[-v3-v4];exists{
                sum+=count
            }
        }
    }

    return sum
}
```
