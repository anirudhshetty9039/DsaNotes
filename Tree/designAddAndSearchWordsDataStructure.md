# Design Add and Search Words Data Structure

## Approach

Store words in a Trie. Adding a word follows or creates one node per letter. Searching follows a matching letter when the pattern has a letter; when it has `.`, try each existing child and continue recursively. A match succeeds only if the full pattern ends at a node marked as the end of a word.

## Java Solution

```java
class WordDictionary {
    // Each node has one child slot per lowercase English letter.
    private static class TrieNode {
        TrieNode[] children = new TrieNode[26];
        boolean isEndOfWord;
    }

    private final TrieNode root;

    public WordDictionary() {
        // The root represents the empty prefix.
        root = new TrieNode();
    }

    public void addWord(String word) {
        TrieNode current = root;

        for (char ch : word.toCharArray()) {
            int index = ch - 'a'; // Map 'a'..'z' to indexes 0..25.

            // Create the next node when this path does not exist yet.
            if (current.children[index] == null) {
                current.children[index] = new TrieNode();
            }
            current = current.children[index];
        }

        // Mark that a complete word ends at this node.
        current.isEndOfWord = true;
    }

    public boolean search(String word) {
        // Start matching the pattern at the root and its first character.
        return dfs(root, word, 0);
    }

    private boolean dfs(TrieNode current, String word, int index) {
        // The whole pattern matched only if this node ends a stored word.
        if (index == word.length()) {
            return current.isEndOfWord;
        }

        char ch = word.charAt(index);

        if (ch != '.') {
            // A regular letter has exactly one possible matching child.
            int childIndex = ch - 'a';
            if (current.children[childIndex] == null) {
                return false;
            }
            return dfs(current.children[childIndex], word, index + 1);
        }

        // '.' can match any one letter, so try every existing child.
        for (TrieNode child : current.children) {
            if (child != null && dfs(child, word, index + 1)) {
                return true;
            }
        }

        return false;
    }
}
```

## Complexity

Let `L` be the pattern length:

- **Add word:** `O(L)` time.
- **Search:** `O(26^L)` worst-case time when many characters are `.`; searches without wildcards take `O(L)`.
- **Space:** `O(S)` trie nodes for `S` total characters across added words, with 26 child slots per node. Search recursion uses up to `O(L)` stack space.

This implementation expects lowercase English letters in added words and uses `.` as the one-letter wildcard.
