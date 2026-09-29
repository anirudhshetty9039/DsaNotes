# Subtree of Another Tree

## Approach

Try matching `subRoot` at each node in `root`. If the current node and `subRoot` are identical, a match is found; otherwise, search the left and right subtrees of `root`.

The helper compares both corresponding child pairs. They must **both** match, so the recursive calls are joined with `&&`.

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
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) {
            return subRoot == null;
        }

        if (isSame(root, subRoot)) {
            return true;
        }

        return isSubtree(root.left, subRoot)
                || isSubtree(root.right, subRoot);
    }

    private boolean isSame(TreeNode root, TreeNode subRoot) {
        if (root == null && subRoot == null) {
            return true;
        }

        if (root == null || subRoot == null || root.val != subRoot.val) {
            return false;
        }

        return isSame(root.left, subRoot.left)
                && isSame(root.right, subRoot.right);
    }
}
```

## Complexity

- **Time:** `O(m * n)` in the worst case, where `n` is the number of nodes in `root` and `m` is the number of nodes in `subRoot`.
- **Space:** `O(h)`, where `h` is the height of `root` for the search recursion, plus the height of `subRoot` while comparing trees.
