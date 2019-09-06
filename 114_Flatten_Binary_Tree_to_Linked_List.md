[题目介绍](https://leetcode.com/problemset/top-100-liked-questions/)

Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

```
    1
   / \
  2   5
 / \   \
3   4   6
```

The flattened tree should look like:

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```



### 非递归解法

从根节点出发，将右子树作为左子树最后节点的右子树，左子树作为右子树，左子树置为NULL，然后root->right进行处理。

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
    void flatten(TreeNode* root) {
        TreeNode* now = root;
        while(now){
            if(now->left){
                TreeNode* pre = now->left;
                while(pre->right){
                    pre = pre->right;
                }
                pre->right = now ->right;
                now->right = now->left;
                now->left = NULL;
            }
            now = now->right;
        }
        
    }
};
```



### 递归解法

反先序遍历，不太好理解。

先处理右子树，在处理左子树，在处理root节点。

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
    TreeNode* prev = NULL;
    void flatten(TreeNode* root) {
        if(root == NULL){
            return;
        }
        flatten(root->right);
        flatten(root->left);
        root->right = prev;
        root->left = NULL;
        prev = root;
        
    }
};
```

