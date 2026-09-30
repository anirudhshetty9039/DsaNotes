# Binary Tree Right Side View

## Approach

Use breadth-first search (level order traversal). Track the number of nodes at the start of each level, and add the last node processed at that level to the result. Since children are enqueued left to right, that last node is the rightmost visible node.

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            int currentSize = queue.size();

            for (int i = 0; i < currentSize; i++) {
                TreeNode current = queue.poll();

                if (i == currentSize - 1) {
                    result.add(current.val);
                }

                if (current.left != null) {
                    queue.add(current.left);
                }
                if (current.right != null) {
                    queue.add(current.right);
                }
            }
        }

        return result;
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is processed once.
- **Space:** `O(w)` for the queue, where `w` is the maximum width of the tree.
