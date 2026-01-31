# Subarray Sums Divisible by K

**Problem Link:** https://leetcode.com/problems/subarray-sums-divisible-by-k/

## Why this problem?

This problem is a classic application of **Prefix Sum + Hashing (Remainder Frequency)**.

The signals are clear:

- We are working with **subarrays** (contiguous)
- Numbers can be **negative**
- We need to count how many subarrays satisfy a condition
- Sliding Window does **not work**

This directly points to **Prefix Sum + Remainder Hashing**.

---

## The Intuition

We are given an array and an integer `k`.

Our task is to count how many subarrays have a **sum divisible by `k`**.

Key observation:

If two prefix sums have the **same remainder** when divided by `k`,
their difference is divisible by `k`.

Mathematically:

prefixSum[i] % k == prefixSum[j] % k


Then the subarray `(i + 1) → j` has a sum divisible by `k`.

---

## The Algorithm

We maintain:

- A running `prefixSum`
- A frequency array to count remainders:
remainder → frequency


### Steps:

1. Initialize remainder frequency:
freq[0] = 1

This handles subarrays starting at index `0`.

2. Traverse the array:
- Update `prefixSum`
- Compute remainder:
  ```
  rem = ((prefixSum % k) + k) % k
  ```
  (This fixes negative remainders)
- Add `freq[rem]` to the answer
- Increment `freq[rem]`

---

## Example

Input:
nums = [4,5,0,-2,-3,1]
k = 5


Output:
7


Explanation:
Subarrays with sum divisible by 5 are counted using matching remainders


---

## Why this works

- Converts the problem into counting **pairs of prefix sums**
- Uses mathematical properties of divisibility
- Avoids nested loops
- Each element is processed once

---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(k)`

---

## Visualization

![Subarray Divisible by K Visualization](../images/divbyk.png)

---

## Java Solution

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        int count = 0;
        int prefixSum = 0;

        int[] freq = new int[k];
        freq[0] = 1;

        for (int num : nums) {
            prefixSum += num;
            int rem = ((prefixSum % k) + k) % k;

            count += freq[rem];
            freq[rem]++;
        }

        return count;
    }
}