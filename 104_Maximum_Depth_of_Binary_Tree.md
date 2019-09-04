[题目介绍](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.



### 递归解法

递归求解，判断左右子树的最大深度+1。

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
    int maxDepth(TreeNode* root) {
        if(root == NULL){
            return 0;
        } else {
            return 1 + max(maxDepth(root->left), maxDepth(root->right));
        }
        
    }
};
```



### 非递归解法

 使用队列，所有的节点都会依次加入队列，区分好每一层包含的元素，树的深度+1的同时将下一层的节点加入队列。

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
    int maxDepth(TreeNode* root) {
        queue<TreeNode*> treeQueue;
        if(root == NULL){
            return 0;
        }
        treeQueue.push(root);
        int result = 0;
        while(!treeQueue.empty()){
            int size = treeQueue.size();
            result++;
            for(int i = 0;i < size; i++){
                TreeNode * node = treeQueue.front();
                treeQueue.pop();
                if(node->left != NULL){
                    treeQueue.push(node->left); 
                }
                if(node->right != NULL){
                    treeQueue.push(node->right); 
                }
            }
        }
        return result;
        
    }
};
```

