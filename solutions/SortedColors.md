# Sort Colors (Dutch National Flag Problem)

**Problem Link:** https://leetcode.com/problems/sort-colors/

## Why this problem?

This problem is a classic example of the **Three Pointer pattern** (from the Two Pointers family).

The signals are clear:

1. The input is an array  
2. The array contains only three distinct values (0, 1, 2)  
3. We must sort the array in-place  
4. No sorting function is allowed  

All these directly point to a pointer-based solution.

---

## The Intuition

We are given only three values:

- `0` → Red  
- `1` → White  
- `2` → Blue  

Our goal is to arrange them as:

0s → 1s → 2s


Since the values are limited, we don’t need traditional sorting.  
We just place each value in its correct region.

---

## The Algorithm

We divide the array into three regions:

- Left region → all `0`s  
- Middle region → all `1`s  
- Right region → all `2`s  

To achieve this in one pass, we use three pointers:

- `l` → position for the next `0`
- `m` → current element
- `h` → position for the next `2`

### Initial Setup

l = 0
m = 0
h = nums.length - 1


---

### At each step:

- If `nums[m] == 0`  
  - Swap `nums[m]` with `nums[l]`  
  - Move both `l` and `m`

- If `nums[m] == 2`  
  - Swap `nums[m]` with `nums[h]`  
  - Move only `h`

- If `nums[m] == 1`  
  - It is already in the correct place  
  - Move `m`

Continue until `m > h`.

---

## Example

Input:
[2,0,2,1,1,0]


Output:
[0,0,1,1,2,2]


---

## Why this works

- `0`s are pushed to the left
- `2`s are pushed to the right
- `1`s automatically stay in the middle
- Each element is processed only once

---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---
![SortedColor Visualisation](../images/sortedColor.png)

## Java Solution

```java
class Solution {
    public void sortColors(int[] nums) {
        int l = 0;
        int m = 0;
        int h = nums.length - 1;

        while (m <= h) {
            if (nums[m] == 0) {
                int temp = nums[l];
                nums[l] = nums[m];
                nums[m] = temp;
                l++;
                m++;
            } else if (nums[m] == 2) {
                int temp = nums[h];
                nums[h] = nums[m];
                nums[m] = temp;
                h--;
            } else {
                m++;
            }
        }
    }
}