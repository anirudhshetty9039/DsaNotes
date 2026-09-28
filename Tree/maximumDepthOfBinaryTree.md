# Maximum Depth of Binary Tree

## Approach

Use recursion to find the depth of each subtree. An empty tree has depth `0`; otherwise, the tree's depth is `1` plus the greater depth of its left and right subtrees.

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
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is visited once.
- **Space:** `O(h)` recursion stack, where `h` is the tree height.
