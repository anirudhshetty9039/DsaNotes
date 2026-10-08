# Linked List Cycle

## Approach

Use Floyd’s slow and fast pointer algorithm. Move `slow` one node at a time and `fast` two nodes at a time. If the list has a cycle, the fast pointer eventually catches the slow pointer inside the cycle. If `fast` reaches the end, the list has no cycle.

## Java Solution

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        // Fast must have two available steps before either pointer advances.
        while (fast != null && fast.next != null) {
            slow = slow.next;       // Move one step.
            fast = fast.next.next;  // Move two steps.

            // A meeting proves the pointers are traveling around a cycle.
            if (slow == fast) {
                return true;
            }
        }

        return false; // Fast reached the end of an acyclic list.
    }
}
```

## Complexity

- **Time:** `O(n)` in the worst case.
- **Auxiliary space:** `O(1)`; only two pointers are used.
