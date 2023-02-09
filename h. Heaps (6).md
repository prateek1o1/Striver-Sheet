# HEAPS

MAXIMUM HEAP & MINIMUM HEAP IMPLEMENTATION
```
#include<bits/stdc++.h>
using namespace std;
void
MaxBottomupheapify (int H[], int i)
{
  int p = (i - 1) / 2, t;
  int temp;

  while (p > -1)
    {
      if (H[i] > H[p])
	{
	  temp = H[i];
	  H[i] = H[p];
	  H[p] = temp;
	  i = p;
	  p = (i - 1) / 2;

	}

      else
	p = -1;
    }

}

void
MaxTopdownheapify (int H[], int i, int n)
{
  int c, t,temp;

  while (2 * i + 2 < n)
    {

      if (H[2 * i + 1] > H[2 * i + 2])
	c = 2 * i + 1;
      else
	c = 2 * i + 2;
      if (H[i] < H[c])
	{
	  temp = H[i];
	  H[i] = H[c];
	  H[c] = temp;
	  i = c;
	}

      else
	i = n;
    }
  c = 2 * i + 1;
  if (c < n & H[i] < H[c])
    {
      temp = H[i];
      H[i] = H[c];
      H[c] = temp;
      i = c;
    }

}

void
MaxAdd (int H[], int X, int *n)
{

  H[*n] = X;
  *n = *n + 1;

  MaxBottomupheapify (H, *n - 1);
}

void
DeleteMax (int H[], int *n)
{
  int t;
  
  *n = *n - 1;
  t = H[0];
  H[0] = H[*n];
  H[*n] = t;
  MaxTopdownheapify (H, 0, *n);
}

void
MaxBuildHeap (int H[],  int n)
{

  int i = n / 2;
  while (i > -1)
    {
      MaxTopdownheapify (H, i--, n);
    }

}

void
Bottomupheapify (int H[],  int i)
{
  int p = (i - 1) / 2, temp;

  while (p > -1)
    {
      if (H[i] < H[p])
	{
	  temp = H[i];
	  H[i] = H[p];
	  H[p] = temp;
	  i = p;
	  p = (i - 1) / 2;

	}

      else
	p = -1;
    }

}

void
Topdownheapify (int H[],  int i, int n)
{
  int c, temp;

  while (2 * i + 2 < n)
    {

      if (H[2 * i + 1] < H[2 * i + 2])
	c = 2 * i + 1;
      else
	c = 2 * i + 2;
      if (H[i] > H[c])
	{
	  temp = H[i];
	  H[i] = H[c];
	  H[c] = temp;
	  i = c;
	}

      else
	i = n;
    }
  c = 2 * i + 1;
  if (c < n & H[i] > H[c])
    {
      temp = H[i];
      H[i] = H[c];
      H[c] = temp;
    }

}

void
Add (int H[], int X, int *n)
{

  H[*n] = X;
  *n = *n + 1;

  Bottomupheapify (H, *n - 1);
}

void
DeleteMin (int H[],  int *n)
{
  
  int t;
  *n = *n - 1;
  t = H[0];
  H[0] = H[*n];
  H[*n] = t;
  Topdownheapify (H,0,*n);
}

void
BuildHeap (int H[],  int n)
{

  int i = n / 2;
  while (i > -1)
    {
      Topdownheapify (H, i--, n);

    }

}

void
DecreaseKey (int H[],  int i, int X)
{

  H[i] = X;

  Bottomupheapify (H, i);


}

void
IncreaseKey (int H[],  int i, int X)
{

  H[i] = X;

  MaxBottomupheapify (H, i);


}

void
HeapSort (int H[],  int n)
{

  int m=n,i;
  BuildHeap(H,n);
  for(i=0;i<n;++i) DeleteMin(H,&m);

  for(i=0;i<n-1;++i) if(H[i]<H[i+1]) cout<<"Problem";

}

int main()
{
    int H[60000],i,j,n;
    cin>>n;
    for(i=0;i<n;++i) H[i]=32000-rand()%61234;

    HeapSort(H,n);
    return 0;
}


```
* * *
KTH LARGEST ELEMENT
https://leetcode.com/problems/kth-largest-element-in-an-array/
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        
        priority_queue<int> PQ;

        for(int i:nums)
        {
            PQ.push(i);
        }
        int t=k-1;
        while(t--)
        {
            PQ.pop();
        }
        return PQ.top();

    }
};
```

```
class Solution {
public:
    int partition(vector<int>& nums,int left,int right)
    {
        int pivot=nums[left];
        int l=left+1;
        int r=right;
        while(l<=r)
        {
            if(pivot < nums[r] && pivot > nums[l])
            {
                swap(nums[l],nums[r]);
                l++;
                r--;
            }
            if(nums[l]>=pivot)
            {
                l++;
            }
            if(nums[r]<=pivot)
            {
                r--;
            }  
        }
        swap(nums[r],nums[left]);
        return r;
    }
	
    int findKthLargest(vector<int>& nums, int k) {
        
        int left=0,right=nums.size()-1;
        int KTH;
        while(1)
        {
        int idx=partition(nums,left,right);
        if(idx==k-1)
        {
            KTH=nums[idx];
            break;
        }
        if(idx < k-1)
        {
            left=idx+1;
        }
        else
        {
            right=idx-1;
        }
        }
        return KTH;
    }
};
```
* * *

MAXIMUM SUM COMBINATION
https://www.interviewbit.com/problems/maximum-sum-combinations/
```
vector<int> Solution::solve(vector<int> &A, vector<int> &B, int C) {
    
    vector<int> R;
    priority_queue<pair<int,pair<int,int>>> p;
    
    sort(A.begin(),A.end());
    sort(B.begin(),B.end());
    
    int N=B.size();
    for(int i=0;i<A.size();i++)
    {
        p.push({A[i]+B[N-1],{i,N-1}});
    }
    
   while(C-- && !p.empty())
    {
        pair<int,pair<int,int>> t=p.top();
        int data=t.first;
        int i=t.second.first;
        int j=t.second.second;
        
        p.pop();
        
        R.push_back(data);
        
        if(j!=0)
        {
            p.push({A[i]+B[j-1],{i,j-1}});
        }
    }
    return R;
}
```
* * *

FIND MEDIAN FROM DATA STREAM
https://leetcode.com/problems/find-median-from-data-stream/
```
class MedianFinder {
public:
    priority_queue <int> HS;
    priority_queue <int,vector <int>, greater <int>> HB;
    MedianFinder() {
    }
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
* * *

MERGE K SORTED ARRAYS

https://www.codingninjas.com/codestudio/problems/merge-k-sorted-arrays_975379
```
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,pair<int,int>> ppi; 
vector<int> mergeKSortedArrays(vector<vector<int>>&kArrays, int k)
{
    // Write your code here. 
    vector<int> output;
    priority_queue<ppi,vector<ppi>,greater<ppi>> p;
    for(int i=0;i<kArrays.size();i++)
    {
        p.push({kArrays[i][0],{i,0}});
    }

    while(!p.empty())
    {
        ppi t=p.top();
        p.pop();

        int i=t.second.first;
        int j=t.second.second;

        output.push_back(t.first);
         if(j < kArrays[i].size()-1)
         {
             p.push({kArrays[i][j+1],{i,j+1}});
         }
    }
    return  output;

}
```
* * *

K MOST FREQUENT ELEMENTS
https://leetcode.com/problems/top-k-frequent-elements/
```
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        
        unordered_map<int,int> M;
        vector<int> answer;
        for(auto x:nums)
        {
            M[x]++;
        }
        priority_queue<pair<int,int>> PQ;

        for(auto it=M.begin();it!=M.end();it++)
            {
                PQ.push({it->second,it->first});

                if(PQ.size() > M.size()-k)
                {
                    answer.push_back(PQ.top().second);
                    PQ.pop();
                }
            }
            return answer;
    }
};
```
* * *