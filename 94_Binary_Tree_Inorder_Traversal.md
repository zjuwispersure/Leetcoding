[题目介绍](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Given a binary tree, return the *inorder* traversal of its nodes' values.

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?



## 求解

### 解法1:递归

中序遍历，按照左中右的顺序遍历。递归方法比较简单：左子树递归；根结点保存；右子树递归。

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
        
    }
    void traversal(TreeNode* root, vector<int>& result){
        if(root == NULL){
            return ;
        }else{
            traversal(root->left, result);
            result.push_back(root->val);
            traversal(root->right, result);
        }
    }
};
```



### 解法2:非递归

使用栈进行循环

1. 结点入栈，所有的左节点入栈；
2. 如果结点为空，出栈，获取结点值；然后将右结点入栈；

```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode*> s;
        TreeNode *p = root;
        while (!s.empty() || p) {
            if (p) {
                s.push(p);
                p = p->left;
            } else {
                p = s.top(); s.pop();
                res.push_back(p->val);
                p = p->right;
            }
        }
        return res;
    }
};
```

