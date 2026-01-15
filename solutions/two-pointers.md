# Pattern 1: Two Pointers

Let’s learn Data Structures and Algorithms **pattern-wise**, not by solving random problems. If you can recognize the pattern, solving the problem becomes much easier.

## What is the Two Pointers pattern?

Instead of using nested loops to iterate through data, we use **two pointers** (indices or references) that move through the data structure based on a specific condition.

* **Efficiency:** This often reduces time complexity from **O(n²)** to **O(n)**.
* **Space:** It often allows for **O(1)** extra space (in-place solutions).

> **Note:** Two pointers do not always mean "no sorting." Sometimes, you must sort the array first to make this pattern work.

---

![Two Pointers Visualization](../images/2pointer.jpeg)

---

## When should you think of Two Pointers?

If you see multiple of these conditions together, **Two Pointers** is a strong hint:

1.  **Structure:** The input is an Array, Linked List, or String.
2.  **Order:** The data is already **sorted**, or the problem allows sorting first.
3.  **Grouping:** The problem asks about **pairs**, **triplets**, or **quadruplets**.
4.  **Operations:** You need to find a sum, remove duplicates, compare, reverse, or rearrange elements.
5.  **Constraints:** The problem requires **O(n)** time complexity with **O(1)** extra space.

## How does it usually work?

There are two common variations of this pattern:

### 1. Left and Right Pointers (Start & End)
Used for sorted arrays (e.g., Finding a pair that sums to a target).
* Initialize one pointer at the **start** (`0`) and one at the **end** (`n-1`).
* Move them toward each other until they meet.

### 2. Fast and Slow Pointers
Used for Linked Lists (e.g., Detecting a cycle or finding the middle).
* Both start at the head.
* The **Fast** pointer moves 2 steps, the **Slow** pointer moves 1 step.

## Code Example: Two Sum (Sorted Input)

Here is a classic example using the **Left & Right** approach.

```javascript
function twoSumSorted(arr, target) {
    let left = 0;
    let right = arr.length - 1;

    while (left < right) {
        let currentSum = arr[left] + arr[right];

        if (currentSum === target) {
            return [left + 1, right + 1]; // Found the pair
        } else if (currentSum > target) {
            right--; // Sum is too large, decrease right
        } else {
            left++;  // Sum is too small, increase left
        }
    }
    return []; // No pair found
}