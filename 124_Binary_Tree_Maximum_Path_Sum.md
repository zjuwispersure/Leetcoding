[题目介绍](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

Given a **non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

**Example 2:**

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```



各种有问题，参考下其他人的代码逻辑。旧的代码在最小值相加的时候越界。

MS(root) = max path sum

1. root must be used
2. at most one child can be used

最后return的时候，只返回一个方向上的值，为什么？这是因为在递归中，只能向父节点返回，不可能存在L->root->R的路径，只可能是L->root或R->root。

原本就是递归调用，只不过更新的时候用左右一起来更新，递归的逻辑还是保持返回左或右的逻辑。

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
    int maxPathSum(TreeNode* root) {
        int result=INT_MIN;
        help(root, result);
        return result;
    }
    
    int help(TreeNode* root, int& result){
        if(!root)    return 0;
        int left=max(0, help(root->left, result));
        int right=max(0, help(root->right, result));
        //root\left\right比较完毕
        result=max(result, left+right+root->val);
        return max(left, right)+root->val;
    }
};
```



参考链接：

1. https://zxi.mytechroad.com/blog/tree/leetcode-124-binary-tree-maximum-path-sum/