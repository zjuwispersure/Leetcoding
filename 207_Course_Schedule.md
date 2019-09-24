[题目介绍](https://leetcode.com/problems/course-schedule/)

There are a total of *n* courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

**Example 1:**

```
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.



### 解法

本质是有向图查看是否有环。

输入的图是用list来表示边，改为用list表示的邻接矩阵形式。

使用拓扑排序来处理。



```
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses, vector<int>());
        vector<int> degree(numCourses, 0);
        for (vector<int> p: prerequisites) {
            adj[p[0]].push_back(p[1]);
            degree[p[1]]++;
        }
        queue<int> q;
        for (int i = 0; i < numCourses; i++){
            if (degree[i] == 0) q.push(i);
        }
        while (!q.empty()) {
            int curr = q.front(); q.pop(); numCourses--;
            for (auto next: adj[curr]){
                if (--degree[next] == 0) {
                    q.push(next);
                }
            }
        }
        return numCourses == 0;
    }
};
```



