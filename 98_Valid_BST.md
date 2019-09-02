[题目介绍](https://leetcode.com/problems/validate-binary-search-tree/)



典型的错误代码如下，只是在每个节点判断是否满足BST的条件，但是子节点中的节点是否满足没有考虑。

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
    bool isValidBST(TreeNode* root) {
        if(root == NULL){
            return true;
        }
        
        if(root->left != NULL && root->val <= root->left->val){
            return false;
        }
        if(root->right != NULL && root->val >= root->right->val){
            return false;
        }
        return isValidBST(root->left) && isValidBST(root->right);
    }
};
```

