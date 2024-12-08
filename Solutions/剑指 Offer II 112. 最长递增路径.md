# [剑指 Offer II 112. 最长递增路径](https://leetcode.cn/problems/fpTFWP/)

- 标签：深度优先搜索、广度优先搜索、图、拓扑排序、记忆化搜索、数组、动态规划、矩阵
- 难度：困难

## 题目链接

- [剑指 Offer II 112. 最长递增路径 - 力扣](https://leetcode.cn/problems/fpTFWP/)

## 题目大意

给定一个 `m * n` 大小的整数矩阵 `matrix`。要求：找出其中最长递增路径的长度。

对于每个单元格，可以往上、下、左、右四个方向移动，不能向对角线方向移动或移动到边界外。

## 解题思路

深度优先搜索。使用二维数组 `record` 存储遍历过的单元格最大路径长度，已经遍历过的单元格就不需要再次遍历了。

## 代码

```python
class Solution:
    
    DIRS = [(-1, 0), (1, 0), (0, -1), (0, 1)]

    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:


        # 如果矩阵为空，返回 0
        if not matrix:
            return 0
        
        # 定义一个递归函数来进行深度优先搜索（DFS），并使用 lru_cache 来缓存结果
        @lru_cache(None)  # 使用缓存来优化递归，避免重复计算相同的子问题
        def dfs(row: int, column: int) -> int:
             # 当前路径的最小长度为 1（当前节点本身）
            best = 1
            # 遍历四个方向：上、下、左、右
            for dx, dy in Solution.DIRS:
                # 计算新位置的行列坐标
                newRow, newColumn = row + dx, column + dy
                # 检查新位置是否在矩阵范围内，并且新位置的值大于当前节点的值
                if 0 <= newRow < rows and 0 <= newColumn < columns and matrix[newRow][newColumn] > matrix[row][column]:
                    # 如果条件满足，递归地计算从新位置开始的最长递增路径，并更新 best
                    best = max(best, dfs(newRow, newColumn) + 1)
            
            # 返回当前节点的最长递增路径长度
            return best

        # 初始化答案为 0
        ans = 0
         # 获取矩阵的行数和列数
        rows, columns = len(matrix), len(matrix[0])

        # 遍历矩阵的每个节点，计算每个节点作为起点的最长递增路径
        for i in range(rows):
            for j in range(columns):
                # 更新答案，取当前节点的最长递增路径和已找到的最长路径的最大值
                ans = max(ans, dfs(i, j))
        return ans

```

