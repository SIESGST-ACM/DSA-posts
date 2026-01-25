# Pattern 3: Slow & Fast Pointer

The **Slow & Fast Pointer pattern** is mainly used when the input is a **linked list**  
and we are required to solve the problem using **O(1) extra space**.

---

## When should you think of Slow & Fast Pointer?

You’ll usually see these hints in the problem:

1. The data structure is a **linked list**
2. The question mentions:
   - cycle or loop
   - middle of the linked list
   - palindrome check
3. You are asked to solve the problem using **constant space**

If these appear together, this pattern is a strong match.

---

## The Intuition

Instead of using extra memory, we use **two pointers moving at different speeds**.

This difference in speed helps us:
- Find positions like the middle
- Detect cycles
- Split the list efficiently

---

## How the Pattern Works

We use two pointers:

- **Slow pointer**
  - Moves **one step** at a time
- **Fast pointer**
  - Moves **two steps** at a time

So in every iteration:

slow → 1 step
fast → 2 steps


This means fast gains **one extra node** over slow on every move.

---

## Why this helps

### 1. Finding the middle of a linked list

- When the **fast pointer reaches the end**
- The **slow pointer is at the middle**

This works because fast moves twice as fast as slow.

---

### 2. Detecting a cycle (loop)

- If there is **no cycle**
  - Fast pointer reaches `null`
- If there **is a cycle**
  - Fast pointer keeps looping
  - Eventually, fast **catches up to slow**

This meeting confirms that a cycle exists.

This technique is also known as **Cycle Detection**.

---

### 3. Palindrome Linked List

- Slow pointer helps reach the **middle**
- Fast pointer helps decide **where to split**
- The second half can then be reversed and compared

---

## Cycle Intuition (Simple)

- **No cycle** → fast reaches `null`
- **Cycle exists** → fast and slow meet inside the loop

The meeting point guarantees a loop.

---

## Why this pattern is powerful

- Uses **no extra memory**
- Works in **one pass**
- Extremely common in **coding interviews**
- Forms the base for many linked list problems

---