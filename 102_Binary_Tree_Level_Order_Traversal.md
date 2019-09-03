[题目介绍](https://leetcode.com/problems/binary-tree-level-order-traversal/)



使用队列，用数字来记录每一层入队列的数量，这个代码有些丑陋。

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root == NULL){
            return result;
        } 
        queue<TreeNode*> que;
        que.push(root);
        int size = 1;
        while(!que.empty()){
            vector<int> tmp;
            int tmp_size = 0;
            while(size-- > 0){
                TreeNode* node = que.front();
                que.pop();

                if(node != NULL){
                    tmp.push_back(node->val);
                    if(node->left != NULL){
                        tmp_size++;
                        que.push(node->left);
                    }
                    if(node->right != NULL){
                        tmp_size++;
                        que.push(node->right);
                    }
                }
            }
            size = tmp_size;
            result.push_back(tmp);
        }
        return result;
    }
};
```



参考其他人的方法调整下，size可以直接去获取队列的数量而不是自己去累加。

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root == NULL){
            return result;
        } 
        queue<TreeNode*> que;
        que.push(root);
        while(!que.empty()){
            vector<int> tmp;
            int size = que.size();
            while(size-- > 0){
                TreeNode* node = que.front();
                que.pop();

                if(node != NULL){
                    tmp.push_back(node->val);
                    if(node->left != NULL){
                        que.push(node->left);
                    }
                    if(node->right != NULL){
                        que.push(node->right);
                    }
                }
            }
            result.push_back(tmp);
        }
        return result;
    }
};
```



还有一种不是按照层次遍历，但是最后结果类似于层次遍历的方法，记录树的深度，每个深度按照次序往里塞值。

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
    vector<vector<int> > levelOrder(TreeNode *root) {
	vector<vector<int> > retVal;
	levelOrder(root, retVal, 0);
	return retVal;
}

void levelOrder(TreeNode* root, vector<vector<int> > &v, int currLevel) {
	if (root == NULL) {
		return;
	}

	if (v.empty() || currLevel > (v.size() - 1)) {
		v.push_back(vector<int>());
	}

	v[currLevel].push_back(root->val);

	levelOrder(root->left, v, currLevel + 1);
	levelOrder(root->right, v, currLevel + 1);
}
};
```

