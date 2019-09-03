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

按照root节点对称分布，画出三层的树来进行对比即可

1. 如果为空，true
2. 如果root为空，比较2left和2right
3. 如果2相等，则第三层需要比较的是：31left与34right，32right与33left

```
               1root
       2left           2right
  3left  32right   33left  34right
```



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

使用栈，入栈的时候将需要验证的两个依次入栈，出栈的时候用top的两个进行比较

1. 如果相等，则按照左左/右右，左右/右左的顺序入栈
2. 不相等，直接返回false

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
        stack<TreeNode*> st;
        if(root == NULL){
            return true;
        }
        st.push(root->left);
        st.push(root->right);
        while(!st.empty()){
            TreeNode* node1 = st.top();
            st.pop();
            TreeNode* node2 = st.top();
            st.pop();
            if(node1 == NULL && node2 == NULL){
                continue;
            }
            if(node1 != NULL && node2 != NULL && node1->val == node2->val){
                st.push(node1->left);
                st.push(node2->right);
                st.push(node1->right);
                st.push(node2->left);
            } else {
                return false;
            }
        }
        return true;
        
    }
};
```



