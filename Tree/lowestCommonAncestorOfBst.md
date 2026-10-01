# Lowest Common Ancestor of a BST

## Approach

Use the BST ordering to move toward both target nodes. If both values are greater than the current node, continue right; if both are smaller, continue left. Otherwise, the current node is where the paths meet, so it is the lowest common ancestor.

This assumes both target nodes are present in the BST, as in the LeetCode problem.

## Java Solution

```java
/**
 * Definition for a binary tree node.
 *
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }

        if (p.val > root.val && q.val > root.val) {
            return lowestCommonAncestor(root.right, p, q);
        }

        if (p.val < root.val && q.val < root.val) {
            return lowestCommonAncestor(root.left, p, q);
        }

        return root;
    }
}
```

## Complexity

- **Time:** `O(h)`, where `h` is the BST height.
- **Space:** `O(h)` recursion stack in this recursive implementation.
