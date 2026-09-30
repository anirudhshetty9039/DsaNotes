# Validate Binary Search Tree

## Approach

Check each node against a valid range. A node must be strictly greater than its lower bound and strictly less than its upper bound. Pass the current value as the upper bound to the left subtree and as the lower bound to the right subtree. Use `long` bounds so `Integer.MIN_VALUE` and `Integer.MAX_VALUE` are valid node values.

## Java Solution

```java
/**
 * Definition for a binary tree node.
 *
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
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
    public boolean isValidBST(TreeNode root) {
        return check(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean check(TreeNode root, long min, long max) {
        if (root == null) {
            return true;
        }

        if (root.val <= min || root.val >= max) {
            return false;
        }

        return check(root.left, min, root.val)
                && check(root.right, root.val, max);
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is checked once.
- **Space:** `O(h)` recursion stack, where `h` is the tree height.
