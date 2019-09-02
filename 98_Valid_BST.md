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





解法：

引入最大值和最小值，这样左右子树的时候可以用来判断是否满足。

其中valid的最大值和最小值只int类型的时候出错，只是调整类型后可以跑过，为啥呢？

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
       return valid(root, LONG_MIN, LONG_MAX);
    }
    
    bool valid(TreeNode* root, long min, long max){
         if(!root){
            return true;
        }
        if(root->val >= max || root->val <= min){
            return false;
        }
        
        return valid(root->left, min, root->val) && valid(root->right, root->val, max);
    }
};
```

