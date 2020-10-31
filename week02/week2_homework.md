# week2_homework

1.有效的字母异位词

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) !=len(t):
            return False

        count={}
        for char in s:
            if char in count:
                count[char]+=1
            else:
                count[char]=1
        for char in t:
            if char in count:
                count[char]-=1
            else:
                return False
        for value in count.values():
            if value !=0:
                return False

        return True       

```

2.两数之和

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable=dict()
        for i,num in enumerate(nums):
            if target-num in hashtable:
                return (hashtable[target-num],i)
            hashtable[nums[i]]=i
        return []
```

3.N叉树的前序遍历

```

class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        if root is None:
           return []
        stack,output=[root, ],[]
        while stack:
            root=stack.pop()
            output.append(root.val)
            stack.extend(root.children[::-1])
        return output
```

4.字母异位词分组

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dict={}
        for item in strs:
            key=tuple(sorted(item))
            dict[key]=dict.get(key,[])+[item]
        return list(dict.values())


```

5.二叉树的前序遍历

```
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        def preorder(root):
            if root:
                res.append(root.val)
                preorder(root.left)
                preorder(root.right)
        res=list()
        preorder(root)
        return res
        
```

6.二叉树的中序遍历

```
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        stack=[]
        node=root
        res=[]
        if root ==None:
            return res
        while node or stack:
            while node:
                stack.append(node)
                node=node.left
            node=stack.pop()
            res.append(node.val)
            node=node.right
        return res
```

7.N叉树的层序遍历

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        if not root:
            return []
        res=[]
        d=collections.deque()
        d.append(root)
        while d:
            n=len(d)
            tmp=[]
            for i in range(n):
                node=d.popleft()
                tmp.append(node.val)
                if node.children:
                    d.extend(node.children)
            res.append(tmp)
        return res
```

8.丑数

```
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        res=[]
        ls=[1]
        heapq.heapify(ls)
        for _ in range(n):
            cur=heapq.heappop(ls)
            res.append(cur)
            cur1,cur2,cur3=cur*2,cur*3,cur*5
            setls=set(ls)
            setTmp={cur1,cur2,cur3}
            diff=setTmp.difference(setls)
            print(diff)
            if diff:
                for item in diff:
                    heapq.heappush(ls,item)
        return res[-1]
```

9.前K个高频元素

```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        dic=collections.Counter(nums)
        heap,ans=[],[]
        for i in dic:
            heapq.heappush(heap,(-dic[i],i))
        for _ in range(k):
            ans.append(heapq.heappop(heap)[1])
        return ans
```

