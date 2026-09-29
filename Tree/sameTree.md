# Same Tree

## Approach

Compare the two trees recursively. Matching null nodes are equal; if only one node is null or their values differ, the trees are different. Otherwise, both corresponding left and right subtrees must be the same.

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }

        if (p == null || q == null) {
            return false;
        }

        if (p.val != q.val) {
            return false;
        }

        return isSameTree(p.left, q.left)
                && isSameTree(p.right, q.right);
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes in the smaller tree in the worst case.
- **Space:** `O(h)` recursion stack, where `h` is the maximum height of the two trees.




