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

## Problem No. 5-[Sum of two numbers without using arithmetic operators](https://practice.geeksforgeeks.org/problems/sum-of-two-numbers-without-using-arithmetic-operators/1)
Given two integers a and b. Find the sum of two numbers without using arithmetic operators.

Solution-

```
int Add(int x, int y)
{
    // Iterate till there is no carry
    while (y != 0)
    {
        // carry should be unsigned to
        // deal with -ve numbers
        // carry now contains common
        //set bits of x and y
        unsigned carry = x & y;
 
        // Sum of bits of x and y where at
        //least one of the bits is not set
        x = x ^ y;
 
        // Carry is shifted by one so that adding
        // it to x gives the required sum
        y = carry << 1;
    }
    return x;
}
```
###### // This code is contributed by rathbhupendra.
###### T.C:O(Log(y)), S.C:(O(1))

## Problem No. 6-[Product of Primes](https://practice.geeksforgeeks.org/problems/product-of-primes5328/1)
Given two numbers L and R (inclusive) find the product of primes within this range. Print the product modulo 109+7. If there are no primes in that range you must print 1.

Solution- 

```
class Solution{
public:
    bool prime_check(long long n){

        for(int i=2;i*i<=n;i++){
            if(n%i==0)
            return 0;
        }
        return 1;
    }
    long long primeProduct(long long L, long long R){
        // code here
        long long res=1;
        for(long long i=L;i<=R;i++){
            if(prime_check(i))
            res=(res*i)%1000000007;
        }
        return res;
    }
};
```

## Problem No. 7-[Killing Spree](https://practice.geeksforgeeks.org/problems/killing-spree3020/1#)
There are Infinite People Standing in a row, indexed from 1.A person having index 'i' has strength of (i*i). You have Strength 'P'. You need to tell what is the maximum number of People You can Kill With your Strength P. You can only Kill a person with strength 'X' if P >= 'X'  and after killing him, Your Strength decreases by 'X'. 

Solution-

```
class Solution {
public:
    long long int killinSpree(long long int n)
    {
        // Code Here
        long long count=0;
        long long i=1;
        while((i*(i+1)*(2*i+1))/6 <= n){
            count++;
            i++;
        }
        return count;
    }
};
```

## Problem No. 8-[Shop in Candy Store](https://practice.geeksforgeeks.org/problems/shop-in-candy-store1145/1#)
In a candy store, there are N different types of candies available and the prices of all the N different types of candies are provided to you. You are now provided with an attractive offer. You can buy a single candy from the store and get at most K other candies ( all are different types ) for free. Now you have to answer two questions. Firstly, you have to find what is the minimum amount of money you have to spend to buy all the N different candies. Secondly, you have to find what is the maximum amount of money you have to spend to buy all the N different candies. In both the cases you must utilize the offer i.e. you buy one candy and get K other candies for free.

Solution-

```
class Solution
{
public:
    vector<int> candyStore(int candies[], int N, int K)
    {
        // Write Your Code here
        sort(candies,candies+N);
        int f=N;
        int b=0;
        int minimum=0,maximum=0;
        for(int i=0;i<f;i++){
           minimum+=candies[i];
           f=f-K;
        }
        for(int i=N-1;i>=b;i--){
            maximum+=candies[i];
            b+=K;
        }
        vector<int>res={minimum,maximum};
        return res;
    }
};
```
###### T.C: O(NLog(N))

## Problem No. 9-[Find length of Loop](https://practice.geeksforgeeks.org/problems/find-length-of-loop/1#)
Given a linked list of size N. The task is to complete the function countNodesinLoop() that checks whether a given Linked List contains a loop or not and if the loop is present then return the count of nodes in a loop or else return 0. C is the position of the node to which the last node is connected. If it is 0 then no loop.

![image](https://user-images.githubusercontent.com/54362906/165839043-0c95ad4e-a692-4392-b527-d514f9a8e025.png)


Solution-

```
// { Driver Code Starts
// driver code

#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    Node* next;
    
    Node(int val)
    {
        data = val;
        next = NULL;
    }
};

void loopHere(Node* head, Node* tail, int position)
{
    if(position==0) return;
    
    Node* walk = head;
    for(int i=1; i<position; i++)
        walk = walk->next;
    tail->next = walk;
}

int countNodesinLoop(Node* head);

int main()
{
    int t;
    cin>>t;
    while(t--)
    {
        int n, num;
        cin>>n;
        
        Node *head, *tail;
        cin>> num;
        head = tail = new Node(num);
        
        for(int i=0 ; i<n-1 ; i++)
        {
            cin>> num;
            tail->next = new Node(num);
            tail = tail->next;
        }
        
        int pos;
        cin>> pos;
        loopHere(head,tail,pos);
        
        cout<< countNodesinLoop(head) << endl;
    }
	return 0;
}
// } Driver Code Ends


/*

struct Node {
    int data;
    struct Node *next;
    Node(int x) {
        data = x;
        next = NULL;
    }
};

*/

//Function to find the length of a loop in the linked list.
int countNodesinLoop(struct Node *head)
{
    // Code here
    struct Node*slow,*fast;
    slow=fast=head;
    while(fast!=NULL and fast->next!=NULL){
        slow=slow->next;
        fast=fast->next->next;
        if(fast==slow){
            int c=1;
            slow=slow->next;
            while(slow!=fast){
                c++;
                slow=slow->next;
            }
            return c;
        }
    }
    return 0;
    
}

```

## Problem No. 10-[Queries on Strings](https://practice.geeksforgeeks.org/problems/queries-on-strings5636/1)
Given a string str you have to answer several queries on that string. In each query you will be provided two values L and R and you have to find the number of distinct characters in the sub string from index L to index R (inclusive) of the original string.

Solution-
```
class Solution:
    def SolveQueris(self, str, Query):
        # Code here
        res=[]
        for i,j in Query:
            res.append(len(set(str[i-1:j])))
        return res
```
