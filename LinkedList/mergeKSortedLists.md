# Merge K Sorted Lists

## Approach

Put every value from every input list into a min-heap. Repeatedly remove the smallest value and append it to a new result list. The heap guarantees the values are added in sorted order.

This version creates new result nodes and stores all `N` input values in the heap, where `N` is the total number of nodes.

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
    public ListNode mergeKLists(ListNode[] lists) {
        // Store all values in a min-heap so the smallest is always removed first.
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (ListNode list : lists) {
            while (list != null) {
                minHeap.add(list.val);
                list = list.next;
            }
        }

        // Build a fresh list in ascending order from the heap values.
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;

        while (!minHeap.isEmpty()) {
            tail.next = new ListNode(minHeap.remove());
            tail = tail.next;
        }

        return dummy.next;
    }
}
```

## Complexity

Let `N` be the total number of nodes across all lists.

- **Time:** `O(N log N)` for heap insertions and removals.
- **Auxiliary space:** `O(N)` for the min-heap.
- **Result space:** `O(N)` for the newly created list nodes.
