# Palindrome Linked List

**Problem Link:** https://leetcode.com/problems/palindrome-linked-list/

## Why this problem?

This problem is a classic application of the **Slow & Fast Pointer pattern**.

The signals are clear:

- The data structure is a **linked list**
- We need to find the **middle**
- No extra space is allowed
- We must solve it in **O(n) time**

This makes Fast & Slow Pointer the perfect choice.

---

## The Intuition

We are given a singly linked list.

Our task is to check whether the list reads the **same forward and backward**.

A palindrome mirrors around its **middle**.

So the idea is:
- Find the middle of the list
- Reverse the second half
- Compare both halves node by node

---

## The Algorithm

### Step 1: Find the middle

Use two pointers:
- `slow` → moves one step
- `fast` → moves two steps

When `fast` reaches the end,  
`slow` will be at the **middle** of the list.

---

### Step 2: Reverse the second half

Reverse the linked list starting from `slow`.

This allows backward comparison using forward pointers.

---

### Step 3: Compare both halves

- Start one pointer from the head
- Start another from the reversed second half
- Compare values one by one

If all values match, the list is a palindrome.

---

## Why this works

- A palindrome mirrors around the middle
- Fast & Slow Pointer finds the middle efficiently
- Reversing avoids extra space
- Direct comparison confirms symmetry

---

## Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## Visualization

![Palindrome Linked list Visualization](../images/palindromeLL.png)

---

## Java Solution

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) return true;

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode secondHalf = reverse(slow);
        ListNode firstHalf = head;

        while (secondHalf != null) {
            if (firstHalf.val != secondHalf.val) return false;
            firstHalf = firstHalf.next;
            secondHalf = secondHalf.next;
        }
        return true;
    }

    private ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}