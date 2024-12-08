# [剑指 Offer II 105. 岛屿的最大面积](https://leetcode.cn/problems/ZL6zAn/)

- 标签：深度优先搜索、广度优先搜索、并查集、数组、矩阵
- 难度：中等

## 题目链接

- [剑指 Offer II 105. 岛屿的最大面积 - 力扣](https://leetcode.cn/problems/ZL6zAn/)

## 题目大意

给定一个只包含 `0`、`1` 元素的二维数组，`1` 代表岛屿，`0` 代表水。一座岛的面积就是上下左右相邻相邻的 `1` 所组成的连通块的数目。找到最大的岛屿面积。

## 解题思路

使用深度优先搜索方法。遍历二维数组的每一个元素，对于每个值为 `1` 的元素，记下其面积。然后将该值置为 `0`（防止二次重复计算），再递归其上下左右四个位置，并将深度优先搜索搜到的值为 `1` 的元素个数，进行累积统计。

## 代码

```python
class Solution:
    def dfs(self, grid, i, j):
        size_n = len(grid)
        size_m = len(grid[0])
        if i < 0 or i >= size_n or j < 0 or j >= size_m or grid[i][j] == 0:
            return 0
        ans = 1
        grid[i][j] = 0
        ans += self.dfs(grid, i + 1, j)
        ans += self.dfs(grid, i, j + 1)
        ans += self.dfs(grid, i - 1, j)
        ans += self.dfs(grid, i, j - 1)
        return ans

    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        ans = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1:
                    ans = max(ans, self.dfs(grid, i, j))
        return ans
```
相当于是随机出现的多个树的叠加过程，下面进一步介绍dfs

```python
def dfs(graph,node,visited=None):
    if visited is None:
        visited = set()
    visited.add(node) # 管理是否已经经历过了
    print(node) # 对节点过程进行操作
    for neighbor in graph[node]:  # 保证回溯能力
        if neighbor not in visited: 
            dfs(graph,neighbor,visited) # 保证继续挖的能力


# 示例图
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B'],
    'F': ['C']
}

dfs(graph, 'A')
```





