1.二叉树的最近公共祖先

```
class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        if root is None or root ==p or root==q:return root 
        left=self.lowestCommonAncestor(root.left,p,q)
        right=self.lowestCommonAncestor(root.right,p,q)
        if left is None:return right 
        if right is None:return left
        return root
```

2.从前序与中序遍历序列构造二叉树

```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        def mybuildTree(preorder_left:int,preorder_right:int,inorder_left:int,inorder_right:int):
            if preorder_left>preorder_right:
                return None
            preorder_root=preorder_left
            inorder_root=index[preorder[preorder_root]]
            #先把根节点建立出来
            root=TreeNode(preorder[preorder_root])

            #得到左子树中的节点数目
            size_left_subtree=inorder_root-inorder_left

            #递归构造左子树,并连接到根节点
            root.left=mybuildTree(preorder_left+1,preorder_left+size_left_subtree,inorder_left,inorder_root-1)
            root.right=mybuildTree(preorder_left+size_left_subtree+1,preorder_right,inorder_root+1,inorder_right)
            return root 
        n=len(preorder)
        index={element:i for i,element in enumerate(inorder)}
        return mybuildTree(0,n-1,0,n-1)
```

3.组合

```
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        nums=[i for i in range(1,n+1)]
        res=[]
        def backtrace(nums_b,curr_res,index):
            if len(curr_res)==k:
                res.append(curr_res[:])
                return 
            for i in range(index,n):
                curr_res.append(nums[i])
                backtrace(nums_b[index:],curr_res,i+1)
                curr_res.pop()
        if n==0 or k==0:
            return res
        backtrace(nums,[],0)
        return res
```

4.全排列

```
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        def backtrace(first=0):
            if first==n:
                res.append(nums[:])
            for i in range(first,n):
                nums[first],nums[i]=nums[i],nums[first]
                backtrace(first+1)
                nums[first],nums[i]=nums[i],nums[first]
        n=len(nums)
        res=[]
        backtrace()
        return res
```

5.全排列ii

```
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        self.res=[]
        check=[0 for i in range(len(nums))]

        self.backtrack([],nums,check)
        return self.res

    def backtrack(self,sol,nums,check):
        if len(sol)==len(nums):
            self.res.append(sol)
            return 
        for i in range(len(nums)):
            if check[i]==1:
                continue
            if i>0 and nums[i]==nums[i-1] and check[i-1]==0:
                continue
            check[i]=1
            self.backtrack(sol+[nums[i]],nums,check)
            check[i]=0
```

