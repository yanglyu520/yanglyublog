---
author: "Yang Lyu"
date: 2024-07-09
title: Leetcode 454 four sum && Leetcode 15 three sum && 18 four sum to new target
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

### Leetcode 15 three sum
[Diagram](/15.png) to help understand it better. The key challenge here is to remove duplicates in results
1. Why not use hashmap solution as two sums?
   - Hashmap Approach: 
   - Using a hashmap requires careful handling of pairs and checking for duplicates.
   - The logic can become complex and harder to follow.
   
2. Time and space complexity for two pointers solution?
- **Time Complexity**: \( O(n^2) \)
    - Sorting the array takes \( O(n \log n) \).
    - The two-pointer technique runs in \( O(n^2) \).
    - The overall time complexity is dominated by \( O(n^2) \).

- **Space Complexity**: \( O(1) \)
    - The sorting step and the two-pointer technique use only a constant amount of extra space.
    - The output space is not considered in the space complexity calculation.

The sorting step and the two-pointer technique use only a constant amount of extra space.
The output space is not considered in the space complexity calculation.
```go
func threeSum(nums []int) [][]int {
  sort.Ints(nums)
  n := len(nums)
  res := [][]int{}

  for i:=0;i<n-2;i++{
    if nums[i]>0{break}
    if i>0 && nums[i]==nums[i-1]{continue}
    left,right:=i+1,n-1
    for left<right {
      sum := nums[i]+nums[left]+nums[right]
      if sum==0{
        res=append(res, []int{nums[i], nums[left],nums[right]})
        for left<right && nums[left]==nums[left+1]{
                left++
            }
        for left<right && nums[right]==nums[right-1]{
                right--
            }
        left++
        right--    
        }else if sum < 0 {
            left++
        }else {
            right--
        }
    }
  }
  return res
}
```
### Leetcode 18 four sum to new target