---
layout: post
title: Algorithm
subtitle: Algorithm class
comments: true
cover-img: /assets/img/007/007-3.jpg
thumbnail-img: ""
# share-img: /assets/img/007/007-3.jpg

---

## 算法

求岛屿的最大面积 BFS

```python
# BFS
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:

        # island area
        max_res = 0

        # row col
        row = len(grid)
        col = len(grid[0])

        # one position
        pos_one = []
        for i in range(row):
            for j in range(col):
                if grid[i][j]==1:
                    pos_one.append((i,j))
                    
        # 防止重复计算1
        hash_set = set()

        # all zeros
        if len(pos_one)==0:
            return 0
        
        # find area
        for i,j in pos_one:

             if (i,j) in hash_set:
                continue

             # 以此为起点进行广度优先搜索
             que = collections.deque()
             que.append((i,j))
             tmp_res = 0

             while que:
                point = que.popleft()
                if point in hash_set:
                    continue
                tmp_res+=1

                hash_set.add(point)
               
                # 判断点是否是满足条件
                for ni,nj in [(point[0]+1,point[1]),(point[0]-1,point[1]),(point[0],point[1]+1),(point[0],point[1]-1)]:
                    if 0<=ni<row and 0<=nj<col and grid[ni][nj]==1 and (ni,nj) not in hash_set:
                        que.append((ni,nj))
                max_res = max(tmp_res,max_res)
        return max_res
```

## DFS

```python
# DFS
class Solution:
    def dfs(self, grid, cur_i, cur_j) -> int:
        if cur_i < 0 or cur_j < 0 or cur_i == len(grid) or cur_j == len(grid[0]) or grid[cur_i][cur_j] != 1:
            return 0
        grid[cur_i][cur_j] = 0
        ans = 1
        for di, dj in [[0, 1], [0, -1], [1, 0], [-1, 0]]:
            next_i, next_j = cur_i + di, cur_j + dj
            ans += self.dfs(grid, next_i, next_j)
        return ans

    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        ans = 0
        for i, l in enumerate(grid):
            for j, n in enumerate(l):
                ans = max(self.dfs(grid, i, j), ans)
        return ans

```

岛屿数量

```python
class Solution:
    def dfs(self, grid, r, c):
        grid[r][c] = 0
        nr, nc = len(grid), len(grid[0])
        for x, y in [(r - 1, c), (r + 1, c), (r, c - 1), (r, c + 1)]:
            if 0 <= x < nr and 0 <= y < nc and grid[x][y] == "1":
                self.dfs(grid, x, y)

    def numIslands(self, grid: List[List[str]]) -> int:
        nr = len(grid)
        if nr == 0:
            return 0
        nc = len(grid[0])

        num_islands = 0
        for r in range(nr):
            for c in range(nc):
                if grid[r][c] == "1":
                    num_islands += 1
                    self.dfs(grid, r, c)
        
        return num_islands
```

子集

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:

        # 递归实现子类枚举
        res = []
        length = len(nums)
        tmp_res = []
        
        def dfs(ids,tmp_res):
            res.append(tmp_res)
            for i in range(ids,length):
                dfs(i+1,tmp_res+[nums[i]])
        
        dfs(0,tmp_res)
        return res
```

二叉树的前序遍历

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        def preorder(root: TreeNode):
            if not root:
                return
            res.append(root.val)
            preorder(root.left)
            preorder(root.right)
        
        res = list()
        preorder(root)
        return res
```

是否是平衡二叉树

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        
        # 是否是平衡二叉树 任意节点的深度相差不超过1

        def dfs(node):
            if not node:
                return 0
            return max(dfs(node.left),dfs(node.right))+1

        # kong is True
        if not root:
            return True
            
        res = abs(dfs(root.left)-dfs(root.right))<=1 and self.isBalanced(root.left) and self.isBalanced(root.right)
        return res
      
```

是否是对称二叉树

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution(object):
	def isSymmetric(self, root):
		"""
		:type root: TreeNode
		:rtype: bool
		"""
		if not root:
			return True
		def dfs(left,right):
			# 递归的终止条件是两个节点都为空
			# 或者两个节点中有一个为空
			# 或者两个节点的值不相等
			if left== None and right == None:
				return True
			if left is None or right is None:
				return False

			if left.val!=right.val:
				return False
			return dfs(left.left,right.right) and dfs(left.right,right.left)
		# 用递归函数，比较左节点，右节点
		return dfs(root.left,root.right)
```



字典树

```python
import collections
class Trie:
    def __init__(self):
        self.child = collections.defaultdict(dict)

    def insert(self, word: str) -> None:
        now_node = self.child

        for s in word:
            if s not in now_node.keys():
                now_node[s] = collections.defaultdict(dict) # create the next node
            now_node = now_node[s]
        now_node['#'] = '#'

    def search(self, word: str) -> bool:

        now_node = self.child
        for s in word:
            if s in now_node.keys():
                now_node = now_node[s]
            else:
                return False
        return '#' in now_node.keys()

    def startsWith(self, prefix: str) -> bool:
        now_node = self.child
        for s in prefix:
            if s in now_node.keys():
                now_node = now_node[s]
            else:
                return False
        return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```



## DP

打家劫舍

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # nums 为空
        if not nums:
            return 0

        # nums
        size = len(nums)
        if size == 1:
            return nums[0]
        # dp init
        # dp 转移方程
        # dp[i] = max(dp[i-2]+ nums[i],dp[i-1])

        dp = [0] * size
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        # dp inference
        for i in range(2, size):
            dp[i] = max(dp[i - 2] + nums[i], dp[i - 1])

        return dp[size - 1]
```



## 贪心

#### [2038. 如果相邻两个颜色均相同则删除当前颜色](https://leetcode-cn.com/problems/remove-colored-pieces-if-both-neighbors-are-the-same-color/)  

总共有 n 个颜色片段排成一列，每个颜色片段要么是 'A' 要么是 'B' 。给你一个长度为 n 的字符串 colors ，其中 colors[i] 表示第 i 个颜色片段的颜色。

Alice 和 Bob 在玩一个游戏，他们 轮流 从这个字符串中删除颜色。Alice 先手 。

如果一个颜色片段为 'A' 且 相邻两个颜色 都是颜色 'A' ，那么 Alice 可以删除该颜色片段。Alice 不可以 删除任何颜色 'B' 片段。
如果一个颜色片段为 'B' 且 相邻两个颜色 都是颜色 'B' ，那么 Bob 可以删除该颜色片段。Bob 不可以 删除任何颜色 'A' 片段。
Alice 和 Bob 不能 从字符串两端删除颜色片段。
如果其中一人无法继续操作，则该玩家 输 掉游戏且另一玩家 获胜 。

假设 Alice 和 Bob 都采用最优策略，如果 Alice 获胜，请返回 `true`，否则 Bob 获胜，返回 `false`。

```python
class Solution:
    def winnerOfGame(self, colors: str) -> bool:
        freq = [0, 0]
        cur, cnt = 'C', 0
        for c in colors:
            if c != cur:
                cur = c
                cnt = 1
            else:
                cnt += 1
                if cnt >= 3:
                    freq[ord(cur) - ord('A')] += 1
        return freq[0] > freq[1]

```



## 双指针

#### [986. 区间列表的交集](https://leetcode-cn.com/problems/interval-list-intersections/)  

```python
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
    
        res = []
        p1 = 0
        p2 = 0

        while p1<len(firstList) and p2<len(secondList):
            sta1,end1 = firstList[p1][0],firstList[p1][1]
            sta2,end2 = secondList[p2][0],secondList[p2][1]
            start,end = max(sta1,sta2),min(end1,end2)
            if start<=end:
                res.append([start,end])
            if end1 < end2:
                p1+=1
            else:
                p2+=1

        return res
```



#### [82. 删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)  

给定一个已排序的链表的头 `head` ， *删除原始链表中所有重复数字的节点，只留下不同的数字* 。返回 *已排序的链表* 。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head:
            return head
        
        dummy = ListNode(0, head)

        cur = dummy

        while cur.next and cur.next.next:
            if cur.next.val == cur.next.next.val:
                x = cur.next.val
                while cur.next and cur.next.val == x:
                    cur.next = cur.next.next
            else:
                cur = cur.next

        return dummy.next
```



## 滑动窗口

#### [713. 乘积小于K的子数组](https://leetcode-cn.com/problems/subarray-product-less-than-k/)  

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:

        # 从左到右 left right
        # if res > k : left+1 else : right+1

        if k <= 1: return 0
        left, right, multi, ans = 0, 0, 1, 0

        while right < len(nums):

            multi *= nums[right] # 以右侧元素为pivot

            while multi >= k: # 找到对应这个pivot的最长窗口左侧点
                multi //= nums[left]
                left += 1

            ans += right - left + 1 # 统计以pivot为右侧元素的子数组
            right += 1

        return ans
```



#### [209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)  

```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:

        # 滑动窗口
        left,right = 0,0
        length = len(nums)       

        if max(nums)>=target:
            return 1
        if sum(nums)<target:
            return 0
        
        res = 0xffffffff
        tmp_sum = nums[0]

        if nums[0]>=target:
            return 1

        while left<length and right<length and left <= right:
            print(left,right,tmp_sum)

            # if sum > tar left+=1
            if tmp_sum>=target:
                res = min(res,right-left+1)
                tmp_sum-=nums[left]
                left+=1
            else:
                right+=1
                if right <len(nums):
                    tmp_sum+=nums[right]
                # res = min(res,right-left+1)
        return res
```

