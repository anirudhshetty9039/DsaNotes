# Diameter of Binary Tree

## Approach

Use a postorder depth-first traversal. For each node, calculate the heights of its left and right subtrees. A path passing through that node has `leftHeight + rightHeight` edges; track the largest such value as the diameter. Return the node's height to its parent.

The diameter is measured in **edges**, as required by the problem. The height helper returns `0` for a null node, so a leaf has height `1`.

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
    private int maxDiameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        getHeight(root);
        return maxDiameter;
    }

    private int getHeight(TreeNode node) {
        if (node == null) {
            return 0;
        }

        int leftHeight = getHeight(node.left);
        int rightHeight = getHeight(node.right);

        maxDiameter = Math.max(maxDiameter, leftHeight + rightHeight);

        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is visited once.
- **Space:** `O(h)` recursion stack, where `h` is the tree height.
