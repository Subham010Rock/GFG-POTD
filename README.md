# GFG-POTD

## Problem No. 1- [K-Ary Tree](https://practice.geeksforgeeks.org/problems/k-ary-tree1235/1)
Find the number of leaf nodes in a full k-ary tree of height m.<br />
Note: You have to return the answer module 10^9+7.

Solution- 
```
class Solution:
    def power(self,k,m):
        if(m==0):
            return 1
        elif(m%2==0):
            y=(self.power(k,m//2))%1000000007
            return y*y
        else:
            return (k*self.power(k,m-1))%1000000007
    def karyTree(self, k, m):
        return (self.power(k,m))%1000000007

if __name__ == '__main__': 
    t = int (input ())
    for _ in range (t):
        k,m=map(int,input().split())
        ob = Solution()
        print(ob.karyTree(k,m))
```
###### T.C=O(log(n))


