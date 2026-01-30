# Subarray Sum Equals K

**Problem Link:** https://leetcode.com/problems/subarray-sum-equals-k/

## Why this problem?

This problem is a classic application of **Prefix Sum + HashMap**.

The signals are clear:

- We are dealing with **subarrays** (contiguous)
- Numbers can be **positive or negative**
- We need to count how many subarrays equal a given sum
- Sliding Window does **not work** due to negative numbers

This directly points to **Prefix Sum with HashMap**.

---

## The Intuition

We are given an array and a number `k`.

Our task is to count how many subarrays have a sum equal to `k`.

Key observation:

If:

prefixSum[j] - prefixSum[i] = k


then the subarray from `(i + 1)` to `j` has sum `k`.

So instead of checking all subarrays,
we track **prefix sums** and how often they appear.

---

## The Algorithm

We maintain:

- A running `prefixSum`
- A HashMap storing:
prefixSum → frequency


### Steps:

1. Initialize the map with:
{0 : 1}

This handles subarrays starting from index `0`.

2. Traverse the array:
- Add current number to `prefixSum`
- Check if `(prefixSum - k)` exists in the map
  - If yes, add its frequency to the answer
- Store/update `prefixSum` in the map

---

## Example

Input:
nums = [1,1,1]
k = 2


Output:
2


Explanation:
[1,1] at indices (0,1)
[1,1] at indices (1,2)


---

## Why this works

- Converts the problem into counting **pairs of prefix sums**
- Handles negative numbers correctly
- Avoids nested loops
- Each element is processed once

---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)`

---

## Visualization

![Subarray of Sum K Visualization](../images/subarray.png)

---

## Java Solution

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        int sum = 0, count = 0;

        for (int num : nums) {
            sum += num;
            count += map.getOrDefault(sum - k, 0);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
Key Takeaway
If a problem asks for:

Number of subarrays with a given sum

And negative numbers are involved