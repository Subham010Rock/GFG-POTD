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

## Problem No. 11-[Super Primes](https://practice.geeksforgeeks.org/problems/super-primes2443/1#)
A prime number is Super Prime if it is a sum of two primes. Find all the Super Primes upto N

Solution-
```
class Solution{
public:	
	int superPrimes(int n)
	{
	    // Your code goes here
	    vector<int>v(n+1,1);
	    for(int i=2;i<=sqrt(n);i++){
	        if(v[i]==1){
	            for(int j=i*i;j<=n;j+=i){
	                v[j]=0;
	            }
	        }
	    }
	    int c=0;
	    for(int i=5;i<=n;i+=2){
	        if(v[i]==1){
	        if(v[i-2]==1)
	        c++;}
	    }
	    return c;
	}
};
```

###### T.C: O(NLog(LogN)), S.C: O(N)

## Problem No. 12-[Hungry Pizza Lovers](https://practice.geeksforgeeks.org/problems/hungry-pizza-lovers3148/1#)
Dominos Pizza has hungry customers waiting in the queue. Each unique order is placed by a customer at time x[i], and the order takes y[i] units of time to complete.
You have information on all n orders, Find the order in which all customers will receive their pizza and return it. If two or more orders are completed at the same time then sort them by non-decreasing order number.

Solution-

```
#User function Template for python3

class Solution:
    def permute(self,arr,n):
        l=[(arr[i][0]+arr[i][1],i+1) for i in range(n)]
        l=sorted(l,key=lambda x:x[0])
        res=[j for i,j in l ]
        return res


#{ 
#  Driver Code Starts
#Initial Template for Python 3

    
for _ in range(0,int(input())):
    n = int(input())
    arr = []
    for _ in range(0, n):
        ll = list(map(int, input().strip().split()))
        arr.append(ll)
    obj=Solution()
    ans = obj.permute(arr, n)
    for i in ans:
        print(i)
    



# } Driver Code Ends
```
###### T.C: O(NLogN), S.C: O(N)

## Problem No. 13-[Partition a number into two divisible parts](https://practice.geeksforgeeks.org/problems/partition-a-number-into-two-divisible-parts3605/1)
Given a number (as string) and two integers a and b, divide the string in two non-empty parts such that the first part is divisible by a and the second part is divisible by b. In case multiple answers exist, return the string such that the first non-empty part has minimum length.

Solution-
```
#User function Template for python3
class Solution:
    def stringPartition(ob,S,a,b):
        # Code here
        for i in range(len(S)-1):
            if(int(S[0:i+1])%a==0 and int(S[i+1:])%b==0):
                return S[0:i+1]+" "+S[i+1:]
        return -1
        
                
        


#{ 
#  Driver Code Starts
#Initial Template for Python 3
if __name__ == '__main__': 
    t = int (input ())
    for _ in range (t):
        
        S,a,b=map(str,input().strip().split(" "))
        a=int(a)
        b=int(b)
        ob = Solution()
        print(ob.stringPartition(S,a,b))
# } Driver Code Ends
```

## Problem No. 14-[Merge two sorted linked lists](https://practice.geeksforgeeks.org/problems/merge-two-sorted-linked-lists/1#)
Given two sorted linked lists consisting of N and M nodes respectively. The task is to merge both of the list (in-place) and return head of the merged list.

Solution-
```
// { Driver Code Starts
#include<iostream>
using namespace std;

/* Link list Node */
struct Node
{
    int data;
    struct Node *next;
    
    Node(int x)
    {
        data = x;
        next = NULL;
    }
};

Node* sortedMerge(struct Node* a, struct Node* b);

/* Function to print Nodes in a given linked list */
void printList(struct Node *n)
{
    while (n!=NULL)
    {
        cout << n->data << " ";
        n = n->next;
    }
    cout << endl;
}

/* Driver program to test above function*/
int main()
{
    int t;
    cin>>t;
    while(t--)
    {
        int n,m;
        cin>>n>>m;

        int data;
        cin>>data;
        struct Node *head1 = new Node(data);
        struct Node *tail1 = head1;
        for (int i = 1; i < n; ++i)
        {
            cin>>data;
            tail1->next = new Node(data);
            tail1 = tail1->next;
        }

        cin>>data;
        struct Node *head2 = new Node(data);
        struct Node *tail2 = head2;
        for(int i=1; i<m; i++)
        {
            cin>>data;
            tail2->next = new Node(data);
            tail2 = tail2->next;
        }

        Node *head = sortedMerge(head1, head2);
        printList(head);
    }
    return 0;
}
// } Driver Code Ends


 


//Function to merge two sorted linked list.
Node* sortedMerge(Node* head1, Node* head2)  
{  
    // code here
    if(head1==NULL){
        return head2;
    }
    if(head2==NULL){
        return head1;
    }
    if(head1->data > head2->data){
        head2->next=sortedMerge(head1,head2->next);
        return head2;
    }
    else{
        head1->next=sortedMerge(head1->next,head2);
        return head1;
    }
    
}
```

## Problem No. 15-[Nth item through sum](https://practice.geeksforgeeks.org/problems/nth-item-through-sum3544/1#)
Given two sorted arrays A and B of length L1 and L2, we can get a set of sums(add one element from the first and one from second). Find the Nth element in the set considered in sorted order.<br/>
**Note:** Set of sums should have unique elements.

Solution-

```
#User function Template for python3

class Solution:
    def nthItem(self, L1, L2, A, B, N):
        # code here
        d={A[i]+B[j]:1 for i in range(L1) for j in range(L2)}
        if N>len(d):
            return -1
        else:
            return sorted(d.items(), key=lambda x:x[0])[N-1][0]

#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__':
    t = int(input())
    for _ in range(t):
        L1, L2 = [int(x) for x in input().split()]
        A = input().split()
        for itr in range(L1):
            A[itr] = int(A[itr])
        B = input().split()
        for it in range(L2):
            B[it] = int(B[it])
        N = int(input())
        
        ob = Solution()
        print(ob.nthItem(L1, L2, A, B, N))
# } Driver Code Ends
```

## Problem No. 16-[Largest number with given sum](https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1/#)
Geek lost the password of his super locker. He remembers the number of digits N as well as the sum S of all the digits of his password. He know that his password is the largest number of N digits that can be made with given sum S. As he is busy doing his homework, help him retrieving his password.

Solution-
```
#User function Template for python3

class Solution:
    #Function to return the largest possible number of n digits
    #with sum equal to given sum.
    def largestNum(self,n,s):
        
        # code here
        no_ofnine=s//9
        if no_ofnine+min(1,s%9)>n:
            return -1
        else:
            return no_ofnine*"9"+min(1,s%9)*str(s%9)+(n-no_ofnine-min(1,s%9))*"0"
            
    
    
if __name__ == '__main__':
    test_cases = int(input())
    for cases in range(test_cases) :
        n,s = map(int,input().strip().split())
        ob = Solution()
        print(ob.largestNum(n,s))
```
