[题目介绍](https://leetcode.com/problems/implement-trie-prefix-tree/)

mplement a trie with `insert`, `search`, and `startsWith` methods.

**Example:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

**Note:**

- You may assume that all inputs are consist of lowercase letters `a-z`.

- All inputs are guaranteed to be non-empty strings.

  



### 解法

用unordered_set来记录，每次插入的时候将所有的前缀都保存下来。

```
class Trie {
public:
    unordered_set<string> valueSet;
    unordered_set<string> prefixSet;
    
    /** Initialize your data structure here. */
    Trie() {
        
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        for(int i = 0; i<= word.size(); i++){
            prefixSet.insert(word.substr(0, i));
        }
        valueSet.insert(word);
        
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        return valueSet.find(word) != valueSet.end();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        return prefixSet.find(prefix) != prefixSet.end();
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```





进阶版

```
class Trie {
public:
    Trie() {}

    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->next.count(ch)) { node->next[ch] = new Trie(); }
            node = node->next[ch];
        }
        node->isword = true;
    }

    bool search(string word) {
        Trie* node = this;
        for (char ch : word) {
            if (!node->next.count(ch)) { return false; }
            node = node->next[ch];
        }
        return node->isword;
    }

    bool startsWith(string prefix) {
        Trie* node = this;
        for (char ch : prefix) {
            if (!node->next.count(ch)) { return false; }
            node = node->next[ch];
        }
        return true;
    }

private:
    unordered_map<char, Trie*> next = {};
    bool isword = false;
};
/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

