# Minimum Size Subarray Sum — Sliding Window Approach

**Problem Link:**  
https://leetcode.com/problems/minimum-size-subarray-sum/

---

## Problem Statement

We are given a **target** value and an array of **positive integers**.

We need to find the **smallest contiguous subarray** whose sum is **at least the target**.

If no such subarray exists, return `0`.

---

## Key Observations

- We are dealing with **contiguous subarrays**
- The window size is **not fixed**
- All numbers are **positive**

This makes it a perfect fit for a **Dynamic Sliding Window** technique.

---

## Core Idea (Sliding Window)

We maintain two pointers:

- `i` → left pointer  
- `j` → right pointer  

And a running sum.

### Step-by-step logic:

1. Expand the window by moving `j` forward and add `nums[j]` to the sum.
2. When the sum becomes **≥ target**, try shrinking the window from the left (`i`)
3. While shrinking:
   - Update the minimum length
   - Subtract `nums[i]` from sum
   - Move `i` forward
4. Continue until `j` reaches the end.

---

## Why This Works

- All numbers are **positive**
- Expanding the window **increases** the sum
- Shrinking the window **decreases** the sum

So once the sum reaches the target, we can safely try to minimize the window.

Each element is:
- Added once
- Removed once

So the time complexity is **O(n)**.

---

## Time & Space Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## Summary

This is a classic **Dynamic Sliding Window** problem where:

- Window size changes dynamically
- We optimize for minimum length
- Positivity of numbers guarantees correctness

Efficient, clean, and optimal.

---
![Min Size Subarray Visualization](../images/minsizesub.png)

```java
class Solution {
    public int maxSubarraySum(int[] arr, int k) {
        int result = 0;
        int h = k - 1;
        int l = 0;

        for (int i = 0; i <= h; i++) {
            result = result + arr[i];
        }

        int Sum = result;

        while (h < arr.length - 1) {
            Sum = Sum + arr[h + 1] - arr[l];
            result = Math.max(result, Sum);
            l++;
            h++;
        }

        return result;
    }
}
