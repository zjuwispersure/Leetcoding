[题目介绍](https://leetcode.com/problems/lru-cache/submissions/)

Design and implement a data structure for [Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a **positive** capacity.

**Follow up:**
Could you do both operations in **O(1)** time complexity?

**Example:**

```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```



### 解法

最开始想到用hash来保存，用链表来记录，但是感觉太复杂，而且复杂度好像也不符合要求。但是其实hashmap可以直接存放链表位置，链表可以通过splice函数来很方便的进行节点的移动。

最后参考了其他人的代码。

```
class LRUCache {
    int capacity;
    list<pair<int, int>> items;
    unordered_map<int, list<pair<int, int>>::iterator > cache;
public:
    LRUCache(int capacity) : capacity(capacity) {
        
    }
    
    int get(int key) {
        if(cache.find(key) == cache.end()){
            return -1;
        }
        items.splice(items.begin(), items, cache[key]);
        return cache[key]->second;
        
    }
    
    void put(int key, int value) {
        if(cache.find(key) == cache.end()){
            if(cache.size() == capacity){
                cache.erase(items.back().first);
                items.pop_back();
            }
            items.push_front(std::make_pair(key, value));
            cache[key] = items.begin();            
        } else {
            cache[key]->second = value;
            items.splice(items.begin(), items, cache[key]);
        }
        
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

