# [剑指 Offer II 111. 计算除法](https://leetcode.cn/problems/vlzXQL/)

- 标签：深度优先搜索、广度优先搜索、并查集、图、数组、最短路
- 难度：中等

## 题目链接

- [剑指 Offer II 111. 计算除法 - 力扣](https://leetcode.cn/problems/vlzXQL/)

## 题目大意

给定一个变量对数组 `equations` 和一个实数数组 `values` 作为已知条件，其中 `equations[i] = [Ai, Bi]`  和 `values[i]` 共同表示 `Ai / Bi = values[i]`。每个 `Ai` 或 `Bi` 是一个表示单个变量的字符串。

再给定一个表示多个问题的数组 `queries`，其中 `queries[j] = [Cj, Dj]` 表示第 `j` 个问题，要求：根据已知条件找出 `Cj / Dj = ?` 的结果作为答案。返回所有问题的答案。如果某个答案无法确定，则用 `-1.0` 代替，如果问题中出现了给定的已知条件中没有出现的表示变量的字符串，则也用 `-1.0` 代替这个答案。

## 解题思路

在「[等式方程的可满足性](https://leetcode.cn/problems/satisfiability-of-equality-equations)」的基础上增加了倍数关系。在「[等式方程的可满足性](https://leetcode.cn/problems/satisfiability-of-equality-equations)」中我们处理传递关系使用了并查集，这道题也是一样，不过在使用并查集的同时还要维护倍数关系。

举例说明：

- `a / b = 2.0`：说明 `a = 2b`，`a` 和 `b` 在同一个集合。
- `b / c = 3.0`：说明 `b = 3c`，`b`  和 `c`  在同一个集合。

根据上述两式可得：`a`、`b`、`c` 都在一个集合中，且 `a = 2b = 6c`。

我们可以将同一集合中的变量倍数关系都转换为与根节点变量的倍数关系，比如上述例子中都转变为与 `a` 的倍数关系。

具体操作如下：

- 定义并查集结构，并在并查集中定义一个表示倍数关系的 `multiples` 数组。
- 遍历 `equations` 数组、`values` 数组，将每个变量按顺序编号，并使用 `union` 将其并入相同集合。
- 遍历 `queries` 数组，判断两个变量是否在并查集中，并且是否在同一集合。如果找到对应关系，则将计算后的倍数关系存入答案数组，否则则将 `-1` 存入答案数组。
- 最终输出答案数组。

并查集中维护倍数相关方法说明：

- `find` 方法： 
    - 递推寻找根节点，并将倍数累乘，然后进行路径压缩，并且更新当前节点的倍数关系。
- `union` 方法：
    - 如果两个节点属于同一集合，则直接返回。
    - 如果两个节点不属于同一个集合，合并之前当前节点的倍数关系更新，然后再进行更新。
- `is_connect` 方法：
    - 如果两个节点不属于同一集合，返回 `-1`。
    - 如果两个节点属于同一集合，则返回倍数关系。

## 代码

```python
# [剑指 Offer II 111. 计算除法](https://leetcode.cn/problems/vlzXQL/)

- 标签：深度优先搜索、广度优先搜索、并查集、图、数组、最短路
- 难度：中等

## 题目链接

- [剑指 Offer II 111. 计算除法 - 力扣](https://leetcode.cn/problems/vlzXQL/)

## 题目大意

给定一个变量对数组 `equations` 和一个实数数组 `values` 作为已知条件，其中 `equations[i] = [Ai, Bi]`  和 `values[i]` 共同表示 `Ai / Bi = values[i]`。每个 `Ai` 或 `Bi` 是一个表示单个变量的字符串。

再给定一个表示多个问题的数组 `queries`，其中 `queries[j] = [Cj, Dj]` 表示第 `j` 个问题，要求：根据已知条件找出 `Cj / Dj = ?` 的结果作为答案。返回所有问题的答案。如果某个答案无法确定，则用 `-1.0` 代替，如果问题中出现了给定的已知条件中没有出现的表示变量的字符串，则也用 `-1.0` 代替这个答案。

## 解题思路

在「[等式方程的可满足性](https://leetcode.cn/problems/satisfiability-of-equality-equations)」的基础上增加了倍数关系。在「[等式方程的可满足性](https://leetcode.cn/problems/satisfiability-of-equality-equations)」中我们处理传递关系使用了并查集，这道题也是一样，不过在使用并查集的同时还要维护倍数关系。

举例说明：

- `a / b = 2.0`：说明 `a = 2b`，`a` 和 `b` 在同一个集合。
- `b / c = 3.0`：说明 `b = 3c`，`b`  和 `c`  在同一个集合。

根据上述两式可得：`a`、`b`、`c` 都在一个集合中，且 `a = 2b = 6c`。

我们可以将同一集合中的变量倍数关系都转换为与根节点变量的倍数关系，比如上述例子中都转变为与 `a` 的倍数关系。

具体操作如下：

- 定义并查集结构，并在并查集中定义一个表示倍数关系的 `multiples` 数组。
- 遍历 `equations` 数组、`values` 数组，将每个变量按顺序编号，并使用 `union` 将其并入相同集合。
- 遍历 `queries` 数组，判断两个变量是否在并查集中，并且是否在同一集合。如果找到对应关系，则将计算后的倍数关系存入答案数组，否则则将 `-1` 存入答案数组。
- 最终输出答案数组。

并查集中维护倍数相关方法说明：

- `find` 方法： 
    - 递推寻找根节点，并将倍数累乘，然后进行路径压缩，并且更新当前节点的倍数关系。
- `union` 方法：
    - 如果两个节点属于同一集合，则直接返回。
    - 如果两个节点不属于同一个集合，合并之前当前节点的倍数关系更新，然后再进行更新。
- `is_connect` 方法：
    - 如果两个节点不属于同一集合，返回 `-1`。
    - 如果两个节点属于同一集合，则返回倍数关系。

## 代码

```python
from collections import defaultdict
class Solution:
    def calcEquation(self, equations, values, queries):
        # 构图：使用 defaultdict 来构建一个图，图的每个节点是一个变量，边的权重是该变量之间的比值
        graph = defaultdict(dict)

        # 遍历每个等式和对应的值，构建图
        for (a, b), value in zip(equations, values):
            graph[a][b] = value
            graph[b][a] = 1 / value


        # 定义深度优先搜索（DFS）函数来找路径
        def dfs(start,end,visited):
            # 如果 start 或者 end 不在图中，说明无法找到路径，返回 -1.0
            if start not in graph or end not in graph:
                return -1.0


            # 如果 start 和 end 相同，说明路径长度为 1.0，直接返回
            if start==end:
                return 1.0


            # 标记当前节点为已访问，避免重复访问同一个节点
            visited.add(start)

            # 遍历从 start 出发的所有边（即 start 连接到其他节点的所有比值）
            for i,value in graph[start].items():
                # 如果 i 还没有被访问过，继续递归查找路径
                if i not in visited:
                    # 递归查找从 i 到 end 的路径，并计算路径的比值
                    path_value = dfs(i,end,visited)

                    # 如果找到了有效路径，返回当前边的比值乘以路径的比值
                    if path_value!=-1.0:
                        return value*path_value


            # 如果没有找到路径，返回 -1.0
            return -1.0

        # 用来存储查询结果的列表
        res=[]

        # 遍历所有的查询，使用 DFS 查找每一对查询的比值
        for start,end in queries:
            # 对每个查询调用 DFS，查询 start 和 end 之间的比值
            res.append(dfs(start,end,set()))
        return res


"""
"""

```

