# STACK AND QUEUE 2

NEXT SMALLER ELEMENT
https://www.codingninjas.com/codestudio/problems/1112581

Note- Using Stack
```
vector<int> Solution::prevSmaller(vector<int> &A) {
    
    int n=A.size();
    stack<int> s;
    vector<int> B(n,-1);
    
    for(int i=0;i<n;i++)
    {
        while(!s.empty() && s.top() >= A[i])
        {
            s.pop();
        }
        if(!s.empty())
            B[i]=s.top();
        
        s.push(A[i]);
    }
    return B;
}
```
***
LRU CACHE
https://leetcode.com/problems/lru-cache/

Note- Hashmap & Doubly Linked List
The functions get and put must each run in O(1) average time complexity.
```
class LRUCache {
public:
    class node{
    
    public:
        int key;
        int value;
        node *next;
        node *prev;
        node(int _key,int _val)
        {   
            key=_key;
            value=_val;
        }
    };
    node *head=new node(-1,-1);
    node *tail=new node(-1,-1);
    int size;
    unordered_map<int,node*> m;

    LRUCache(int capacity) {
        size=capacity;
        head->next=tail;
        tail->prev=head;
    }
    
    void addnode(node *newnode)
    {
        node* t=head->next;
        newnode->prev=head;
        newnode->next=t;
        head->next=newnode;
        t->prev=newnode;
    }

    void deletenode(node *delnode)
    {
        node *beforedel=delnode->prev;
        node *afterdel=delnode->next;

        beforedel->next=afterdel;
        afterdel->prev=beforedel;
    }

    int get(int key) {
        if(m.find(key)!=m.end())
        {
            node *rfnode=m[key];
            int rf=rfnode->value;
            deletenode(rfnode);
            addnode(rfnode);
            m[key]=head->next;
            return rf;
        }
        return -1;
    }
    
    void put(int key, int value) {
        if(m.find(key)!=m.end())
        {
            node* rfnode=m[key];
            m.erase(key);
            deletenode(rfnode);
        }
        if(m.size()==size)
        {
            m.erase(tail->prev->key);
            deletenode(tail->prev);
        }
        addnode(new node(key,value));
        m[key]=head->next;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
***

LFU CACHE (Hard)
https://leetcode.com/problems/lfu-cache/description/

```
struct Node
{
    int key,value,count;
    Node* next;
    Node* prev;
    Node(int _key,int _value)
    {
        key=_key;
        value=_value;
        count=1;
    }
};

struct List
{
    int size;
    Node *head;
    Node *tail;
    List()
    {
        head=new Node(0,0);
        tail=new Node(0,0);
        head->next=tail;
        tail->prev=head;
        size=0;
    }

    void addFront(Node *node)
    {
        Node *t=head->next;
        node->next=t;
        node->prev=head;
        head->next=node;
        t->prev=node;
        size++;
    }

    void removeNode(Node* delnode)
    {
        Node *delprev=delnode->prev;
        Node *delnext=delnode->next;
        delprev->next=delnext;
        delnext->prev=delprev;
        size--;
    }
};

class LFUCache {
public:
    map<int,Node*> keyNode;
    map<int, List*> freqListMap;
    int maxSizeCache;
    int minFreq;
    int curSize;

    LFUCache(int capacity) {
        maxSizeCache=capacity;
        minFreq=0;
        curSize=0;
    }
    void updateFreqListMap(Node *node)
    {
        keyNode.erase(node->key);
        freqListMap[node->count]->removeNode(node);
        if(node->count==minFreq && freqListMap[node->count]->size==0)
        {
            minFreq++;
        }
        List *nextHigherFreqList=new List();
        if(freqListMap.find(node->count+1)!=freqListMap.end())
        {
            nextHigherFreqList=freqListMap[node->count+1];
        }
        node->count+=1;
        nextHigherFreqList->addFront(node);
        freqListMap[node->count]=nextHigherFreqList;
        keyNode[node->key]=node;
    }
    
    int get(int key) {
        if(keyNode.find(key)!=keyNode.end())
        {
            Node *node=keyNode[key];
            int v=node->value;
            updateFreqListMap(node);
            return v;
        }
        return -1;
    }
    
    void put(int key, int value) {
        if(maxSizeCache==0)
        {
            return;
        }
        if(keyNode.find(key)!=keyNode.end())
        {
            Node* node=keyNode[key];
            node->value=value;
            updateFreqListMap(node);
        }
        else
        {
            if(curSize == maxSizeCache)
            {
                List* list=freqListMap[minFreq];
                keyNode.erase(list->tail->prev->key);
                freqListMap[minFreq]->removeNode(list->tail->prev);
                curSize--;
            }
            curSize++;
            minFreq=1;
            List *listFreq=new List();
            if(freqListMap.find(minFreq) != freqListMap.end())
            {
                listFreq=freqListMap[minFreq];
            }
            Node* node=new Node(key,value);
            listFreq->addFront(node);
            keyNode[key]=node;
            freqListMap[minFreq]=listFreq;
        }
    }
};

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache* obj = new LFUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
***
LARGEST RECTANGLE IN A HISTORAM (Hard)
https://leetcode.com/problems/largest-rectangle-in-histogram/

```
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n=heights.size();
        vector<int> ns(n,n),ps(n,-1);
        stack<int> s;
        int MaxArea=INT_MIN;
        for(int i=0;i<n;i++)
        {
            while(!s.empty() && heights[s.top()]>=heights[i])
                s.pop();
            
            if(!s.empty())
                ps[i]=s.top();
            
            s.push(i);
        }
        while(!s.empty())
            s.pop();

        for(int i=n-1;i>=0;i--)
        {
            while(!s.empty() && heights[s.top()]>=heights[i])
                s.pop();
            
            if(!s.empty())
                ns[i]=s.top();
            
            s.push(i);
        }

        for(int i=0;i<n;i++)
        {
         int width=ns[i]-ps[i]-1;
         MaxArea=max(MaxArea,heights[i]*width);
        }
        return MaxArea;
    }
};
```
***
SLIDING WINDOW MAXIMUM (Hard)
https://leetcode.com/problems/sliding-window-maximum/

```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        
        int n=nums.size();
        deque<int> d;
        vector<int> a;
        for(int i=0;i<n;i++)
        {
            if(!d.empty() && d.front()==i-k) 
                d.pop_front();

            while(!d.empty() && nums[d.back()] < nums[i])
                d.pop_back();

            d.push_back(i);

            if(i>=k-1) a.push_back(nums[d.front()]);
        }
        return a;
    }
};
```
***
$TC=O(N)+O(N)$

IMPLEMENT MIN STACK
https://leetcode.com/problems/min-stack/

1.
```
class MinStack {
public:
stack<pair<int,int>> s;
    MinStack() {
        
    }
    
    void push(int val) {
        int minimum;
        if(s.empty())
        {
            minimum=val;
        }
        else
        {
            minimum=min(s.top().second,val);
        }
        s.push({val,minimum});
    }
    
    void pop() {
        s.pop();
    }
    
    int top() {
        return s.top().first;
    }
    
    int getMin() {
        return s.top().second;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

2.
```
class MinStack {
public:
    stack<long long> s;
    long long m;

    MinStack() {
        m=INT_MAX;    
    }
    
    void push(int val) {
        long long value=val;
        if(s.empty())
        {
            m=value;
            s.push(value);
        }
        else
        {
            if(value < m)
            {
                s.push(1LL* 2* value - m);
                m=value;
            }
            else
            {
                s.push(value);
            }
        }
    }
    
    void pop() {
        if(s.empty())
            return;
        long long t=s.top();
        s.pop();
        if(t < m)
            {
                m=2*m-t;
            }
    }
    
    int top() {
        if(s.empty())
            return -1;
        
        long long t=s.top();
        if(t < m) 
            return m;
        else
            return t;
        
    }
    
    int getMin() {
        return m;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

***
ROTTEN ORANGE (BFS & Queue)
https://leetcode.com/problems/rotting-oranges/

```
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        
        int m=grid.size();
        int n=grid[0].size();

        vector<vector<int>> v(m,vector<int>(n,0));
        queue< pair<pair<int,int>,int> > Q;

        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
                {
                    if(grid[i][j]==2)
                            {
                                Q.push({{i,j},0});
                                v[i][j]=2;
                            }
                }
        }
        int di[]={-1,1,0,0};
        int dj[]={0,0,-1,1};
        int answer;
        int time=0;
        while(!Q.empty())
        {
            pair<pair<int,int>,int> data=Q.front();
            Q.pop();
            time=data.second;
            int i=data.first.first;
            int j=data.first.second;
            for(int k=0;k<4;k++)
            {
                int p=i+di[k];
                int q=j+dj[k];

          if(p<m && p>=0 && q<n && q>=0 && grid[p][q]==1 && v[p][q]!=2 )
                {
                    v[p][q]=2;
                    Q.push({{p,q},time+1});
                }
            }
        }
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(grid[i][j]==1 && v[i][j]!=2)
                {
                    return -1;
                }
            }
        }
        return time;
    }
};
```
$TC=O(N*M)$
***

STOCK SPAN PROBLEM
https://leetcode.com/problems/online-stock-span/

```
class StockSpanner {
public:
    stack<pair<int,int>> Monotonic;
    StockSpanner() {     
    }
    int next(int price) {
        int r=1;
        while(!Monotonic.empty() && Monotonic.top().first<=price)
        {
            r+=Monotonic.top().second;
            Monotonic.pop();
        }
        Monotonic.push({price,r});
        return r;
    }
};

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner* obj = new StockSpanner();
 * int param_1 = obj->next(price);
 */
```
***
FIND THE MAXIMUM OF MINIMUMS OF EVERY WINDOW SIZE (Hard)
https://www.codingninjas.com/codestudio/problems/max-of-min_982935

1. Naive Approach $O(N^3)$
```
#include <bits/stdc++.h>
using namespace std;

void printMaxOfMin(int arr[], int n)
{	for (int k = 1; k <= n; k++) 
	{
		int maxOfMin = INT_MIN;
		for (int i = 0; i <= n - k; i++) 
		{
			int min = arr[i];
			for (int j = 1; j < k; j++) 
			{
				if (arr[i + j] < min)
					min = arr[i + j];
			}
		if (min > maxOfMin)
				maxOfMin = min;
		}
		cout << maxOfMin << " ";
	}
}
```

2. Using Stack $O(N)$
```
#include <bits/stdc++.h>
using namespace std; 
vector<int> maxMinWindow(vector<int> a, int n) {
    // Write your code here.
    vector<int> ps(n,-1),ns(n,n),answer(n,INT_MIN);
    stack <int> s;

    for(int i=0;i<n;i++)
    {
        while(!s.empty() && a[s.top()] >= a[i])
        {s.pop();
        }
        if(!s.empty())
            ps[i]=s.top();
        
        s.push(i);
    }
    while(!s.empty())
        s.pop();
    
     for(int i=n-1;i>=0;i--)
    {
        while(!s.empty() && a[s.top()] >= a[i])
        {s.pop();
        }
        if(!s.empty())
            ns[i]=s.top();
        
        s.push(i);
    }

    for(int i=0;i<n;i++)
    {
        int l=ns[i]-ps[i]-1;
        answer[l-1]=max(answer[l-1],a[i]);
    }
    for(int i=n-2;i>=0;i--)
    {
        answer[i]=max(answer[i],answer[i+1]);
    }
    return answer;
}


```
***
THE CELEBRITY PROBLEM
https://www.codingninjas.com/codestudio/problems/the-celebrity-problem_982769

```
#include <bits/stdc++.h> 
/*
	This is signature of helper function 'knows'.
	You should not implement it, or speculate about its implementation.

	bool knows(int A, int B); 
	Function 'knows(A, B)' will returns "true" if the person having
	id 'A' know the person having id 'B' in the party, "false" otherwise.
*/
using namespace std;
int findCelebrity(int n) {
 	// Write your code here.
	stack <int> s;
	for(int i=0;i<n;i++)
		s.push(i);

	while(s.size()>1)
	{
		int a=s.top();
		s.pop();
		int b=s.top();
		s.pop();
		if(knows(a,b)==true)
		{
			s.push(b);
		}
		else
		{
			s.push(a);
		}
	}
	int c=s.top();

	for(int i=0;i<n;i++)
	{
		if((i!=c) && (knows(c,i) || !knows(i,c)))
			return -1;
	}	 

	return c;
}

```
***