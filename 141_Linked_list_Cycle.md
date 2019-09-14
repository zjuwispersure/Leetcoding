[题目介绍](https://leetcode.com/problems/linked-list-cycle/)

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

 

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**Follow up:**

Can you solve it using *O(1)* (i.e. constant) memory?





### 解法：快慢指针

快慢两个指针，慢指针每次往后移动一个；快指针每次往后移动两个，如有移动过程中发现有重复的，则说明有环。

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {  
        if(head == NULL){
            return false;
        }
        ListNode* slowNode = head;
        ListNode* fastNode = head;
        while(slowNode && fastNode){
            slowNode = slowNode->next;
            if(fastNode->next){
                fastNode = fastNode->next->next;
            } else {
                return false;
            }
            if(slowNode == fastNode){
                return true;
            }
        }
        return false;
        
    }
};
```

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {  
       ListNode* slow = head;
        ListNode* fast = head;
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
        
    }
};
```





### 解法：hash

用hash来保存位置信息，如果碰到一样的说明有环。

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
       std::unordered_set<ListNode *> nodeSet;
        while(head){
            if(nodeSet.find(head) != nodeSet.end()){
                return true;
            } 
            nodeSet.insert(head);
            head = head->next;
        }
        return false;
    }
};
```



