## Question 1: Max Sum Subarray of Size K

**Problem Link:**  
https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/

---

We are given an array and a number `k`.

We need to find the **maximum sum of any subarray of length `k`**.

Since the subarray must be **contiguous** and the size is **fixed**,  
this is a perfect **Sliding Window** problem.

---

## Brute Force Approach

The brute force solution tries all possible subarrays of length `k`.

- For each subarray, compute the sum
- Total time complexity: **O(n × k)**

This is inefficient for large inputs.

---

## Optimized Sliding Window Approach (O(n))

### How the approach works:

1. First, calculate the sum of the **first `k` elements**  
   → this forms the **first window**

2. Then, slide the window one step at a time:
   - **Remove** the element going out of the window (left side)
   - **Add** the new element coming into the window (right side)

3. Update the sum in **O(1)** time for each shift

4. Keep track of the **maximum sum** seen so far

---

## Why this works

- Each element is **added once**
- Each element is **removed once**

So:
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)` (no extra space used)

This makes Sliding Window the optimal solution here.

![Max Sum of Size K](../images/maxsumk.png)