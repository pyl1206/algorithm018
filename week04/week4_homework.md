week4_homework

1.柠檬水找零

```
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        five=ten=0
        for bill in bills:
            if bill==5:
                five+=1
            elif bill==10:
                if not five: return False
                five-=1
                ten+=1
            else:
                if ten and five:
                    five-=1
                    ten-=1
                elif five>=3:
                    five-=3
                else:
                    return False
        return True
```

2.买卖股票的最佳时机II

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        inf=int(1e9)
        minprofit=inf
        maxprofit=0
        for price in prices:
            maxprofit=max(price-minprofit,maxprofit)
            minprofit=min(minprofit,price)
        return maxprofit
```

3.分发饼干

```
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        i=0
        for a in s:
            if i==len(g):
                break
            elif g[i]<=a:
                i+=1
        return i
```

4.模拟行走机器人

```
class Solution:
    def robotSim(self, commands: List[int], obstacles: List[List[int]]) -> int:
        dx,dy,x,y=0,1,0,0
        distance=0
        obs_dict={}
        for obs in obstacles:
            obs_dict[tuple(obs)]=0
        for com in commands:
            if com==-1:
                dx,dy=dy,-dx
            elif com==-2:
                dx,dy=-dy,dx
            else:
                for j in range(com):
                    next_x=x+dx
                    next_y=y+dy
                    if (next_x,next_y) in obs_dict:
                        break
                    x,y=next_x,next_y
                    distance=max(distance,x*x+y*y)
        return distance
```

5.二分查找半有序数组[4,5,6,7,0,1,2]中间无序的地方





6.单词接龙

```
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        def addWord(word: str):
            if word not in wordId:
                nonlocal nodeNum
                wordId[word] = nodeNum
                nodeNum += 1
        
        def addEdge(word: str):
            addWord(word)
            id1 = wordId[word]
            chars = list(word)
            for i in range(len(chars)):
                tmp = chars[i]
                chars[i] = "*"
                newWord = "".join(chars)
                addWord(newWord)
                id2 = wordId[newWord]
                edge[id1].append(id2)
                edge[id2].append(id1)
                chars[i] = tmp

        wordId = dict()
        edge = collections.defaultdict(list)
        nodeNum = 0

        for word in wordList:
            addEdge(word)
        
        addEdge(beginWord)
        if endWord not in wordId:
            return 0
        
        disBegin = [float("inf")] * nodeNum
        beginId = wordId[beginWord]
        disBegin[beginId] = 0
        queBegin = collections.deque([beginId])

        disEnd = [float("inf")] * nodeNum
        endId = wordId[endWord]
        disEnd[endId] = 0
        queEnd = collections.deque([endId])

        while queBegin or queEnd:
            queBeginSize = len(queBegin)
            for _ in range(queBeginSize):
                nodeBegin = queBegin.popleft()
                if disEnd[nodeBegin] != float("inf"):
                    return (disBegin[nodeBegin] + disEnd[nodeBegin]) // 2 + 1
                for it in edge[nodeBegin]:
                    if disBegin[it] == float("inf"):
                        disBegin[it] = disBegin[nodeBegin] + 1
                        queBegin.append(it)

            queEndSize = len(queEnd)
            for _ in range(queEndSize):
                nodeEnd = queEnd.popleft()
                if disBegin[nodeEnd] != float("inf"):
                    return (disBegin[nodeEnd] + disEnd[nodeEnd]) // 2 + 1
                for it in edge[nodeEnd]:
                    if disEnd[it] == float("inf"):
                        disEnd[it] = disEnd[nodeEnd] + 1
                        queEnd.append(it)
        
        return 0


```

7.岛屿数量

```
class Solution:
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
                    grid[r][c] = "0"
                    neighbors = collections.deque([(r, c)])
                    while neighbors:
                        row, col = neighbors.popleft()
                        for x, y in [(row - 1, col), (row + 1, col), (row, col - 1), (row, col + 1)]:
                            if 0 <= x < nr and 0 <= y < nc and grid[x][y] == "1":
                                neighbors.append((x, y))
                                grid[x][y] = "0"
        
        return num_islands

```

8.扫雷游戏



```
class Solution:
        def updateBoard(self, board: List[List[str]], click: List[int]) -> List[List[str]]:
            direction = ((1, 0), (-1, 0), (0, 1), (0, -1), (1, 1), (-1, 1), (-1, -1), (1, -1))
            if board[click[0]][click[1]] == 'M':
                board[click[0]][click[1]] = 'X'
                return board
            self.m,self.n = len(board), len(board[0])
            def check(i, j):
                cnt = 0
                for x,y in direction:
                    x, y = x + i, y + j
                    if 0 <= x < self.m and 0 <= y < self.n and board[x][y]=='M':
                        cnt += 1
                return cnt    
            def dfs(i, j):
                cnt = check(i, j)
                if not cnt:
                    board[i][j] = 'B'
                    for x, y in direction:
                        x, y = x + i, y + j
                        if  0 <= x < self.m and 0 <= y < self.n and board[x][y]=='E': dfs(x, y)
                else: board[i][j] = str(cnt)
            dfs(click[0],click[1])
            return board


```

9.跳跃游戏

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n,rightmost=len(nums),0
        for i in range(n):
            if i <=rightmost:
                rightmost=max(rightmost,i+nums[i])
                if rightmost>n-1:
                    return True
        return False

```

10.搜索旋转排序数组

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1
        l,r=0,len(nums)-1
        while l<=r:
            mid=(l+r)//2
            if nums[mid]==target:
                return mid
            elif nums[0]<=nums[mid]:
                if nums[0]<=target<nums[mid]:
                    r=mid-1
                else:
                    l=mid+1
            else:
                if nums[mid]<target<=nums[len(nums)-1]:
                    l=mid+1
                else:
                    r=mid-1
        return -1

```

11.搜索二维矩阵

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m=len(matrix)
        if m==0:
            return False
        n=len(matrix[0])
        left,right=0,m*n-1
        while left <= right:
            mid=(left+right)//2
            pivot_element=matrix[mid//n][mid%n]
            if pivot_element==target:
                return True
            else:
                if target<pivot_element:
                    right=mid-1
                else:
                    left=mid+1
        return False
        
```





