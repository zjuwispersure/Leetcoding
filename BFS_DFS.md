[BFS_DFS](https://cuijiahua.com/blog/2018/01/alogrithm_10.html)



## 一、前言

我们首次接触 [BFS](https://cuijiahua.com/blog/tag/bfs/) 和 DFS 时，应该是在数据结构课上讲的 “图的遍历”。还有就是刷题的时候，遍历二叉树我们会经常用到[BFS](https://cuijiahua.com/blog/tag/bfs/)和DFS。

本篇文章就单纯来讲讲它们的区别和各自的应用，不会涉及任何代码。我们以“图的遍历”为例，进行说明。

## 二、区别

**广度优先搜索算法（Breadth-First-Search，缩写为 BFS）**，是一种利用**队列**实现的搜索算法。简单来说，其搜索过程和 “湖面丢进一块石头激起层层涟漪” 类似。

**深度优先搜索算法（Depth-First-Search，缩写为 DFS）**，是一种利用**递归**实现的搜索算法。简单来说，其搜索过程和 “不撞南墙不回头” 类似。

**BFS 的重点在于队列，而 DFS 的重点在于递归。这是它们的本质区别。**

举个典型例子，如下图，灰色代表墙壁，绿色代表起点，红色代表终点，规定每次只能走一步，且只能往下或右走。求一条绿色到红色的最短路径。

[![算法基础：BFS和DFS的直观解释](https://cuijiahua.com/wp-content/uploads/2018/01/alogrithm_10_1.png)](https://cuijiahua.com/wp-content/uploads/2018/01/alogrithm_10_1.png)

对于上面的问题，BFS 和 DFS 都可以求出结果，它们的区别就是在复杂度上存在差异。我可以先告诉你，该题 BFS 是较佳算法。

**BFS示意图：**

[![算法基础：BFS和DFS的直观解释](https://cuijiahua.com/wp-content/uploads/2018/01/alogrithm_10_2.gif)](https://cuijiahua.com/wp-content/uploads/2018/01/alogrithm_10_2.gif)

如上图所示，从起点出发，对于每次出队列的点，都要遍历其四周的点。所以说 BFS 的搜索过程和 “湖面丢进一块石头激起层层涟漪” 很相似，此即 “广度优先搜索算法” 中“广度”的由来。

**DFS示意图：**

[![算法基础：BFS和DFS的直观解释](https://cuijiahua.com/wp-content/uploads/2018/01/alogrithm_10_3.gif)](https://cuijiahua.com/wp-content/uploads/2018/01/alogrithm_10_3.gif)

如上图所示，从起点出发，先把一个方向的点都遍历完才会改变方向...... 所以说，DFS 的搜索过程和 “不撞南墙不回头” 很相似，此即 “深度优先搜索算法” 中“深度”的由来。