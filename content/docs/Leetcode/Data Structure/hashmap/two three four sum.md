---
author: "Yang Lyu"
date: 2024-07-09
title: Leetcode 454 four sum && Leetcode 15 three sum && 
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

Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:
0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0

### Solution

The idea is not different from two sums. We just separate it into two groups, first group is all possibilities of nums1[i] + nums2[j], then the second group is all possibilities of nums3[k] + nums4[l]

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