---
author: "Yang Lyu"
date: 2024-07-09
title: Leetcode 15 Three Sum, Leetcode 16 3Sum Closest, Leetcode 18 four sum
weight: 10
tags:
  - hashmap
---
## Leetcode 15 three sum
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

![here](content/docs/Leetcode/Data Structure/hashmap/15.png) to help understand it better. The key challenge here is to remove duplicates in results
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
## 16. 3Sum Closest

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

- Answer:
    - very similar to above thinking patterns, but much easier
Diagram is ![here](/18.png)
```go
func threeSumClosest(nums []int, target int) int {
    // Sort the array
    sort.Ints(nums)
    // Initialize the closest sum with a large value
    closestSum := math.MaxInt32

    // Iterate through the array
    for i := 0; i < len(nums)-2; i++ {
        // Use two pointers to find the best pair
        left, right := i+1, len(nums)-1
        for left < right {
            sum := nums[i] + nums[left] + nums[right]
            // If the sum is exactly the target, return it
            if sum == target {
                return sum
            }
            // Update the closest sum if the current sum is closer to the target
            if abs(sum-target) < abs(closestSum-target) {
                closestSum = sum
            }
            // Move the pointers based on the comparison with the target
            if sum < target {
                left++
            } else {
                right--
            }
        }
    }
    return closestSum
}

// Helper function to calculate the absolute value
func abs(x int) int {
    if x < 0 {
        return -x
    }
    return x
}
```

## Leetcode 18 Four sum
Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order.

diagram here for easier understanding

- Answer:
    - very similar to above thinking patterns, and just adding another loop
```go
func fourSum(nums []int, target int) [][]int {
    sort.Ints(nums)
    n := len(nums)
    ans := [][]int{}
    if n<4{return nil}
    for k:=0;k<n-3;k++{
        if k>0&&nums[k]==nums[k-1]{continue}
        for i:=k+1;i<n-2;i++{
            if i>k+1&&nums[i]==nums[i-1]{continue}
            left,right:=i+1,n-1
            for left < right{
                sum := nums[k]+nums[i]+nums[left]+nums[right]
                if sum==target{
                    ans=append(ans,[]int{nums[k],nums[i],nums[left],nums[right]})
                    for left<right && nums[left]==nums[left+1]{
                        left++
                    }
                    for left<right && nums[right]==nums[right-1]{
                        right--
                    }
                    left++
                    right--
                }else if sum>target{
                    right--
                }else{
                    left++
                }
            }
        }
    }   
    return ans 
}
```
