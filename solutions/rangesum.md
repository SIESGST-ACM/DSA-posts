# Range Sum Query (Immutable)

**Problem Link:** https://leetcode.com/problems/range-sum-query-immutable/

## Why this problem?

This problem is a textbook example of the **Prefix Sum pattern**.

The signals are clear:

- We are asked to handle **multiple range sum queries**
- The array is **immutable**
- Recalculating sums for every query would be too slow

This directly points to using **Prefix Sum**.

---

## The Intuition

We are given an array and need to answer multiple queries of the form:

sum(left → right)


If we compute this using a loop for every query, the total time becomes inefficient.

Key idea:

Instead of recalculating sums again and again,  
we **precompute cumulative sums once** and reuse them.

---

## The Algorithm

### Step 1: Build the prefix array

Create a prefix array such that:

prefix[i] = sum of elements from index 0 to i - 1


This means:
- `prefix[0] = 0`
- `prefix[1] = nums[0]`
- `prefix[2] = nums[0] + nums[1]`
- and so on...

---

### Step 2: Answer range queries

To get the sum from index `left` to `right`:

sum = prefix[right + 1] - prefix[left]


This gives the result in **O(1)** time.

---

## Example

Input:
nums = [-2,0,3,-5,2,-1]
sumRange(0, 2)


Output:
1


Explanation:
prefix[3] - prefix[0] = (−2 + 0 + 3) − 0 = 1


---

## Why this works

- Prefix Sum avoids repeated calculations
- Precomputation is done once
- Each query becomes a simple subtraction
- Perfect for immutable arrays with multiple queries

---

## Complexity

- **Preprocessing Time:** `O(n)`
- **Query Time:** `O(1)`
- **Space Complexity:** `O(n)`

---

## Visualization

![Range sum query Visualization](../images/rangesum.png)

---

## Java Solution

```java
class NumArray {
    int[] prefix;

    public NumArray(int[] nums) {
        prefix = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }
    }

    public int sumRange(int left, int right) {
        return prefix[right + 1] - prefix[left];
    }
}

## Key Takeaway
If a problem involves:

Multiple range sum queries

An immutable array