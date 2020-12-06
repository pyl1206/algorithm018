爬楼梯

```
class Solution:
    def climbStairs(self, n: int) -> int:
        if n==1 or n== 2: return n
        a,b,temp=1,2,0
        for i in range(3,n+1):
            temp=a+b
            a=b
            b=temp
        return temp
```

实现Trie树

```
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root={}


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node=self.root
        for w in word:
            if w not in node:
                node[w]={}
            node=node[w]
        node['#']='#'


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node=self.root
        for w in word:
            if w not in  node:
                return False
            node=node[w]
        if "#" in node:
            return True
        return False
        
    


    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node=self.root
        for w in prefix:
            if w not in  node:
                return False
            node=node[w]
        return True
            



# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

朋友圈

```
class Solution:
    def findCircleNum(self, M: List[List[int]]) -> int:
        n=len(M)
        count=0
        visited=set()
        def dfs(i):
            for j in range(n):
                if M[i][j] and j not in visited:
                    visited.add(j)
                    dfs(j)
        for i in range(n):
            if i not in visited:
                visited.add(i)
                count+=1
                dfs(i)
        return count

```

岛屿数量

```
class Solution:
    def dfs(self,grid,r,c):
        grid[r][c]=0
        nr,nc=len(grid),len(grid[0])
        for x,y in [(r,c-1),(r,c+1),(r-1,c),(r+1,c)]:
            if 0<=x<nr and 0<=y<nc and grid[x][y]=="1":
                self.dfs(grid,x,y)
    def numIslands(self, grid: List[List[str]]) -> int:
        nr =len(grid)
        if nr==0:
            return 0
        nc=len(grid[0])
        count=0
        for r in range(nr):
            for c in range(nc):
                if grid[r][c]=="1":
                    count+=1
                    self.dfs(grid,r,c)
        return count
```

被围绕的区域

```
class Solution:
 
    def solve(self, board: List[List[str]]) -> None:
        if not board:
            return
        n, m = len(board), len(board[0])

        def dfs(x, y):
            if not 0 <= x < n or not 0 <= y < m or board[x][y] != 'O':
                return
            
            board[x][y] = "A"
            dfs(x + 1, y)
            dfs(x - 1, y)
            dfs(x, y + 1)
            dfs(x, y - 1)

        for i in range(n):
            dfs(i,0)
            dfs(i,m-1)

        for j in range(m):
            dfs(0,j)
            dfs(n-1,j)
            
        for b in range(n):
            for d in range(m):
                if board[b][d]=='A':
                    board[b][d]='O'
                elif board[b][d]=='O':
                    board[b][d]='X' 

    
```

有效的数独

```
class Solution:
    def isValidSudoku(self, board):
        rows = [{} for i in range(9)]
        columns = [{} for i in range(9)]
        boxes = [{} for i in range(9)]

       
        for i in range(9):
            for j in range(9):
                num = board[i][j]
                if num != '.':
                    num = int(num)
                    box_index = (i // 3 ) * 3 + j // 3
                    
                    
                    rows[i][num] = rows[i].get(num, 0) + 1
                    columns[j][num] = columns[j].get(num, 0) + 1
                    boxes[box_index][num] = boxes[box_index].get(num, 0) + 1
                    
                    
                    if rows[i][num] > 1 or columns[j][num] > 1 or boxes[box_index][num] > 1:
                        return False         
        return True


```

括号生成

```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        def generate(A):
            if len(A) == 2*n:
                if valid(A):
                    ans.append("".join(A))
            else:
                A.append('(')
                generate(A)
                A.pop()
                A.append(')')
                generate(A)
                A.pop()

        def valid(A):
            bal = 0
            for c in A:
                if c == '(': bal += 1
                else: bal -= 1
                if bal < 0: return False
            return bal == 0

        ans = []
        generate([])
        return ans

```

