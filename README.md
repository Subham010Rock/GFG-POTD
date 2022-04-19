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
###### T.C=O(log(n))<br />

## Problem No. 2- [Partition a Linked List around a given value](https://practice.geeksforgeeks.org/problems/partition-a-linked-list-around-a-given-value/1#)
Given a linked list and a value x, partition it such that all nodes less than x come first, then all nodes with value equal to x and finally nodes with value greater than or equal to x. The original relative order of the nodes in each of the three partitions should be preserved. The partition must work in-place.

Solution-

```

struct Node* partition(struct Node* head, int x) {
    // code here
    struct Node* h1,*h2,*h3,*iter1,*iter2,*iter3;
    h1=h2=h3=iter1=iter2=iter3=NULL;
    while(head!=NULL){
        struct Node*temp=new Node(head->data);
        if(head->data<x){
            if(h1==NULL){
                h1=temp;
                iter1=temp;
            }
            else{
                iter1->next=temp;
                iter1=temp;
            }
        }
        else if(head->data==x){
            if(h2==NULL){
                h2=temp;
                iter2=temp;
            }
            else{
                iter2->next=temp;
                iter2=temp;
            }
        }
        else{
            if(h3==NULL){
                h3=temp;
                iter3=temp;
            }
            else{
                iter3->next=temp;
                iter3=temp;
            }
        }
        head=head->next;
    }
    if(h1==NULL){
        if(h2==NULL){
            return h3;
        }
        else{
            if(h3==NULL){
                return h2;
            }
            else{
                iter2->next=h3;
                return h2;
            }
        }
    }
    else{
        if(h2==NULL){
            iter1->next=h3;
            return h1;
        }
        else{
            iter1->next=h2;
            iter2->next=h3;
            return h1;
        }
    }
}
```
###### T.C: O(N), S.C: O(N)


