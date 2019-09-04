[题目介绍](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)





### 递归解法

先序遍历的第一个节点root_value就是根节点root，然后去中序遍历中查找root_value的位置end，end之前的是root的左子树，end之后的是root的右子树，递归构造左右子树。

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int size = preorder.size();
        if(size == 0){
            return NULL;
        }
        int value = preorder[0];
        TreeNode* node = new TreeNode(value);
        int end = 0;
        for(end = 0; end < size; end++){
            if(inorder[end] == value){
                break;
            }
        }
       
        vector<int> left_pre(preorder.begin() + 1, preorder.begin() + end + 1);
        vector<int> left_in(inorder.begin(), inorder.begin() + end);
        vector<int> right_pre(preorder.begin() + end + 1, preorder.end());
        vector<int> right_in(inorder.begin()+ end +1 , inorder.end());
            
        node->left = buildTree(left_pre, left_in);
        node->right = buildTree(right_pre, right_in);
        }
        return node;
        
    }
};
```



看提交的内存太大，参考网上的说法来调整下，注意preorder中的坐标要转化下，用inorder中的delta来表示。

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return buildTree(preorder, 0 , preorder.size()-1, inorder, 0, inorder.size() - 1);
        
    }

    TreeNode* buildTree(vector<int>& preorder, int pre_begin, int pre_end, vector<int>& inorder, int in_begin, int in_end) {
        if(pre_begin > pre_end || in_begin > in_end){
            return NULL;
        }
       
        TreeNode* node = new TreeNode(preorder[pre_begin]);
        for(int i = in_begin; i <= in_end; i++){
            if(inorder[i] == preorder[pre_begin]){
                node->left = buildTree(preorder, pre_begin+1, pre_begin + i - in_begin, inorder, in_begin, i-1);
                node->right = buildTree(preorder, pre_begin + i - in_begin +1, pre_end, inorder, i+1, in_end);
            }
        }
        
        return node;
        
    }
};
```

