# STACK AND QUEUE

IMPLEMENT STACK USING ARRAYS
https://www.codingninjas.com/codestudio/problems/stack-implementation-using-array_3210209

```
#include <bits/stdc++.h> 
// Stack class.
class Stack {
    int *s;
    int t;
    int size;
public:
    
    Stack(int capacity) {
        // Write your code here.
        s=new int[capacity];
        t=-1;
        size=capacity;
    }

    void push(int num) {
        // Write your code here.
        if(t == size-1)
            {}
        else
            s[++t]=num;
    }

    int pop() {
        // Write your code here.
        if(t!=-1)
            return s[t--];
        else    
            return -1;
    }
    
    int top() {
        // Write your code here.
        if(t!=-1)
        return s[t];
        else
        return -1;
    }
    
    int isEmpty() {
        // Write your code here.
        if(t==-1) return 1;
        else  return 0;
    }
    
    int isFull() {
        // Write your code here.
        if(t==size-1)
            return 1;
        else 
            return 0;
    }
    
};
```
***
IMPLEMENT QUEUE USING ARRAYS
https://www.codingninjas.com/codestudio/problems/2099908

Note- CIRCULAR QUEUE
```
#include <bits/stdc++.h> 
class Queue {
public:
    int *arr;
    int f;
    int rear;
    int size;

    Queue() {
        // Implement the Constructor
        size=10001;
        arr=new int[size];
        f=rear=-1;
    }

    /*----------------- Public Functions of Queue -----------------*/

    bool isEmpty() {
        // Implement the isEmpty() function
        return (f==-1);
    }

    void enqueue(int data) {
        // Implement the enqueue() function
        if((f==0 && rear==size-1) || (rear==(f-1)%(size-1)))
        {
         return;   
        }   
        else if(f==-1)
        {
            f=rear=0;
            arr[rear]=data;
        }
        else if(rear==size-1)
        {
            rear=0;
            arr[rear]=data;
        }
        else
        {
            rear++;
            arr[rear]=data;
        }

    }

    int dequeue() {
        // Implement the dequeue() function
        if(f==-1)
          return -1;
        
        int remove=arr[f];
        if(f == rear)
        {
            f=rear=-1;
        }
        else if(f==size-1)
        {
            f=0;
        }
        else
        {
            f++;
        }
        return remove;
    }

    int front() {
        // Implement the front() function
        if(f==-1)
            return -1;
        else
            return arr[f];    
    }
};

```
***
IMPLEMENT STACK USING QUEUE

https://leetcode.com/problems/implement-stack-using-queues/
```
class MyStack {
public:
    queue <int> q1,q2;
    MyStack() {   
    }  
	
    void push(int x) {
        q2.push(x);
        while(!q1.empty())
        {
            q2.push(q1.front());
            q1.pop();
        }
        queue<int> q;
        q=q2;
        q2=q1;
        q1=q;
    }
	
    int pop() {
        if(!q1.empty())
            {
                int r=q1.front();
                q1.pop();
                return r;
            }
        else
            return -1;
    }  
	
    int top() {
        if(!q1.empty())
            return q1.front();
        else
            return -1;
    }
    
    bool empty() {
        return (q1.empty());
    }
};
```
***
IMPLEMENT QUEUE USING STACK

Push operation: O(N). 
Pop operation: O(1). 
```
class MyQueue {
public:
    stack <int> s1,s2;
    MyQueue() {
        
    }
    
    void push(int x) {
        
        while(!s1.empty())
        {
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(x);
        while(!s2.empty())
        {
            s1.push(s2.top());
            s2.pop();
        }
        
    }
    
    int pop() {
        if(s1.empty()) return -1;

        int r=s1.top();
        s1.pop();
        return r;
    }
    
    int peek() {
        if(s1.empty()) return -1;

        int r=s1.top();
        return r;
    }
    
    bool empty() {
        return (s1.empty());
    }
};
```

Push operation: O(1). 
Pop operation: O(N) in general and O(1) amortized time complexity.
```
class MyQueue {
public:
    stack<int> s1,s2;
    MyQueue() {
        
    }
    
    void push(int x) {
        s1.push(x);
    }
    
    int pop() {
        
        if(s1.empty() && s2.empty()) 
            return -1;
        
        if(s2.empty())
        {
            while(!s1.empty())
                {
                s2.push(s1.top());
                s1.pop();
                }
        }
        int r=s2.top();
        s2.pop();
        return r;
    }
    
    int peek() {
        if(s1.empty() && s2.empty()) 
            return -1;
        
        if(s2.empty())
        {
            while(!s1.empty())
                {
                s2.push(s1.top());
                s1.pop();
                }
        }
        int r=s2.top();
        return r;
    }
    
    bool empty() {
        return (s1.empty() && s2.empty());
    }
};
```
***

CHECK FOR BALANCED PARENTHESIS
https://leetcode.com/problems/valid-parentheses/description/

```
class Solution {
public:
    bool isValid(string s) {
    stack <int> m;
    int n=s.size();
    for(int i=0;i<n;i++)
    {
        if(s[i]=='(' || s[i]=='[' || s[i]=='{')
        {
            m.push(s[i]);
        }
        else
        {
            if(m.empty())
                return false;
            if((s[i]==')' && m.top()=='(') || (s[i]==']' && m.top()=='[') || (s[i]=='}' && m.top()=='{') )
                m.pop();
            else
                return false;
        }
    }
    return(m.empty());
    
    }
};
```
***
NEXT GREATER ELEMENT 2
https://leetcode.com/problems/next-greater-element-ii/description/

```
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n=nums.size();
        stack <int> k;
        vector <int> next(n,-1);
        for(int i=2*n-1;i>=0;i--)
        {
            while(!k.empty() && k.top() <= nums[i%n])
            {
                k.pop();
            }
            if(i<n)
            {
                if(!k.empty())
                    next[i]=k.top();
            }
            k.push(nums[i%n]);
        }
        return next;
    }
};
```
***
SORT A STACK

```
#include <bits/stdc++.h> 
void insert(stack<int> &stack, int n)
{
	if(stack.empty() || (!stack.empty()&& stack.top() < n))
	{
		stack.push(n);
		return;
	}
	int k=stack.top();
	stack.pop();

	insert(stack,n);

	stack.push(k);
}
void sortStack(stack<int> &stack)
{
	// Write your code here
	if(stack.empty())
	{
		return;
	}

	int l=stack.top();
	stack.pop();
	sortStack(stack);
	insert(stack,l);
}
```
* * *