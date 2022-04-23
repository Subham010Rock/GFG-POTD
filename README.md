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

## Problem No. 3-[Theft at World Bank](https://practice.geeksforgeeks.org/problems/theft-at-the-world-bank2156/1#)
The worlds most successful thief Albert Spaggiari was planning for his next heist on the world bank. He decides to carry a sack with him, which can carry a maximum weight of C kgs. Inside the world bank there were N large blocks of gold. All the blocks have some profit value associated with them i.e. if he steals ith block of weight w[i] then he will have p[i] profit. As blocks were heavy he decided to steal some part of them by cutting them with his cutter.
The thief does not like symmetry, hence, he wishes to not take blocks or parts of them whose weight is a perfect square. Now, you need to find out the maximum profit that he can earn given that he can only carry blocks of gold in his sack. 
Note: The answer should be precise upto 3 decimal places.

Solution- 

```
class Solution{
	public:
	static bool sqr(long long n){
	    if(ceil(sqrt(n))==floor(sqrt(n)))
	    return true;
	    else
	    return false;
	}
	long double maximumProfit(int N, long long C, vector<long long> w, vector<long long> p){
	    // Code here.
	    long double res=0;
	    vector<pair<long double,long long>>v;
	    for(int i=0;i<w.size();i++){
	        if(!sqr(w[i])){
	            v.push_back(make_pair(((long double)p[i]/w[i]),w[i]));
	        }
	    }
	    sort(v.rbegin(),v.rend());
	    for(int i=0;i<v.size();i++){
	        if(C==0)
	        return res;
	        long long m=min(v[i].second,C);
	        res+=m*v[i].first;
	        C-=m;
	    }
	    return res;
	}
};
```

###### T.C: O(N*logN), S.C: O(N)

## Problem No. 4-[Search insert position of K in a sorted array](https://practice.geeksforgeeks.org/problems/search-insert-position-of-k-in-a-sorted-array/1#)
Given a sorted array Arr[](0-index based) consisting of N distinct integers and an integer k, the task is to find the index of k, if it’s present in the array Arr[]. Otherwise, find the index where k must be inserted to keep the array sorted.

Solution-

```
class Solution{
    public:
    int searchInsertK(vector<int>Arr, int N, int k)
    {
        // code here
        int low=0;
        int high=N-1;
        int mid;
        while(low<=high){
            mid=(low+high)/2;
            if(Arr[mid]==k)
            return mid;
            else if(Arr[mid]>k){
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        if(Arr[mid]>k){
            return mid;
        }
        else
        return mid+1;
    }
};
```

###### T.C: O(Log(N)), S.C(O(1))
