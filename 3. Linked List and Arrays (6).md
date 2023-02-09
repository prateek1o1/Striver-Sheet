# LINKED LIST AND ARRAYS

ROTATE A LINKED LIST
https://leetcode.com/problems/rotate-list/description/
```
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        ListNode* t;
        t=head;
    
        if(head==NULL) return head;
    
        int counts=1;
        while(t->next!=NULL)
        {
            counts++;
            t=t->next;
        }
        k=k%counts;
        t->next=head;
        int cut=counts-k;
        while(cut--) t=t->next;
        
        head=t->next;
        t->next=NULL;
        
        
    return head;
    }
};
```
$O(n)$
* * *

CLONE A LINKED LIST WITH RANDOM AND NEXT POINTER

https://leetcode.com/problems/copy-list-with-random-pointer/
```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        
        Node* t=head;
        while(t!=NULL)
        {
        Node* copy= new Node(t->val);
        Node* front=t->next;
        t->next=copy;
        copy->next=front;
        t=front;
        }
        
        t=head;
        while(t!=NULL)
        {
            if(t->random)
            {
                t->next->random=t->random->next;
            }
             t=t->next->next; 
        }
        
        t=head;
        Node* dummy=new Node(0);
        Node *k=dummy;
        while(t!=NULL)
        {
            Node* front=t->next->next;
            dummy->next=t->next;
            t->next=front;
            dummy=dummy->next;
            t=front;
        }
        return k->next;
    }
};
```
* * *

3 SUM
https://leetcode.com/problems/3sum/
```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        
        sort(nums.begin(),nums.end());
        vector <vector <int>> Triplets;
        
        
        for(int i=0;i<nums.size()-1;i++)
        {
            if(i==0 || (i>0 && nums[i]!=nums[i-1]))
            {    
                 int sum=0-nums[i];
                 int l=i+1,r=nums.size()-1;
                 while(l<r)
                 {
                     if(nums[l]+nums[r]==sum)
                     {
                         vector<int> t;
                         t.push_back(-sum);
                         t.push_back(nums[l]);
                         t.push_back(nums[r]);
                         Triplets.push_back(t);
                         
                         while(l<r && nums[l]==nums[l+1]) l++;
                         while(l<r && nums[r]==nums[r-1]) r--;
                         l++,r--;
                     }
                     else if(nums[l]+nums[r]<sum)
                         l++;
                     else
                         r--;
                 }
            }
        }
        return Triplets;
    }
};
```
* * *

TRAPPING RAINWATER
https://leetcode.com/problems/trapping-rain-water/
```
class Solution {
public:
    int trap(vector<int>& height) {
        
        int start=0,end=height.size()-1;
        int startmax=0,endmax=0;
        int trapped=0;
        while(start<=end)
        {
            if(height[start]<=height[end])
            {
                if(height[start]>=startmax)
                    startmax=height[start];
                else
                    trapped+=startmax-height[start];
               
                start++;
            }
            else 
            {
             if(height[end]>=endmax)
                    endmax=height[end];
                else
                    trapped+=endmax-height[end];
               
                end--;
            }
        }
    return trapped;
    }
};
```
* * *

REMOVE DUPLICATE FROM SORTED ARRAY
https://leetcode.com/problems/remove-duplicates-from-sorted-array/
```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        unordered_map <int,int> mapping;
        int tracker=0;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]!=nums[tracker])
            {   tracker++;
                nums[tracker]=nums[i];
            }
         else
            {
                continue;
            }
        }
     return tracker+1;   
    }
};
```

* * *

MAX CONSECUTIVE ONES
https://leetcode.com/problems/max-consecutive-ones/
```
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int i=0;
        int huge=0;
        int counting=0;
        while(i < nums.size())
        {
            if(nums[i]==1)
            {counting++;
            
            if(counting>huge)
            {
                huge=counting;
            }
            }
            else
            {
                counting=0;
            }
            i++;
        }
    return huge;
    }
};
```
* * *