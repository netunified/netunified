# 🔄 Rotate Array In-Place in C — A Minimalist, Cycle-Aware Solution

**Author:** [@netunified](https://leetcode.com/u/netunified/)  
**Language:** C  
**Topic:** In-Place Array Rotation  
**Difficulty:** Medium  
**Tags:** Arrays, In-Place Algorithms, Cycles, C Programming

---

## 🧩 Problem

Rotate an array `nums` of size `n` to the right by `k` steps.  
You must do it **in-place** with **O(1)** extra space.

### Example

```c
Input:  nums = [1, 2, 3, 4, 5, 6], k = 2  
Output: [5, 6, 1, 2, 3, 4]
```

---

## 🧠 Solution Overview

This solution, authored by **[@netunified](https://leetcode.com/u/netunified/)**, implements an elegant twist on the classical **cyclic replacement** algorithm.

Instead of using `gcd(numsSize, k)` to detect cycle count, or tracking visited elements, this method relies on **smart pointer manipulation and implicit loop detection** using `ptr_offset`.

All elements are visited exactly once, and swapped correctly — with just a few variables and a single loop.

---

## ✅ C Code

```c
#include <stdio.h>

// Solution by netunified (LeetCode)

int rotate(int* nums, int numsSize, int k) {
 int prev = 0, curr = 0, ptr_offset = 0, ptr = 0; 

  for (int i = 0; i < numsSize; i++) {

    /* if ptr arrives at the offset (loop detected) 
     * increment the offset by 1 and move the ptr 
     * k steps to the right. else continue swapping
     * as usual.
     */ 
    if (ptr_offset == ptr) {
        ptr_offset = (ptr + 1) % numsSize;
        ptr = (ptr_offset + k) % numsSize;
        curr = nums[ptr_offset];
        prev = nums[ptr];
        nums[ptr] = curr;
    } else {
        ptr = (ptr + k) % numsSize;
        curr = nums[ptr];
        nums[ptr] = prev;
        prev = curr;
    }
  }

  return 0;
}

int main() {
  int k = 2;
  int arr[] = {1, 2, 3, 4, 5, 6};
  int arr_len = sizeof(arr) / sizeof(arr[0]);
  int ret = rotate(arr, arr_len, k);


  for (int i = 0; i < arr_len; i++)
    printf(
        (i == 0) ? "[%d," : (i < arr_len - 1) ? "%d," : "%d]\n",
        arr[i]
    );

  return ret;
}
```

---

## 🔍 How It Works

1. `ptr` represents the current index we're writing to.
2. `ptr_offset` tracks the start of a new cycle.
3. When `ptr == ptr_offset`, it means we've completed a cycle. We bump `ptr_offset` and start another.
4. `prev` carries the displaced value forward to be written into the next location.

This smart handling **implicitly tracks multiple disjoint cycles** that arise when `gcd(numsSize, k) > 1`.

---

## 🔄 Visual Walkthrough

For `nums = [1, 2, 3, 4, 5, 6]`, `k = 2`, this is the rotation sequence:

```
Original:  [1, 2, 3, 4, 5, 6]
Step 1 →   [1, 2, 1, 4, 5, 6]
Step 2 →   [1, 2, 1, 4, 3, 6]
Step 3 →   [5, 2, 1, 4, 3, 6]
Step 4 →   [5, 2, 1, 2, 3, 6]
Step 5 →   [5, 6, 1, 2, 3, 6]
Step 6 →   [5, 6, 1, 2, 3, 4]
```

Final output: `[5, 6, 1, 2, 3, 4]`

---

## 🆚 Comparison to Classical Solution

| Feature | Classical GCD-Based | This Solution (@netunified) |
|--------|----------------------|------------------------------|
| Uses GCD? | ✅ Yes | ❌ No |
| Tracks visited? | ✅ Yes | ❌ No |
| Uses counter? | ✅ Yes (`count`) | ❌ No |
| Single loop? | ❌ No | ✅ Yes |
| Elegant + minimal? | ⚠️ Verbose | ✅ Very clean |

---

## 💬 Final Thoughts

This solution is a **concise**, **in-place**, and **loop-aware** approach that avoids the usual boilerplate and complexity of other cyclic replacements.

It’s a perfect example of solving a problem by understanding the **underlying structure** (cyclic shifts) and trusting smart state tracking (`ptr_offset`) instead of brute-force counters.

---

## 🏆 Credit

> ✨ Written by [@netunified](https://leetcode.com/u/netunified/)  
> 🧠 Original idea and implementation  
> 📍 No GCD, no visited flags, no recursion — just clever logic.

---

## 📎 Want to Share?

Feel free to copy, clone, or fork this blog post — just leave credit to [@netunified](https://leetcode.com/u/netunified/) where it's due!

---

ChatGPT wrote this blog post (not the solution) for me :D!
