[题目介绍](https://leetcode.com/problems/invert-binary-tree/)



Invert a binary tree.

**Example:**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**Trivia:**
This problem was inspired by [this original tweet](https://twitter.com/mxcl/status/608682016205344768) by [Max Howell](https://twitter.com/mxcl):

> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.



### 解法：递归

左右互换，然后递归处理。

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
    TreeNode* invertTree(TreeNode* root) {
        if(root==NULL){
return root;
        }
        TreeNode* tmp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(tmp);
        return root;
    }
};
```





### 解法：非递归

使用队列，从队列中拿到节点后，交换左右，如果左右不空则继续入队列。

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
    TreeNode* invertTree(TreeNode* root) {
        if(root == NULL){
return root;
        }
        queue<TreeNode*> treeQueue;
        treeQueue.push(root);
        while(!treeQueue.empty()){
TreeNode* node = treeQueue.front();
            treeQueue.pop();
            if(node->left){
            treeQueue.push(node->left);}
if(node->right){
            treeQueue.push(node->right);}
            TreeNode* tmp = node->left;
            node->left = node->right;
            node->right = tmp;

}
        
        return root;
    }
};
```

