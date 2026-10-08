# Reverse Linked List

## Approach

Iterate through the list while tracking the previous node, the current node, and the next node. Save `current.next` before reversing the link so the remaining list is not lost. When the traversal ends, `prev` is the new head.

## Java Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode current = head;
        ListNode prev = null;

        while (current != null) {
            ListNode next = current.next; // Save the rest of the list.
            current.next = prev;          // Reverse the current link.
            prev = current;               // Move prev forward.
            current = next;               // Continue with the saved node.
        }

        return prev; // The last visited node is the new head.
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes.
- **Auxiliary space:** `O(1)`; the list is reversed in place.
