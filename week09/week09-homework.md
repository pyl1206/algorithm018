字符串的第一个唯一字符

```
class Solution:
    def firstUniqChar(self, s: str) -> int:
        count=collections.Counter(s)
        for idx,s1 in enumerate(s):
            if count[s1]==1:
                return idx
        return -1
```

反转字符串ii

```
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        L1=list(s)
        for i in range(0,len(L1),2*k):
            L1[i:i+k]=reversed(L1[i:i+k])
        return "".join(L1)
```

翻转字符串里的单词

```
class Solution:
    def reverseWords(self, s: str) -> str:
       return " ".join(reversed(s.split()))
```

反转字符串中的单词III

```
class Solution:
    def reverseWords(self, s: str) -> str:
        return " ".join(word[::-1] for word in s.split())
```

仅仅反转字母

```
class Solution:
    def reverseOnlyLetters(self, S: str) -> str:
        letters=[c  for c in S if  c.isalpha()]
        ans=[]
        for c in S:
            if c.isalpha():
                ans.append(letters.pop())
            else:
                ans.append(c)
        return "".join(ans)
```

验证回文字符串II

```
class Solution:
    def validPalindrome(self, s: str) -> bool:
        isPalindrom=lambda x : x==x[::-1]
        left,right=0,len(s)-1
        while left <right:
            if s[left]==s[right]:
                left+=1
                right-=1
            else:
                return isPalindrom(s[left+1:right+1]) or isPalindrom(s[left:right])
        return True
```

最长上升子序列

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        d=[]
        for n in nums:
            if not d or n>d[-1]:
                d.append(n)
            else:
                l,r=0,len(d)-1
                loc=r
                while l<=r:
                    mid=(l+r)//2
                    if d[mid]>=n:
                        loc=mid
                        r=mid-1
                    else:
                        l=mid+1
                d[loc]=n
        return len(d)
```

解码方法

```
class Solution:
    def numDecodings(self, s: str) -> int:
        if s.startswith('0'):
            return 0
        n=len(s)
        dp=[1]*(n+1)
        for i in range(2,n+1):
            if s[i-1]=='0' and s[i-2] not in '12':
                return 0
            if s[i-2:i] in ['10','20']:
                dp[i]=dp[i-2]
            elif '10'<s[i-2:i]<='26':
                dp[i]=dp[i-1]+dp[i-2]
            else:
                dp[i]=dp[i-1]
        return dp[n]
```

找到字符串中所有字母异位词

```
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        res=[]
        n=len(s)
        m=len(p)
        p="".join(sorted(p))
        for i in range(n-m+1):
            if "".join(sorted(s[i:i+m]))==p:
                res.append(i)
        return res
```