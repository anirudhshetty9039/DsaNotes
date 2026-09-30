# Binary Tree Level Order Traversal

## Approach

Use breadth-first search (BFS) with a queue. At the start of each iteration, capture the queue size; those nodes are exactly the current level. Collect their values, enqueue their non-null children, then add the completed level to the result.

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            List<Integer> level = new ArrayList<>();
            int levelSize = queue.size();

            for (int i = 0; i < levelSize; i++) {
                TreeNode current = queue.poll();
                level.add(current.val);

                if (current.left != null) {
                    queue.add(current.left);
                }
                if (current.right != null) {
                    queue.add(current.right);
                }
            }

            result.add(level);
        }

        return result;
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is processed once.
- **Space:** `O(w)` for the queue, where `w` is the maximum width of the tree. The returned levels require `O(n)` space.
