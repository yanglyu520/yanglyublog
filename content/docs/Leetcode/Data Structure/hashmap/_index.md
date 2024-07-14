# Hashmap

## 1.Understanding Hash Tables Basic Concepts

In general, hash tables are used to quickly determine if an element is present in a collection.

For hash tables, it is important to understand the role of hash functions and hash collisions.

A hash function maps the given key to an index in the symbol table.

Hash collision handling deals with scenarios where multiple keys map to the same index. 
Common ways to handle collisions include chaining and linear probing.

## Common Hash Structures

The three common hash structures are:

- Arrays
- Sets
- Maps

### Maps as Hash Tables

In the context of the "Two Sum" problem, maps make their formal appearance.

Let's discuss the limitations of using arrays and sets for hash-based methods.

- **Arrays**: The size of an array is limited. If the elements are sparse and the hash values are too large, it results in wasted memory space.
- **Sets**: A set contains only unique keys. In the "Two Sum" problem, not only do we need to check if `y` exists, but we also need to record the index of `y` to return the indices of `x` and `y`. Therefore, sets are not suitable.

A map, which has a `<key, value>` structure, is most suitable for this problem because we can use the key to store the value and the value to store the index.

C++ provides the following three types of maps (for details, see [About Hash Tables, What You Should Know](opens new window)):

- `std::map`
- `std::multimap`
- `std::unordered_map`

`std::unordered_map` is implemented as a hash table, while `std::map` and `std::multimap` are implemented as red-black trees.

Similarly, the keys in `std::map` and `std::multimap` are ordered. In the "Two Sum" problem, we don't need the keys to be ordered, so `std::unordered_map` is more efficient.

In the "4Sum II" problem, we mentioned that maps are seen wherever hashing is needed.

At first glance, this problem seems similar to "4Sum" and "3Sum", but there are significant differences!

The key difference is that this problem involves four independent arrays. We just need to find `A[i] + B[j] + C[k] + D[l] = 0` without worrying about duplicates. In contrast, "4Sum" and "3Sum" involve finding combinations that sum to zero within a single array, which is much more challenging!

Using hashing solves the "Two Sum" problem, and many students might think that hashing can also solve "3Sum" and "4Sum".

While it can solve them, it is very cumbersome and results in low efficiency due to the need to remove duplicates.

In "3Sum", I provided both hashing and two-pointer solutions, demonstrating that using hashing is more cumbersome.

Therefore, for "4Sum" and "3Sum", the two-pointer method is recommended!

## Summary

Many students are familiar with hash tables, but their knowledge may not be systematic.

In this article, we present a complete picture of hash tables, from their theoretical foundations to classic applications of arrays, sets, and maps.

We also emphasize that while maps are versatile, it is important to know when to use arrays and sets.

Through this summary, we hope you gain a comprehensive understanding of hash tables.


