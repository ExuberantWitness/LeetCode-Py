# [剑指 Offer II 118. 多余的边](https://leetcode.cn/problems/7LpjUW/)

- 标签：深度优先搜索、广度优先搜索、并查集、图
- 难度：中等

## 题目链接

- [剑指 Offer II 118. 多余的边 - 力扣](https://leetcode.cn/problems/7LpjUW/)

## 题目大意

一个 `n` 个节点的树（节点值为 `1~n`）添加一条边后就形成了图，添加的这条边不属于树中已经存在的边。图的信息记录存储与长度为 `n` 的二维数组 `edges`，`edges[i] = [ai, bi]` 表示图中在 `ai` 和 `bi` 之间存在一条边。

现在给定代表边信息的二维数组 `edges`。

要求：找到一条可以山区的边，使得删除后的剩余部分是一个有着 `n` 个节点的树。如果有多个答案，则返回数组 `edges` 中最后出现的边。

## 解题思路

树可以看做是无环的图，这道题就是要找出那条添加边之后成环的边。可以考虑用并查集来做。

从前向后遍历每一条边，如果边的两个节点不在同一个集合，就加入到一个集合（链接到同一个根节点）。如果边的节点已经出现在同一个集合里，说明边的两个节点已经连在一起了，再加入这条边一定会出现环，则这条边就是所求答案。

## 代码

```python
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:


        
        n = len(edges)  # n 是边的数量，实际上也是节点数量的上限


        # 初始化并查集，parent[i] 表示节点 i 的父节点，初始时每个节点的父节点都是自己
        # 这里就是直接基于n生成一个列表
        parent = list(range(n + 1))  # 从 1 到 n 的节点，所以大小为 n+1


        # 查找操作，找到节点所在集合的根节点
        def find(index: int) -> int:
            if parent[index] != index:
                # 路径压缩，递归查找父节点并将其直接指向根节点
                parent[index] = find(parent[index])
            return parent[index]
        
        # 合并操作，将两个节点所在集合合并
        def union(index1: int, index2: int):
            parent[find(index1)] = find(index2)

        # 遍历所有的边
        for node1, node2 in edges:
            # 如果 node1 和 node2 已经在同一个连通分量中，则添加的边形成了环，返回这条边
            if find(node1) != find(node2):
                # 如果不在同一个集合，进行合并
                union(node1, node2)
            else:
                # 如果已经在同一集合，说明形成了环，返回当前这条边
                return [node1, node2]
        
        return []

"""
这个图本质是找环

1，先生成一个直接的节点


"""
```

