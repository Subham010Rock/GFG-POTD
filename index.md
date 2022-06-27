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

## Problem No. 17-[Unique Subsets](https://practice.geeksforgeeks.org/problems/subsets-1587115621/1#)
Given an array arr[] of integers of size N that might contain duplicates, the task is to find all possible unique subsets.<br/>
Note: Each subset should be sorted.

Solution-
```
// { Driver Code Starts
#include <bits/stdc++.h>
using namespace std;


 // } Driver Code Ends
class Solution
{
    public:
    //Function to find all possible unique subsets.
    vector<vector<int> > AllSubsets(vector<int> arr, int n)
    {
        // code here 
         set<vector<int>>s;
        vector<vector<int>>res={};
        unsigned int set_size=pow(2,n);
	    for(int i=0;i<set_size;i++){
	        vector<int>a;
	    for(int j=0;j<n;j++){
	        if(i & (1<<j))
	        a.push_back(arr[j]);
	    }
	    sort(a.begin(),a.end());
	    s.insert(a);
	  }
	  for(std::set<vector<int>>::iterator it=s.begin();it!=s.end();it++){
	      res.push_back(*it);
	  }
	  //sort(res.begin(),res.end());
	  return res;
    }
};

// { Driver Code Starts.

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        vector<int> A;
        int x;
        for(int i=0;i<n;i++){
            cin>>x;
            A.push_back(x);
        }
        Solution obj;
        vector<vector<int> > result = obj.AllSubsets(A,n);
        // printing the output
        for(int i=0;i<result.size();i++){
            cout<<'(';
            for(int j=0;j<result[i].size();j++){
                cout<<result[i][j];
                if(j<result[i].size()-1)
                    cout<<" ";
            }
            cout<<")";
        }
        cout<<"\n";
    }
}   


  // } Driver Code Ends
  ```
  
## Problem N0. 18-[Longest subarray with sum divisible by K](https://practice.geeksforgeeks.org/problems/longest-subarray-with-sum-divisible-by-k1259/1#)
Given an array containing N integers and a positive integer K, find the length of the longest sub array with sum of the elements divisible by the given value K.

Solution--
```
#User function Template for python3
class Solution:
    def longSubarrWthSumDivByK (self,arr,  n, K) : 
        #Complete the function
        d={}
        s=0
        index=0
        for ind,i in enumerate(arr):
            s+=i
            r=s%K
            if r==0:
                index=ind+1
            elif r in d:
                index=max(index,ind-d[r])
            else:
                d[r]=ind
        return index



#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__':

    for _ in range(0,int(input())):
        n, K = map(int ,input().split())
        arr = list(map(int,input().strip().split()))
        ob = Solution()
        res = ob.longSubarrWthSumDivByK(arr, n, K)
        print(res)

# } Driver Code Ends
```

## Problem No. 19-[Minimum Number in a sorted rotated array](https://practice.geeksforgeeks.org/problems/minimum-number-in-a-sorted-rotated-array-1587115620/1#)
Given an array of distinct elements which was initially sorted. This array is rotated at some unknown point. The task is to find the minimum element in the given sorted and rotated array.

Solution--
```
// { Driver Code Starts
#include <bits/stdc++.h>
using namespace std;


 // } Driver Code Ends


class Solution
{
    public:
    //Function to find the minimum element in sorted and rotated array.
    int minNumber(int arr[], int low, int high)
    {
        // Your code here
        int mid;
        while(low<=high){
            mid=low+(high-low)/2;
                if(arr[mid]>=arr[high])
                low=mid+1;
                else
                high=mid;
        }
        return arr[mid];
         
        
    }
};

// { Driver Code Starts.


int main()
{
	
	int t;
	cin>>t;
	while(t--)
	{
		int n;
		cin>>n;
		int a[n];
		for(int i=0;i<n;++i)
			cin>>a[i];	
		Solution obj;
		cout << obj.minNumber(a,0,n-1) << endl;
	}
	return 0;
}  // } Driver Code Ends
```
## Problem No. 20-[Permutation with Spaces](https://practice.geeksforgeeks.org/problems/permutation-with-spaces3627/1)
Given a string you need to print all possible strings that can be made by placing spaces (zero or one) in between them. The output should be printed in sorted increasing order of strings.

Solution-
```
// { Driver Code Starts
#include <bits/stdc++.h>
using namespace std;


 // } Driver Code Ends
class Solution{
public:
    void powerset(string S,string curr,vector<string>&res,int i){
        if(i==S.length()){
            res.push_back(curr);
            return;
        }
        if(i!=0)
        powerset(S,curr+" "+S[i],res,i+1);
        powerset(S,curr+S[i],res,i+1);
    }

    vector<string> permutation(string S){
        // Code Here
        vector<string>res;
        powerset(S,"",res,0);
        return res;
    }
};

// { Driver Code Starts.

int  main(){
    int t;
    cin>>t;
    while(t--){
        string S;
        cin>>S;
        vector<string> ans;
        Solution obj;
        ans = obj.permutation(S);
        for(int i=0;i<ans.size();i++){
            cout<<"("<<ans[i]<<")";
        }
        cout << endl;
    }
}
  // } Driver Code Ends
  ```

## Problem No. 21-[Transform String](https://practice.geeksforgeeks.org/problems/transform-string5648/1)
Given two strings A and B. Find the minimum number of steps required to transform string A into string B. The only allowed operation for the transformation is selecting a character from string A and inserting it in the beginning of string A.

Solution--
```
#Back-end complete function Template for Python 3

class Solution:
    def transform(self, A, B): 
        #code here.
        if(len(A)!=len(B)):
            return -1
        da={}
        db={}
        res=0
        for i in A:
            da[i]=da.get(i,0)+1
        for i in B:
            db[i]=db.get(i,0)+1
        for i in A:
            if(da[i]!=db.get(i,0)):
                return -1
        j=len(B)-1
        i=len(A)-1
        while i>=0:
            #print(i,j)
            if(A[i]!=B[j]):
                while( i>=0 and A[i]!=B[j]):
                    res+=1
                    i-=1
                j-=1
                i-=1
            else:
                j-=1
                i-=1
        return res


#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__': 
    t = int(input())
    for _ in range(t):
        line = input().strip().split()
        A = line[0]
        B = line[1]
        ob = Solution()
        print(ob.transform(A,B))
# } Driver Code Ends
```
## Problem No. 22-[A Special Keyboard](https://practice.geeksforgeeks.org/problems/228d0aa9f26db93ee5b2cb3583dbd4b197447e16/1)
Imagine you have a special keyboard with all keys in a single row. The layout of characters on a keyboard is denoted by a string S1 of length 26. S1 is indexed from 0 to 25. Initially, your finger is at index 0.<br/>
To type a character, you have to move your finger to the index of the desired character. The time taken to move your finger from index i to index j is |j-i|, where || denotes absolute value.Find the time taken to type the string S2 with the given keyboard layout.

Solution-
```
#User function Template for python3

class Solution:
    def findTime(self, S1, S2):
        # code here 
        d={}
        for i in range(len(S1)):
            d[S1[i]]=i
        time_taken=d[S2[0]]
        last_visit=S2[0]
        for i in S2[1:]:
            time_taken+=(abs(d[i]-d[last_visit]))
            last_visit=i
        return time_taken
            

#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__': 
    t = int (input ())
    for _ in range (t):
        S1=input()
        S2=input()
        
        ob = Solution()
        print(ob.findTime(S1,S2))
# } Driver Code Ends
```
## Problem No. 23-[Farthest number](https://practice.geeksforgeeks.org/problems/1a31d09f7b8e9c0633339df07858deb3a728fe19/1#)
Given an array Arr[] of size N. For every element in the array, the task is to find the index of the farthest element in the array to the right which is smaller than the current element. If no such number exists then print -1.<br/>
Note: 0 based indexing.

Solution-
```
// { Driver Code Starts
//Initial Template for C++
#include<bits/stdc++.h>
using namespace std;

 // } Driver Code Ends
//User function Template for C++
class Solution{   
  public:
    int b_search(vector<int>&a,int t,int l,int h){
        int ind=-1;
        while(l<=h){
            if(a[h]<t){
                return h;
            }
            else{
                if(a[l]<t){
                    ind=l;
                }
                h--;
                l++;
            }
        }
        return ind;
    }
    vector<int> farNumber(int N,vector<int> Arr){
        //code here
        vector<int>res(N,-1);
        //sort(res.begin();res.end());
        for(int i=0;i<N-1;i++){
                res[i]=b_search(Arr,Arr[i],i+1,N-1);
        }
        return res;
    }
};

// { Driver Code Starts.
signed main()
{
    int t;
    cin>>t;
    while(t--)
    {
        int N;
        cin>>N;
        vector<int> Arr(N);
        for(int i=0;i<N;i++)
            cin>>Arr[i];
        Solution obj;
        vector<int> answer=obj.farNumber(N,Arr);
        for(auto i:answer)
            cout<<i<<" ";
        cout<<endl;
  }
}  // } Driver Code Ends
```

## Problem No. 24-[Find an Replace in String](https://practice.geeksforgeeks.org/problems/find-an-replace-in-string/1)
Given a string S on which you need to perform Q replace operations.<br/>
Each replacement operation has 3 parameters: a starting index i, a source word x and a target word y. The rule is that if x starts at position i in the original string S, then we will replace that occurrence of x with y. If not, we do nothing.<br/>
Note: All these operations occur simultaneously. It's guaranteed that there won't be any overlap in replacement: for example, S = "abc", indexes = [0,1], sources = ["ab", "bc"] is not a valid test case.<br/>

Solution-
```
#User function Template for python3

class Solution:
    def findAndReplace(self, S, Q, index, sources, targets):
        # code here 
        l=[]
        ind=0
        for i in range(Q):
            l.append(S[ind:index[i]])
            ind+=(index[i]-ind)
            if(S[index[i]:index[i]+len(sources[i])]==sources[i]):
                l.append(targets[i])
                ind+=len(sources[i])
        if ind<len(S):
            l.append(S[ind:])
        return "".join(l)

#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__': 
    t = int (input ())
    for _ in range (t):
        S=input()
        Q=int(input())
        index=list(map(int,input().split()))
        sources=list(map(str,input().split()))
        targets=list(map(str,input().split()))
        
        ob = Solution()
        print(ob.findAndReplace(S,Q,index,sources,targets))
# } Driver Code Ends
```
## Problem No. 25-[Even and Odd](https://practice.geeksforgeeks.org/problems/even-and-odd/1#)
Given an array arr[] of size N containing equal number of odd and even numbers. Arrange the numbers in such a way that all the even numbers get the even index and odd numbers get the odd index.<br/>
Note: There are multiple possible solutions, Print any one of them. Also, 0-based indexing is considered.

Solution-
```
// { Driver Code Starts
#include <bits/stdc++.h>
using namespace std;


 // } Driver Code Ends
//User function Template for C++

class Solution {
  public:
    void reArrange(int arr[], int N) {
        // code here
        int e=0;
        int o=1;
        while(e<N){
            if(arr[e]%2!=0){
                while(o<N){
                    if(arr[o]%2==0){
                        swap(arr[o],arr[e]);
                        break;
                    }
                    else{
                        o+=2;
                    }
                }
            }
            e+=2;
        }
    }
};

// { Driver Code Starts.

int check(int arr[], int n)
{
    int flag = 1;
    int c=0, d=0;
    for(int i=0; i<n; i++)
    {
        if(i%2==0)
        {
            if(arr[i]%2)
            {
                flag = 0;
                break;
            }
            else
                c++;
        }
        else
        {
            if(arr[i]%2==0)
            {
                flag = 0;
                break;
            }
            else
                d++;
        }
    }
    if(c!=d)
        flag = 0;
        
    return flag;
}

int main() {
    int t;
    cin >> t;
    while (t--) {
        int N;
        cin>>N;
        
        int arr[N];
        for(int i=0; i<N; i++)
            cin>>arr[i];

        Solution ob;
        ob.reArrange(arr,N);
        
        cout<<check(arr,N)<<endl;
    }
    return 0;
}  // } Driver Code Ends
```

## Problem No. 26-[Shortest Path between Cities](https://practice.geeksforgeeks.org/problems/shortest-path-between-cities/1#)
Geek lives in a special city where houses are arranged in a hierarchial manner. Starting from house number 1, each house leads to two more houses.<br/>
1 leads to 2 and 3. <br/>
2 leads to 4 and 5. <br/>
3 leads to 6 and 7. and so on. <br/>
Given the house numbers on two houses x and y, find the length of the shortest path between them. 

Solution-
```
#User function Template for python3

class Solution:
    def shortestPath(self, x, y): 
        # code here
        d={}
        if(x==y):
            return 0
        m=max(x,y)
        n=min(x,y)
        c=0
        while(m!=1):
            c+=1
            m=m//2
            d[m]=c
        r=0
        while(1):
            if n in d:
                return r+d[n]
            else:
                n=n//2
                r+=1

#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__': 
    t = int(input())
    for _ in range(t):
        x,y = map(int,input().strip().split())
        ob = Solution()
        print(ob.shortestPath(x,y))
# } Driver Code Ends
```
## Problem No. 27-[Nearly sorted](https://practice.geeksforgeeks.org/problems/nearly-sorted-1587115620/1)
Given an array of n elements, where each element is at most k away from its target position, you need to sort the array optimally.

Solution--
```
// { Driver Code Starts
#include<bits/stdc++.h>
using namespace std;


 // } Driver Code Ends
class Solution
{
    public:
    //Function to return the sorted array.
    vector <int> nearlySorted(int arr[], int num, int K){
        // Your code here
        priority_queue<int,vector<int>,greater<int>>p;
        for(int i=0;i<num;i++){
           p.push(arr[i]);
        }
        vector<int>res;
        for(int i=0;i<num;i++){
        res.push_back(p.top());
        p.pop();}
        
        return res;
    }
};

// { Driver Code Starts.

int main()
 {
	int T;
	cin>> T;
	
	while (T--)
	{
	    int num, K;
	    cin>>num>>K;
	    
	    int arr[num];
	    for(int i = 0; i<num; ++i){
	        cin>>arr[i];
	    }
	    Solution ob;
	    vector <int> res = ob.nearlySorted(arr, num, K);
	    for (int i = 0; i < res.size (); i++)
	        cout << res[i] << " ";
	        
	    cout<<endl;
	}
	
	return 0;
}
  // } Driver Code Ends
 ```

## Problem No. 28-[Help a Thief!!!](https://practice.geeksforgeeks.org/problems/help-a-thief5938/1#)
You have to help a thief to steal as many as GoldCoins as possible from a GoldMine. There he saw N Gold Boxes an each Gold Boxes consists of Ai Plates each plates consists of Bi Gold Coins. Your task is to print the maximum gold coins theif can steal if he can take a maximum of T plates.

Solution--
```
// { Driver Code Starts
//Initial Template for C++

#include <bits/stdc++.h>
using namespace std;

 // } Driver Code Ends
//User function Template for C++

class Solution {
  public:
    int maxCoins(int A[], int B[], int T, int N) {
        // code here
        vector<pair<int,int>>B_A;
        for(int i=0;i<N;i++){
            B_A.push_back(make_pair(B[i],A[i]));
        }
        sort(B_A.rbegin(),B_A.rend());
        int res=0;
        for(int i=0;i<N;i++){
            if(T>=B_A[i].second){
                res+=B_A[i].first*B_A[i].second;
                T-=B_A[i].second;
            }
            else{
                res+=T*B_A[i].first;
                break;
            }
        }
        return res;
    }
};

// { Driver Code Starts.
int main() {
    int t;
    cin >> t;
    while (t--) {
        int T,N;
        cin>>T>>N;
        
        int A[N], B[N];
        
        for(int i=0; i<N; i++)
            cin>>A[i];
        for(int i=0; i<N; i++)
            cin>>B[i];

        Solution ob;
        cout << ob.maxCoins(A,B,T,N) << endl;
    }
    return 0;
}  // } Driver Code Ends
```

## Problem No.29-[String formation from substring](https://practice.geeksforgeeks.org/problems/string-formation-from-substring2734/1#)
Given a string s, the task is to check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Solution-
```
#User function Template for python3
class Solution:
    def isRepeat(self, s):
        # code here
        n=len(s)
        for ind in range(n-1):
            if s[0:ind+1]*(n//(ind+1))==s:
                return 1
        return 0

#{ 
#  Driver Code Starts
#Initial Template for Python 3

if __name__ == '__main__':
    T=int(input())
    for i in range(T):
        s = input()
        
        ob = Solution()    
        answer = ob.isRepeat(s)
        
        print(answer)


# } Driver Code Ends
```

## Problem No.30- [Ishaan Loves Chocolates](https://practice.geeksforgeeks.org/problems/ishaan-loves-chocolates2156/1)
As we know, Ishaan has a love for chocolates. He has bought a huge chocolate bar that contains N chocolate squares. Each of the squares has a tastiness level which is denoted by an array A[].<br/>
Ishaan can eat the first or the last square of the chocolate at once. Ishaan has a sister who loves chocolates too and she demands the last chocolate square. Now, Ishaan being greedy eats the more tasty square first.<br/>
Determine the tastiness level of the square which his sister gets.

Solution--
```
// { Driver Code Starts
#include<bits/stdc++.h>
using namespace std;


int chocolates(int arr[], int n);


int main()
{
    
    int t;cin>> t;
    while(t--)
    {
        int n;
        cin >> n;
        int arr[n];
        
        for(int i=0;i<n;i++)
            cin>>arr[i];
        
        
        cout << chocolates(arr, n);
        cout << endl;
        
    }

}
// } Driver Code Ends


int chocolates(int arr[], int n)
{
    // Complete the function
    //return *min_element(arr,arr+n);
    int i=0;
    int j=n-1;
    while(i<j){
        if(arr[i]>arr[j])
        i++;
        else
        j--;
    }
    return arr[i];
    
}
```

## Problem No.31- [Reverse a sublist of a linked list](https://practice.geeksforgeeks.org/problems/reverse-a-sublist-of-a-linked-list/1#)
Given a linked list and positions m and n. Reverse the linked list from position m to n.

Solution--
```
// { Driver Code Starts
//Initial Template for C++

#include<bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node {
	int data;
	struct Node *next;
	Node(int x) {
		data = x;
		next = NULL;
	}
};


 // } Driver Code Ends
//User function Template for C++

/*Link list node 
struct Node {
	int data;
	struct Node *next;
	Node(int x) {
		data = x;
		next = NULL;
	}
};*/

class Solution
{
    public:
    Node* reverse(Node* start,Node* end,Node*back){       //Reverse Sublist
        if(start==end)
        return start;
        Node* temp=reverse(start->next,end,back);
        start->next->next=start;
        start->next=back;
        return temp;
    }
    Node* reverseBetween(Node* head, int m, int n)
    {
        //code here
        if(m==n)
        return head;
        Node* start,*end,*iter=head,*front=NULL,*back=NULL;
        int c=1;
        while(c!=n){
            if(c==m)
            start=iter;
            if(c<m)
            front=iter;
            c++;
            iter=iter->next;
        }
        end=iter;
        if(end!=NULL)
        back=end->next;
        Node*reverse_head=reverse(start,end,back);
        if(front!=NULL)
        front->next=reverse_head;
        else
        head=reverse_head;
        return head;
        
    }
};

// { Driver Code Starts.

/* Function to print linked list */
void printList(struct Node *head)
{
	struct Node *temp = head;
	while (temp != NULL)
	{
		printf("%d ", temp->data);
		temp = temp->next;
	}
}



// Driver program to test above functions
int main()
{
	int T;
	cin >> T;

	while (T--)
	{
		int N, m, n;
		cin >> N>>m>>n;

		Node *head = NULL;
		Node *temp = head;

		for (int i = 0; i < N; i++) {
			int data;
			cin >> data;
			if (head == NULL)
				head = temp = new Node(data);
			else
			{
				temp->next = new Node(data);
				temp = temp->next;
			}
		}

		

        Solution ob;

		Node* newhead = ob.reverseBetween(head, m, n);
		printList(newhead);

		cout << "\n";



	}
	return 0;
}
  // } Driver Code Ends
```
## Problem No. 32-[Left View of Binary Tree](https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1#)
Given a Binary Tree, print Left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side. The task is to complete the function leftView(), which accepts root of the tree as argument.

Left view of following tree is 1 2 4 8.
![image](https://user-images.githubusercontent.com/54362906/175775217-47fcd606-0f3b-490f-85af-36ea6591e3f6.png)

     
Solution--

```
//Function to return a list containing elements of left view of the binary tree.
void preorder(Node* root,int l,vector<int>&res){
    if(!root)
    return;
    if(res.size()==l)
    res.push_back(root->data);
    preorder(root->left,l+1,res);
    preorder(root->right,l+1,res);
}
vector<int> leftView(Node *root)
{
   // Your code here
   vector<int>res;
   preorder(root,0,res);
   return res;
}
```
## Problem No. 33-[Change Bits](https://practice.geeksforgeeks.org/problems/change-bits1538/1#)
Given a number N, complete the following tasks,<br/>
Task 1. Generate a new number from N by changing the zeroes in the binary representation of N to 1.<br/>
Task  2. Find the difference between N and the newly generated number.

Solution--
```
// { Driver Code Starts
//Initial Template for C++

#include <bits/stdc++.h>
using namespace std;

 // } Driver Code Ends
//User function Template for C++

class Solution {
  public:
    vector<int> changeBits(int N) {
        // code here
       int a=ceil(log2(N));
       int b=floor(log2(N));
       int n= a==b ? a+1:a;
       vector<int>v(2,0);
       v[1]=pow(2,n)-1;
       v[0]=v[1]-N;
       return v;
    }
};

// { Driver Code Starts.
int main() {
    int t;
    cin >> t;
    while (t--) {
        int N;
        cin>>N;
        Solution ob;
        auto ans = ob.changeBits(N);
        cout<<ans[0]<<" "<<ans[1]<<endl;
    }
    return 0;
}  // } Driver Code Ends
```
## Problem No. 34-[Inorder Traversal (Iterative)](https://practice.geeksforgeeks.org/problems/inorder-traversal-iterative/1#)
Given a binary tree. Find the inorder traversal of the tree without using recursion.

Solution--
```
class Solution {
public:
    vector<int> inOrder(Node* root)
    {
        //code here
        vector<int>res;
        stack<Node*>s;
        Node* r=root;
        while(!s.empty() or r!=NULL){
            if(r!=NULL){
                s.push(r);
                r=r->left;
            }
            else{
                res.push_back(s.top()->data);
                r=s.top()->right;
                s.pop();
            }
        }
        return res;
    }
};
```
