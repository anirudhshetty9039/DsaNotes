# Merge Two Sorted Lists

## Approach

Use a dummy node to simplify building the merged list. Compare the current nodes of both sorted lists, link the smaller one to the result, and advance that list. Once one list is exhausted, attach the remaining nodes from the other list.

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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        // The dummy node avoids a special case for the merged list's first node.
        ListNode dummy = new ListNode();
        ListNode tail = dummy;

        // Link the smaller current node, keeping the merged list sorted.
        while (list1 != null && list2 != null) {
            if (list1.val < list2.val) {
                tail.next = list1;
                list1 = list1.next;
            } else {
                tail.next = list2;
                list2 = list2.next;
            }
            tail = tail.next;
        }

        // At most one list remains; its nodes are already sorted.
        tail.next = (list1 != null) ? list1 : list2;

        return dummy.next;
    }
}
```

## Complexity

Let `m` and `n` be the lengths of the two lists.

- **Time:** `O(m + n)`; each node is linked once.
- **Auxiliary space:** `O(1)`; existing nodes are reused, with one dummy node.
