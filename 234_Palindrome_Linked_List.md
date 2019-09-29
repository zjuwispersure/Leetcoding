[题目介绍](https://leetcode.com/problems/palindrome-linked-list/)

Given a singly linked list, determine if it is a palindrome.

**Example 1:**

```
Input: 1->2
Output: false
```

**Example 2:**

```
Input: 1->2->2->1
Output: true
```

**Follow up:**
Could you do it in O(n) time and O(1) space?





### 解法

搞一个queue和一个stack，然后依次对比。

空间复杂度为O(n)

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
    bool isPalindrome(ListNode* head) {
        ListNode* base = head;
        queue<int> nodeQueue;
        stack<int> nodeStack;
        int num = 0;
        while(head){
            nodeStack.push(head->val);
            nodeQueue.push(head->val);
            num++;
            head = head->next;
        }
        while(!nodeStack.empty() && !nodeQueue.empty()){
            if(nodeStack.top() != nodeQueue.front()){
                return false;
            }
            nodeStack.pop();
            nodeQueue.pop();
        }
        
        return true;
        
    }
};
```



上面算法有几个问题：

1、对比一半就可以

2、不需要使用queue。

step1:

```
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode* base = head;
        queue<int> nodeQueue;
        stack<int> nodeStack;
        int num = 0;
        while(head){
            nodeStack.push(head->val);
            nodeQueue.push(head->val);
            num++;
            head = head->next;
        }
        int i = 0;
        while(!nodeStack.empty() && !nodeQueue.empty() && i < num/2){
            if(nodeStack.top() != nodeQueue.front()){
                return false;
            }
            nodeStack.pop();
            nodeQueue.pop();
        }
        
        return true;
        
    }
};
```

step2:

```
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode* base = head;
        stack<int> nodeStack;
        int num = 0;
        while(head){
            nodeStack.push(head->val);
            num++;
            head = head->next;
        }
        int i = 0;
        while(!nodeStack.empty() && i < num/2 && base){
            if(base->val != nodeStack.top()){
                return false;
            }
            base = base->next;
            nodeStack.pop();
        }
        
        return true;
        
    }
};
```



### 解法：递归

按照这个对比方法，第一个和最后一个进行比较，然后head--，tail++。

和类似于栈的方法。

```
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        return check(head, head);
    }
    
    bool check(ListNode*& head, ListNode* p) {
        if(!p) { return true; }
        bool isPal = check(head, p->next);
        if(head->val != p->val) {
            return false;
        }
        head = head->next;
        return isPal;
    }
};
```

