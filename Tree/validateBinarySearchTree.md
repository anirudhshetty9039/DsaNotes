# Validate Binary Search Tree

## Approach

An inorder traversal of a valid binary search tree visits node values in strictly increasing order. Keep the previously visited value and compare it with each current node. If the current value is not greater, the tree is invalid.

The `prev` field is reset at the start of `isValidBST` so the result does not depend on an earlier call to the same `Solution` instance.

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
    private Integer prev;

    public boolean isValidBST(TreeNode root) {
        prev = null;
        return inorder(root);
    }

    private boolean inorder(TreeNode root) {
        if (root == null) {
            return true;
        }

        if (!inorder(root.left)) {
            return false;
        }

        if (prev != null && prev >= root.val) {
            return false;
        }

        prev = root.val;
        return inorder(root.right);
    }
}
```

## Complexity

- **Time:** `O(n)` in the worst case, where `n` is the number of nodes.
- **Space:** `O(h)` recursion stack, where `h` is the tree height.
