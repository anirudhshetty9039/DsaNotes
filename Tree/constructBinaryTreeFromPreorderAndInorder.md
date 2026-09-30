# Construct Binary Tree from Preorder and Inorder Traversal

## Approach

Preorder visits the root before its children, so `preIndex` identifies the next subtree root. Use a map from each inorder value to its index to divide the current inorder range into left and right subtrees. Recursively build those ranges.

This method assumes all node values are unique, as required by the problem, so each value has one unambiguous inorder position.

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
    private int preIndex = 0;
    private final Map<Integer, Integer> inorderIndex = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        for (int i = 0; i < inorder.length; i++) {
            inorderIndex.put(inorder[i], i);
        }

        return build(preorder, 0, inorder.length - 1);
    }

    private TreeNode build(int[] preorder, int left, int right) {
        if (left > right) {
            return null;
        }

        int rootValue = preorder[preIndex++];
        TreeNode root = new TreeNode(rootValue);
        int mid = inorderIndex.get(rootValue);

        root.left = build(preorder, left, mid - 1);
        root.right = build(preorder, mid + 1, right);

        return root;
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each value is indexed and processed once.
- **Space:** `O(n)` for the index map and, in the worst case, the recursion stack.
