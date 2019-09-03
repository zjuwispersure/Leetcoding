BST

# 定义

二叉查找树(Binary Search Tree)，也称为二叉搜索树、二叉有序树或排序二叉树，是指一棵空树或者具有下列性质的二叉树：

1. 若任意节点的左子树不空，则左子树所有节点的值均小于它的根节点的值；
2. 若任意节点的右子树不空，则右子树所有节点的值均大于它的根节点的值；
3. 任意节点的左右子树也分别为二叉查找树；
4. 没有键值相等的节点。



### 结构

```C++
 struct TreeNode {
   int val;
   TreeNode *left;
   TreeNode *right;
   TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 };
```







#### 时间复杂度

| 算法 | 平均            | 最差       |
| ---- | --------------- | ---------- |
| 空间 | ```O(n)```      | ```O(n)``` |
| 搜索 | ```O(log(n))``` | ```O(n)``` |
| 插入 | ```O(log(n))``` | ```O(n)``` |
| 删除 | ```O(log(n))``` | ```O(n)``` |



# 算法

###  查找

二叉搜索树b查找x的过程为：

1. 若b是空树，则搜索失败，否则：
2. 若x等于b根节点的val，则查找成功；否则：
3. 若x小于b根节点的val，则搜索左子树；否则：
4. 搜索右子树

```
// C function to search a given key in a given BST 
struct node* search(struct TreeNode* root, int key) 
{ 
    // Base Cases: root is null or key is present at root 
    if (root == NULL || root->val == key) 
       return root; 
     
    // Key is greater than root's key 
    if (root->val < key) 
       return search(root->right, key); 
  
    // Key is smaller than root's key 
    return search(root->left, key); 
} 
```



### 插入

二叉搜索树b插入节点s的过程为：

1. 若b是空树，则将s作为根节点插入；否则：
2. 若s->val等于b->val，则返回；否则：
3. 若s->val 小于b->val,则将s插入左子树中；否则：
4. 将s插入右子树中

```
Status InsertBST(TreeNode *root, ElemType e) {
    if (!root) {
        s = new TreeNode;
        s->val = e;
        s->left = s->right = NULL;
        root = s; // 被插節点*s为新的根结点
    } else if (e.val == root->val)
        return false;// 关键字等于e.key的数据元素，返回錯誤
    if (e.val < root->val)
        InsertBST(root->left, e);  // 將 e 插入左子樹
    else
        InsertBST(root->right, e);  // 將 e 插入右子樹
    return true;
}
```



### 删除

二叉搜索树删除节点分三种情况讨论：

1、





参考：

1. [https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%85%83%E6%90%9C%E5%B0%8B%E6%A8%B9](https://zh.wikipedia.org/wiki/二元搜尋樹)
2. 