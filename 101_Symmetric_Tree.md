[题目介绍](https://leetcode.com/problems/symmetric-tree/)

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

 

But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

 

**Note:**
Bonus points if you could solve it both recursively and iteratively.



一看题目就有点蒙了，后面还是要先自己思考，看到是个简单题，但是混沌状态感觉不简单。



### 递归

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
    bool isSymmetric(TreeNode* root) {
        return root == NULL || check(root->left, root->right);
        
    }
    bool check(TreeNode* left, TreeNode* right){
        if(left == NULL && right == NULL){
            return true;
        } else if(left != NULL && right != NULL){
            return left->val == right->val && check(left->left, right->right) && check(left->right, right->left);
        }
        return false;
    }
};
```





### 非递归

