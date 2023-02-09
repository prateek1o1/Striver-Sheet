# BINARY TREE (MISCELLANEOUS)

BINARY TREE TO DOUBLE LINKED LIST
https://leetcode.com/problems/flatten-binary-tree-to-linked-list/
```
class Solution {
public:
    void flatten(TreeNode* root)
    {
    TreeNode* current=root;
        
        while(current!=NULL)
        {
            if(current->left!=NULL)
            {
              TreeNode* previous=current->left;
                
                while(previous->right)
                {
                    previous=previous->right;
                }
                previous->right=current->right;
                current->right=current->left;
                current->left=NULL;
            }
            current=current->right;
        }
    }
};
```
***
FIND MEDIAN IN A STREAM OF RUNNING INTEGERS
https://leetcode.com/problems/find-median-from-data-stream/
```
class MedianFinder {
public:
    priority_queue <int> HS;
    priority_queue <int,vector <int>, greater <int>> HB;
    void addNum(int num) {
        
        HS.push(num);
        HB.push(HS.top());
        HS.pop();
        
        if(HB.size() > HS.size()) // ns >= nb
        {
            HS.push((HB.top()));
            HB.pop();
        }
    }
    
    double findMedian() 
    {
        if(HS.size()>HB.size()) return HS.top();
    
        return (HS.top()+HB.top()) / 2.0;
    }
};
```
***
KTH LARGEST ELEMENT IN A STREAM
https://leetcode.com/problems/kth-largest-element-in-a-stream/
```
class KthLargest {
public:
    priority_queue <int,vector<int>,greater <int>> PRIO;
    int K;
    KthLargest(int k, vector<int>& nums) {
        K=k;
        for(auto i:nums)
        {
            PRIO.push(i);
        }
    }
    
    int add(int val) {
        
        PRIO.push(val);
        while(PRIO.size() > K)
        {   
        PRIO.pop();
        }
        
        return PRIO.top();
    }
};
```
***
DISTINCT NUMBERS IN WINDOW
https://www.interviewbit.com/problems/distinct-numbers-in-window/
```
vector<int> Solution::dNums(vector<int> &A, int B) {
    
    unordered_map <int,int> H;
    vector <int> answer;
    
    int count=0;
    
    for(int i=0;i<B;i++)
    {
        if(H[A[i]]==0)
        {
            count+=1;
        }
        H[A[i]]+=1;
    }
    int N=A.size();
    answer.push_back(count);
    
    for(int i=B;i<N;i++)
    {
        if(H[A[i-B]]==1)
        {
                count--;
        }
        H[A[i-B]]-=1;
        
        if(H[A[i]]==0)
        {
            count++;
        }
        H[A[i]]+=1;
        
        answer.push_back(count);
    }
    return answer;
}
```
TC=$O(N)$
SC=$O(N)$
***
KTH LARGEST ELEMENT IN AN UNSORTED ARRAY
https://leetcode.com/problems/kth-largest-element-in-an-array/
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        
        priority_queue <int,vector<int>,greater <int>> PRIO;
        for(auto i:nums)
        {
            PRIO.push(i);
        }
        
        while(PRIO.size() > k)
        {
            PRIO.pop();
        }
        return PRIO.top();
    }
};
```
***
FLOOD FILL ALGORITHM
https://leetcode.com/problems/flood-fill/
```
class Solution {
public:
    void DFS(vector<vector<int>> &image,int i,int j,int value,int color)
    {
        if(i<0 || i>=image.size() || j<0 || j>=image[0].size() || image[i][j]!=value || image[i][j]==color )
        {
            return;
         }
        image[i][j]=color;
        DFS(image,i+1,j,value,color);
        DFS(image,i-1,j,value,color);
        DFS(image,i,j+1,value,color);
        DFS(image,i,j-1,value,color);
        
    }
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        
        int value=image[sr][sc];
        DFS(image,sr,sc,value,color);
        return image;
    }
};
```
TC=$O(N)$
SC=$O(N)$
***