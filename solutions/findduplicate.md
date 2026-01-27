# Find the Duplicate Number

**Problem Link:** https://leetcode.com/problems/find-the-duplicate-number/

## Why this problem?

This problem is a classic application of the **Slow & Fast Pointer pattern** (Floyd’s Cycle Detection).

The signals are clear:

- No extra space is allowed
- The array must **not be modified**
- Values behave like **pointers to indices**
- Exactly **one duplicate exists**

All of this indicates **cycle detection**.

---

## The Intuition

We are given an array of size `n + 1`  
with values in the range `1` to `n`.

Since there are more elements than possible values,
**at least one number must repeat**.

Key idea:

If we treat:
- **Index → node**
- **nums[i] → next pointer**

Then the array behaves like a **linked list**.

A duplicate value means **two indices point to the same next node**,  
which creates a **cycle**.

The duplicate number is the **entry point of that cycle**.

---

## The Algorithm

We use **Floyd’s Cycle Detection Algorithm**.

### Phase 1: Detect the cycle

- Use two pointers:
  - `slow` → moves one step
  - `fast` → moves two steps
- They will meet **inside the cycle**

---

### Phase 2: Find the cycle entry (duplicate)

- Reset `slow` to the start
- Move both pointers **one step at a time**
- The point where they meet again is the **duplicate number**

---

## Why this works

- A faster pointer will always catch a slower one inside a cycle
- Resetting one pointer aligns both to meet at the **cycle start**
- The cycle start corresponds to the **duplicate value**

---

## Example

Input:
[1,3,4,2,2]


Output:
2


Explanation:
Duplicate value creates a cycle → entry point is 2


---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## Visualization

![Find Duplicate Visualization](../images/fndduplicate.png)

---

## Java Solution

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];

        // Phase 1: Detect cycle
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        // Phase 2: Find cycle entry
        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }

        return slow;
    }
}

