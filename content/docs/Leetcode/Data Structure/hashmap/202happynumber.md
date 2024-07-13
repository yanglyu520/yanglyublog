---
author: "Yang Lyu"
date: 2024-07-09
title: Leetcode 202 happy number
weight: 10
tags:
  - hashmap
---
# Leetcode 202 Happy Number

A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not.

## Solutions:
There are 2 final situations with these square sum
1. It will end in 1
2. It will enter into a loop

- We need to learn how to get each digit of a number, the way to do such is to n%10 to get the last digit of the number and n/10 to delete the last digit of such number

### Question: why does it not become bigger and bigger endlessly?
Answer:
We can get into an example of biggest two digits number 99, and the nextStep, it becomes 2*81=162, we can see it shrinks
Then we can try examples of 999, 9999, 99999, and they all start shrinking

### Solution in Golang
```go
func isHappy(n int) bool {
   set := make(map[int]struct{})

   for {
      n = nextStep(n)
      if n == 1 {
        return true
      }
      if _, ok := set[n]; ok {
        return false
      }
      set[n]=struct{}{}
   }

   return n==1
}

func  nextStep (n int) int {
    sum := 0
    for n>0{
        sum+=(n%10)*(n%10) // get the last digit of n and square and add to sum
        n=n/10 // delete last digit of n and n will shrink eventually to 0
    }
    return sum
}
```

### Question: what is the time complexity of this solution?
- time complexity: O(log(n))
- space complexity: O(log(n))
- This is because the number of digits in n is log10(n)
- Once a number is below 243, its sum of squares will not return above 243(3*81). Therefore, we can use the longest cycle length below 243 to effectively detect happy numbers. 

### Question: Do you have an alternative way to solve this problem since you mentioned about it getting into a loop?

```go
func isHappy(n int) bool {
   slow, fast := n, n
   for {
      slow = nextStep(slow)
      fast = nextStep(nextStep(fast))
      if fast == 1{return true}
      if slow == fast {return false}
   }
}

func  nextStep (n int) int {
    ... same as above
}
```