# Add Two Numbers

## Approach

The input lists store digits in reverse order, so start at the head of each list and add corresponding digits. Treat a missing digit as `0`, include the carry in each sum, and append `sum % 10` to the result. Continue while either list has digits or a carry remains.

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // Dummy node simplifies appending the first result digit.
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        int carry = 0;

        // Keep going after the lists end if there is still a carry to append.
        while (l1 != null || l2 != null || carry != 0) {
            int x = (l1 != null) ? l1.val : 0;
            int y = (l2 != null) ? l2.val : 0;
            int sum = carry + x + y;

            carry = sum / 10; // Carry the tens digit to the next position.
            current.next = new ListNode(sum % 10); // Store the ones digit.
            current = current.next;

            // Advance each list only if it still has a node.
            if (l1 != null) {
                l1 = l1.next;
            }
            if (l2 != null) {
                l2 = l2.next;
            }
        }

        return dummy.next;
    }
}
```

## Complexity

Let `m` and `n` be the lengths of the two input lists.

- **Time:** `O(max(m, n))`.
- **Auxiliary space:** `O(1)`, excluding the result list.
- **Result space:** `O(max(m, n))`, with at most one extra node for a final carry.
