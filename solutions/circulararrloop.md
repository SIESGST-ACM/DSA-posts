# Circular Array Loop

**Problem Link:** https://leetcode.com/problems/circular-array-loop/

## Why this problem?

This problem is a classic application of the **Fast & Slow Pointer pattern** (Floyd’s Cycle Detection).

The signals are clear:

- The problem involves **cycle detection**
- No extra space is allowed
- Array indices behave like **linked list pointers**
- We must determine if a **valid loop** exists

This makes Fast & Slow Pointer the ideal approach.

---

## The Intuition

We are given a **circular array** where each element tells us how far to jump:
- Positive value → move forward
- Negative value → move backward

Our task is to check whether there exists a **valid cycle**.

### A cycle is valid if:
- Cycle length is **greater than 1**
- All moves are in the **same direction** (all positive or all negative)
- We eventually come back to the **same index**

---

## Key Idea

Treat:
- **Index → node**
- **nums[i] → jump to next node**

With this interpretation, the array behaves like a **linked list with jumps**.

If a cycle exists:
- `slow` (1 step)
- `fast` (2 steps)

will eventually meet.

---

## The Algorithm

For each index in the array:

1. Skip if already visited
2. Initialize:
   - `slow = i`
   - `fast = i`
   - Fix the direction (positive or negative)
3. Move pointers:
   - `slow` moves one jump
   - `fast` moves two jumps
4. Stop if:
   - Direction changes
   - A single-length loop is detected
5. If `slow == fast` → **valid cycle found**
6. If no cycle:
   - Mark all visited nodes from this start to avoid rechecking

---

## Why this works

- In a circular path, a faster pointer will always catch a slower one **if and only if** a valid cycle exists
- Direction checks ensure only valid cycles are considered
- Marking visited nodes prevents redundant work

---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)` (ignoring visited marking)

---

## Visualization

![Circular Array loop Visualization](../images/circulararrloop.png)

---

## Java Solution

```java
class Solution {

    public boolean circularArrayLoop(int[] nums) {
        int n = nums.length;
        boolean[] visited = new boolean[n];

        for (int i = 0; i < n; i++) {

            if (visited[i]) continue;

            int slow = i, fast = i;
            boolean dir = nums[i] > 0;

            while (true) {
                slow = nextIndex(nums, slow, dir);
                fast = nextIndex(nums, fast, dir);

                if (fast != -1)
                    fast = nextIndex(nums, fast, dir);

                if (slow == -1 || fast == -1)
                    break;

                if (slow == fast)
                    return true;
            }

            int idx = i;
            while (true) {
                int next = nextIndex(nums, idx, dir);
                visited[idx] = true;
                if (next == -1 || visited[next]) break;
                idx = next;
            }
        }
        return false;
    }

    private int nextIndex(int[] nums, int idx, boolean dir) {
        boolean currDir = nums[idx] > 0;
        if (currDir != dir) return -1;

        int n = nums.length;
        int next = ((idx + nums[idx]) % n + n) % n;

        if (next == idx) return -1;
        return next;
    }
}
