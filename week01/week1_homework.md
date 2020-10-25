week1_homework

用add first 或add last 这套新的API改写Deque的代码

不会JAVA语言，把双端队列的源代码默写加注释了一下

```
class Deque(object):
    """双端队列"""
    def __init__(self):
        """创建一个空的队列"""
        self.__list = []

    def add_front(self, elem):
        """往双端对列头部添加一个elem元素"""
        self.__list.insert(0, elem)

    def add_rear(self, elem):
        """往双端队列尾部添加一个elem元素"""
        self.__list.append(elem)

    def pop_front(self):
        """从双端队列头部取出一个元素"""
        if self.is_empty():
            return None
        else:
            return self.__list.pop(0)

    def pop_rear(self):
        """从双端对列尾部取出一个元素"""
        if self.is_empty():
            return None
        else:
            return self.__list.pop()

    def is_empty(self):
        """判断一个队列是否为空"""
        return [] == self.__list

    def size(self):
        """返回队列的大小"""
        return len(self.__list)


if __name__ == '__main__':
    dq = Deque()
    dq.add_front(1)
    dq.add_front(2)
    dq.add_rear(3)
    dq.add_rear(4)
    print(dq.pop_rear())
    print(dq.pop_front())


```

分析Queue和Priority Queue的源码

Priority Queue源码

```
class PriorityQueue(Queue):

    def _init(self, maxsize):

        self.queue = []


    def _qsize(self, len=len):  ###数组长度大小

        return len(self.queue)


    def _put(self, item, heappush=heapq.heappush):#添加元素

        heappush(self.queue, item)


    def _get(self, heappop=heapq.heappop):##查询

     
return heappop(self.queue)
```

Queue的源码部分

```
class Queue():
def _init(self, maxsize):

        self.queue = deque()


    def _qsize(self, len=len):

        return len(self.queue)


    # Put a new item in the queue

    def _put(self, item):

        self.queue.append(item)


    # Get an item from the queue

    def _get(self):

return self.queue.popleft()
```

队列是先进先出，优先队列中是使用heapq来实现的，其中优先队列中的插入的时间复杂度和队列是一样的都是O（1），但是优先队列取出的时间复杂度是log(n),本质上可以认为两者算法本质是一样的

删除排序数组中的重复性

方法一：采用双指针，时间复杂度为O（1）

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        a = 0
        b = 1
        while b < len(nums):
            if nums[a]==nums[b]:
                b +=1
            else:
                a +=1
                nums[a]=nums[b]
        return a+1
```

方法二：

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        a = 0
        b = 1
        while b < len(nums):
            if nums[a]==nums[b]:
                nums.pop(b)
            else:
                a +=1
                b +=1
        return len(nums)
```

旋转数组

方法一：该方法的的时间复杂度为O（n)，但是该方法的运行时间较长

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        if n < 2:
            pass
        else:
            while k >0:
                a = nums[-1]
                nums[1:n] = nums[0:n-1]
                nums[0]=a
                k -=1
            return nums
```

方法二：是采用将数组的最后一个数组插入到数组的第一个位置，循环K次

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        if n < 2:
            pass
        else:
            while k:
                nums.insert(0,nums[-1])
                nums.pop()
                k -=1
```

方法三：这个是自己想的但是没运行出来，希望老师解惑一下。采用的方法是数组中的每个索引i都加上k,然后用（i+k)%n(数组长度n)取余数，作为新数组的索引但是结果有问题

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        if n < 2:
            pass
        else:
            for i in range(n):
                m=i+k
                j = m % n
                nums[j] = num[i]
            return nums
            
 例子是nums=[1,2,3,4,5,6,7] ,k=3
这段代码的结果是[2,3,1,1,2,3,1],这里感觉就没有遍历4之后的位置。请老师帮忙解答一下，谢谢。 
```

合并两个有序数组

方法一：采用双指针，从前向后

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        a=0
        b=0
        nums1_copy=nums1[:m]
        nums1[:]=[]
        while a <m and b < n:
            if nums1_copy[a] <= nums2[b]:
                nums1.append(nums1_copy[a])
                a += 1
            else:
                nums1.append(nums2[b])
                b += 1
        if a < m:
            nums1[a+b:]=nums1_copy[a:]
        if b< n:
            nums1[a+b:]=nums2[b:]
```

方法二：双指针，从后向前

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        p1 = m-1
        p2 = n-1
        p = m+n-1
        while p1 >= 0 and p2 >= 0:
            if nums1[p1] < nums2[p2]:
                nums1[p] = nums2[p2]
                p2 -= 1
            else:
                nums1[p] = nums1[p1]
                p1 -= 1
            p -=1
        nums1[:p2+1] = nums2[:p2+1]

            
```

合并两个有序链表

方法一：使用递归

```
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2
        if not l2: return l1
        if l1.val <= l2.val:
            l1.next = self.mergeTwoLists(l1.next,l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1,l2.next)
            return l2
```

方法二：迭代法

```
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        prehead=ListNode(-1)

        prev=prehead
        while l1 and l2:
            if l1.val <= l2.val:
                prev.next=l1
                l1=l1.next
            else:
                prev.next=l2
                l2=l2.next
            prev=prev.next
        prev.next=l1 if l1 is not None else l2
        return prehead.next
```

两数之和

方法一：暴力法，

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        n=len(nums)
        for i in range(0,n):
            for j in range(i+1,n):
                if nums[i]+nums[j]==target:
                    return [i,j]
        return []
```

方法二：哈希表

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable=dict()
        for i,num in enumerate(nums):
            if target-num in hashtable:
                return (hashtable[target-num],i)
            hashtable[nums[i]] = i
        return []
```

移动零

方法一：暴力法

```
for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i]==0 and nums[j]!=0:
                    nums[i],nums[j]=nums[j],0
        return nums
```

方法二：

```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        for
        """
        count=0
        n=len(nums)
        for i in range(n):
            if nums[i] ==0:
                count +=1
            elif count >0:
                nums[i-count],nums[i]=nums[i],0
        return nums
```

加一

方法一：

```
class Solution:
 def plusOne(self, digits: List[int]) -> List[int]:
        newlst = []
        while digits and digits[-1] == 9:
            digits.pop()
            newlst.append(0)
        if not digits:
            return [1] + newlst
        else:
            digits[-1] += 1
            return digits + newlst
```

方法二：将字符串转化成数字，再加一，然后在将数字转换成字符

```
class Solution:
 def plusOne(self, digits: List[int]) -> List[int]:
        a=[i*10**index for index,i in enumerate(digits[::-1])]
        a=sum(a)+1
        return [int(num) for num in str(a)]
```

设计循环双端队列

```
class MyCircularDeque:

    def __init__(self, k: int):
        self.max_len = k
        self.queue = []

    def insertFront(self, value: int) -> bool:
        """
        Adds an item at the front of Deque. Return true if the operation is successful.
        """
        if len(self.queue) < self.max_len:
            self.queue = self.queue[::-1]  # [::-1]使列表倒序
            self.queue.append(value)
            self.queue = self.queue[::-1]
            return True
        return False

    def insertLast(self, value: int) -> bool:
        """
        Adds an item at the rear of Deque. Return true if the operation is successful.
        """
        if len(self.queue) < self.max_len:
            self.queue.append(value)
            return True
        return False

    def deleteFront(self) -> bool:
        """
        Deletes an item from the front of Deque. Return true if the operation is successful.
        """
        if len(self.queue):
            del self.queue[0]
            return True
        return False

    def deleteLast(self) -> bool:
        """
        Deletes an item from the rear of Deque. Return true if the operation is successful.
        """
        if len(self.queue):
            del self.queue[-1]
            return True
        return False

    def getFront(self) -> int:
        """
        Get the front item from the deque.
        """
        if len(self.queue):
            return self.queue[0]
        return -1

    def getRear(self) -> int:
        """
        Get the last item from the deque.
        """
        if len(self.queue):
            return self.queue[-1]
        return -1

    def isEmpty(self) -> bool:
        """
        Checks whether the circular deque is empty or not.
        """
        return not len(self.queue)

    def isFull(self) -> bool:
        """
        Checks whether the circular deque is full or not.
        """
        return len(self.queue) == self.max_len
```



接雨水

```
class Solution:
    def trap(self, height: List[int]) -> int:
        n=len(height)
        left,right=0,n-1
        SUM,tem,high=0,0,1
        while(left<=right):
            while(left<=right and height[left]<high):
                SUM+=height[left]
                left+=1
            while(right>=left and height[right]<high):
                SUM+=height[right]
                right-=1
            high+=1
            tem+=right-left+1
        return tem-SUM
```

