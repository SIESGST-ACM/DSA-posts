 Find Pivot Index

**Problem Link:** https://leetcode.com/problems/find-pivot-index/

## Why this problem?

This problem is a classic application of the **Prefix Sum pattern**.

The signals are clear:

- We need to compare **left and right ranges**
- Brute force would require **recomputing sums**
- We want an **O(n)** time solution
- Extra space should be minimal

This directly points to using **Prefix Sum thinking**.

---

## The Intuition

We are given an array and need to find an index such that:

Sum of elements on the left = Sum of elements on the right


A brute-force approach would recalculate left and right sums for every index, which is inefficient.

Key observation:

If we know the **total sum** of the array, then for any index:

Right Sum = Total Sum − Left Sum − Current Element


So we don’t need separate loops.

---

## The Algorithm

### Step 1: Compute total sum

- Traverse the array once to calculate `totalSum`

---

### Step 2: Traverse and compare

- Initialize `leftSum = 0`
- For each index:
  - Calculate `rightSum` using:
    ```
    rightSum = totalSum - leftSum - nums[i]
    ```
  - If `leftSum == rightSum`, this index is the pivot
  - Update `leftSum` by adding `nums[i]`

Return the **first index** that satisfies the condition.

---

## Example

Input:
[1,7,3,6,5,6]


Output:
3


Explanation:
Left sum = 1 + 7 + 3 = 11
Right sum = 5 + 6 = 11


---

## Why this works

- Prefix Sum allows reuse of previous computations
- Each element is processed only once
- Eliminates unnecessary nested loops

---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## Visualization

![Find Pivot Visualization](../images/findpivot.png)

---

## Java Solution

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int totalSum = 0;
        for (int n : nums) totalSum += n;

        int leftSum = 0;
        for (int i = 0; i < nums.length; i++) {
            int rightSum = totalSum - leftSum - nums[i];
            if (leftSum == rightSum) return i;
            leftSum += nums[i];
        }
        return -1;
    }
}
