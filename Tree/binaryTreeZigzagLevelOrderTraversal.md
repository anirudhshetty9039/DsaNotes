# Binary Tree Zigzag Level Order Traversal

## Approach

Use breadth-first search (BFS) to collect values one level at a time. Keep a direction flag and reverse every other level before adding it to the result. Children are always enqueued from left to right; only the collected level's order changes.

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        boolean reverse = false;

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

            if (reverse) {
                Collections.reverse(level);
            }

            result.add(level);
            reverse = !reverse;
        }

        return result;
    }
}
```

## Complexity

- **Time:** `O(n)`, where `n` is the number of nodes; each node is processed once, and reversing levels takes `O(n)` total across the traversal.
- **Space:** `O(w)` for the queue, where `w` is the maximum width of the tree. The returned levels require `O(n)` space.
