# Kth Smallest Element in a BST

## Approach

Inorder traversal visits a binary search tree's values in ascending order. Collect the values, then return the element at index `k - 1` because Java lists are zero-indexed.

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
    public int kthSmallest(TreeNode root, int k) {
        List<Integer> values = new ArrayList<>();
        inorder(root, values);
        return values.get(k - 1);
    }

    private void inorder(TreeNode root, List<Integer> values) {
        if (root == null) {
            return;
        }

        inorder(root.left, values);
        values.add(root.val);
        inorder(root.right, values);
    }
}
```

## Complexity

- **Time:** `O(n)` in the worst case, where `n` is the number of nodes.
- **Space:** `O(n)` for the list of values, plus `O(h)` recursion stack space, where `h` is the tree height.
