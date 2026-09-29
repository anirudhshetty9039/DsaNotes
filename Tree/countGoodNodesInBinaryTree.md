# Count Good Nodes in Binary Tree

## Approach

Traverse the tree from the root while carrying the largest value seen on the path so far. A node is good when its value is greater than or equal to that maximum. Update the maximum for its children, count the good nodes in both subtrees, and add those counts to the current node's contribution.

Each recursive branch receives its own `maxValue` argument, so updates on one path do not affect another.

## Java Solution

```java
/**
 * Definition for a binary tree node.
 *
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int goodNodes(TreeNode root) {
        return countGood(root, Integer.MIN_VALUE);
    }

    private int countGood(TreeNode node, int maxValue) {
        if (node == null) {
            return 0;
        }

        int count = 0;
        if (node.val >= maxValue) {
            count++;
            maxValue = node.val;
        }

        count += countGood(node.left, maxValue);
        count += countGood(node.right, maxValue);

        return count;
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is visited once.
- **Space:** `O(h)` recursion stack, where `h` is the tree height.
