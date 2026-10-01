# Implement Trie (Prefix Tree)

## Approach

Each trie node stores up to 26 child links, one for each lowercase English letter, and a flag marking the end of a complete word. Insertion creates any missing nodes; search checks both the path and the end-of-word flag; prefix search only needs to confirm that the path exists.

## Java Solution

```java
class Trie {
    // A node has one child slot per lowercase English letter.
    private static class TrieNode {
        TrieNode[] children = new TrieNode[26];
        boolean isEndOfWord;
    }

    private final TrieNode root;

    public Trie() {
        // The root represents the empty prefix.
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode current = root;

        for (char ch : word.toCharArray()) {
            int index = ch - 'a'; // Map 'a'..'z' to indexes 0..25.

            // Create the path node if this character has not been seen here.
            if (current.children[index] == null) {
                current.children[index] = new TrieNode();
            }
            current = current.children[index];
        }

        // Distinguish a complete word from a prefix of another word.
        current.isEndOfWord = true;
    }

    public boolean search(String word) {
        TrieNode current = findNode(word);

        // A matching path alone is not enough; it must end a stored word.
        return current != null && current.isEndOfWord;
    }

    public boolean startsWith(String prefix) {
        // Any existing path represents a stored prefix.
        return findNode(prefix) != null;
    }

    // Follows a string's character path and returns its final node, if present.
    private TrieNode findNode(String text) {
        TrieNode current = root;

        for (char ch : text.toCharArray()) {
            int index = ch - 'a';
            if (current.children[index] == null) {
                return null;
            }
            current = current.children[index];
        }

        return current;
    }
}
```

## Complexity

For a word or prefix of length `L`:

- **Insert:** `O(L)` time.
- **Search:** `O(L)` time.
- **Starts with:** `O(L)` time.
- **Space:** Up to `O(26L)` new child slots in the worst case for inserting a word; equivalently `O(L)` trie nodes, with a fixed 26-slot array per node.

This implementation expects lowercase English letters (`'a'` through `'z'`).
