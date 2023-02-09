# LINKED LIST

REVERSE A LINKED LIST
https://leetcode.com/problems/reverse-linked-list/

```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev,*curr,*nxt;
        prev=NULL;
        curr=head;
            while(curr!=NULL)
            {   
                nxt=curr->next;
                curr->next=prev;
                prev=curr;
                curr=nxt;     
            }
        return prev;
    }
};
```

* * *

FIND THE MIDDLE OF LINKED LIST
https://leetcode.com/problems/middle-of-the-linked-list/

```
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *temp;
        int size =0;
    temp=head;
    while(temp!=NULL)
    {temp=temp->next;
     size+=1;   
    }
    if(size%2!=0)
    {size=(size+1)/2;
    }
    else
    {size=(size/2)+1;
    }
          temp=head;
    for(int i=0;i<size-1;i++)
    {
        temp=temp->next;
    }
    return temp; 
}
};
```

* * *

```
class Solution { 
public: ListNode* middleNode(ListNode* head) 
{ ListNode *slow = head, *fast = head; 
while (fast && fast->next) slow = slow->next, fast = fast->next->next; return slow; } };
```

* * *

MERGE TWO SORTED LINKED LIST
https://leetcode.com/problems/merge-two-sorted-lists/

```
  ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode *rethead,p1,p2;
        if(list1== NULL) return list2;
        if(list2== NULL) return list1;
        if(list1->val > list2->val) swap(list1,list2);
        rethead=list1;
        while(list1!=NULL && list2!=NULL)
        {
            ListNode *temp;    
            while(list1!=NULL && list1->val <= list2->val)
            {
                temp=list1;
                list1=list1->next;
            }
            temp->next=list2;
            swap(list1,list2);
        }
            return rethead;
    }
***
REMOVE NTH NODE FROM BACK OF LINKED LIST https://leetcode.com/problems/remove-nth-node-from-end-of-list/
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
       ListNode * rethead= new ListNode();
      rethead->next=head;
    ListNode * first = new ListNode();
    ListNode * second = new ListNode();
           first=rethead;
        second=rethead
    for(int i=1;i<=n;i++)
        first=first->next;
    while(first->next!=NULL)
    {
        first=first->next;
        second=second->next;
    }
            second->next=second->next->next;
            return rethead->next;
    }
};
```

* * *

ADD TWO NUMBERS AS LINKED LIST
https://leetcode.com/problems/add-two-numbers/

```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* rethead=new ListNode();
        ListNode* temp=new ListNode();
        rethead=temp;
        int cy=0;
        while(l1!=NULL || l2!=NULL || cy==1)
        {
            int add=0;
            if(l1!=NULL)
            {
                add+=l1->val;
                l1=l1->next;
            }
            if(l2!=NULL)
            {
                add+=l2->val;
                l2=l2->next;
            }
            add+=cy;
            cy=add/10;
            ListNode* newnode=new ListNode(add%10);
            temp->next=newnode;
            temp=temp->next;
        }
                  return rethead->next;
    }
};
```

* * *

DELETE A GIVEN NODE WHEN A NODE IS GIVEN

https://leetcode.com/problems/delete-node-in-a-linked-list/
```
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val=node->next->val;
        node->next=node->next->next;
    }
};
```
$O(1)$
* * *

# LINKED LIST 2

FIND INTERSECTION POINT OF 2 LINKED LIST
https://leetcode.com/problems/intersection-of-two-linked-lists/
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode *> pointer;
        ListNode *t=headA;
        ListNode *u=headB;
        while(t)
        {   pointer.insert(t);
            t=t->next;
        }
        while(u)
        {
            if(pointer.find(u)!=pointer.end())
            {
                return u;
            }
            u=u->next;
        }
        return NULL;
    }
};
```
$O(m+n)$

***
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
       ListNode *x =headA;
       ListNode *y =headB;
        
        while(x!=y)
        {
            if(x == NULL)
                x=headB;
            else
                x=x->next;
            
            if(y == NULL)
                y=headA;
            else 
                y=y->next;
        }
        return x;
    }
};
```
$O \max (length\ L1 , Length\ L2)$

* * *

DETECT A CYCLE IN LINKED LIST
https://leetcode.com/problems/linked-list-cycle/
```
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *slow=head;
        ListNode *fast=head;
        
        if(head==NULL) return false;
        
        while(fast->next!=NULL && fast->next->next!=NULL)
        {
            fast=fast->next->next;
            slow=slow->next;
            
            if(fast==slow) return true;
        }
        
        return false;
        
    }
};
```

* * *

REVERSE A LINKED LIST IN GROUPS OF SIZE K
https://leetcode.com/problems/reverse-nodes-in-k-group/
```
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        
        if (head->next==NULL || K==1)
            return head;
			
        int length =0;
        ListNode *a=head;
        while(a!=NULL)
        {   length++;
            a=a->next;
        }
        
        ListNode* dummy=new ListNode(0);
        ListNode* current;
        ListNode* previous;
        ListNode* tocome;
        dummy->next=head;
        previous=dummy;
        
        while(length>=k)
        {
            current=previous->next;
            tocome=current->next;
            for(int i=1;i<k;i++)
            {
                current->next=tocome->next;
                tocome->next=previous->next;
                previous->next=tocome;
                tocome=current->next;
            }
            length-=k;
            previous=current;
            
        }
    return dummy->next;
    }
	};
```

* * *

CHECK IF A LINKED LIST IS PALINDROME OR NOT
https://leetcode.com/problems/palindrome-linked-list/
```
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        
        ListNode *slow,*fast;
        slow=head;
        fast=head;
        
        while(fast->next!=NULL && fast->next->next!=NULL)
        {
            slow=slow->next;
            fast=fast->next->next;
        }
        ListNode *c,*p,*n;
        p=NULL;
        c=slow->next;
        while(c)
        {
            n=c->next;
            c->next=p;
            p=c;
            c=n;
        }
        slow->next=p;
        
        ListNode *first=head;
        ListNode *second=slow->next;
        while(second)
        {
            if(first->val==second->val)
            {second=second->next;
            first=first->next;
            }
            else
                return false;
        }
        
        return true;
    }
};
```
* * *

FIND THE STARTING POINT OF THE LOOP OF LINKED LIST
https://leetcode.com/problems/linked-list-cycle-ii/
(Slow and Fast pointer method)
```
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow=head, *fast=head, *check=head;
        if(head==NULL)
           return NULL;
        while(fast->next!=NULL && fast->next->next!=NULL)
        {
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast)
            {
            while(check!=slow)
              {
            check=check->next;
            slow=slow->next;
                }
        return check;
            }
        }
		return NULL;  
    }
};
```
* * *

FLATENNING OF A LINKED LIST
https://practice.geeksforgeeks.org/problems/flattening-a-linked-list/1
```
Node *merge( Node * g, Node * h)
{
    Node *t=new Node(0);
    Node *extra=t;
    
    while(g!=NULL && h!=NULL)
    {
     if(g->data < h->data)
     {
         t->bottom=g;
         t=t->bottom;
         g=g->bottom;
     }
     else
     {   t->bottom=h;
         t=t->bottom;
         h=h->bottom;
     }
    }
    if(g) t->bottom=g;
    else t->bottom=h;

    return extra->bottom;
}
    
Node *flatten(Node *root)
{
   // Your code here
   if(root==NULL || root->next==NULL)
   return root;
   
   root->next=flatten(root->next);
   
   root=merge(root,root->next);

    return root;   
 }
```
* * *