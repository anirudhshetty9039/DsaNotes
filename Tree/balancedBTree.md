# Balanced Binary Tree

## Approach

For each node, calculate the heights of its left and right subtrees. The node is balanced when their height difference is at most `1`; both subtrees must also be balanced. This version recalculates subtree heights at each node, so nodes can be visited multiple times.

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
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }

        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);

        if (Math.abs(leftHeight - rightHeight) > 1) {
            return false;
        }

        // Both subtrees must also be balanced.
        return isBalanced(root.left) && isBalanced(root.right);
    }

    // Returns the height of a node; an empty subtree has height 0.
    private int getHeight(TreeNode node) {
        if (node == null) {
            return 0;
        }

        int leftHeight = getHeight(node.left);
        int rightHeight = getHeight(node.right);

        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```

## Complexity

- **Time:** `O(n^2)` in the worst case, because `getHeight` traverses subtrees repeatedly.
- **Space:** `O(h)` recursion stack, where `h` is the tree height.
