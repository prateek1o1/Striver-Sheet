# BINARY SEARCH

THE NTH ROOT OF AN INTEGER USING BINARY SEARCH
https://www.codingninjas.com/codestudio/problems/nth-root-of-m_1062679?topList=striver-sde-sheet-problems
```
#include <bits/stdc++.h>
double multiply(double a,int n)
	{
		double R=1.0;
		for(int i=1;i<=n;i++)
			{
				R*=a;
			}
		return R;
	}
	 
double findNthRootOfM(int n, int m) {
	// Write your code here.
	double lo=1,hi=m;
	double check=1e-9;
	double mid;
	
	while(hi-lo > check)
	{
		mid=(hi+lo)/2.0;

		if(multiply(mid,n) < m)
			lo=mid;
		else
			hi=mid;
	}
	return lo;
}
```
* * *
MATRIX MEDIAN
https://www.codingninjas.com/codestudio/problems/873378
```
int upperbound(vector<int> &A,int u)
    {
        int lo=0;
        int hi=A.size()-1;
        int mid;
        while(lo <= hi)
        {
            mid=lo+((hi-lo)/2);
            if(A[mid]<=u)
                lo=mid+1;
            else
                hi=mid-1;
        }
        return lo;
    }
int Solution::findMedian(vector<vector<int> > &A) {
    
    int n=A.size();
    int m=A[0].size();
    
    int lo=1;
    int hi=1e9;
    int mid;
    while(lo<=hi)
    {
        mid=lo+((hi-lo)/2);
        int count=0;
        for(int i=0;i<n;i++)
            {
                count+=upperbound(A[i],mid);
            }
        if(count <= (n*m)/2)
            lo=mid+1;
        else
            hi=mid-1;
            
    }
    return lo;
}

```
* * *
FIND THE ELEMENT THAT APPEARS ONCE IN A SORTED ARRAY, AND THE REST ELEMENT APPEARS TWICE
https://leetcode.com/problems/single-element-in-a-sorted-array/
```
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        
        int n=nums.size();
        int lo=0,hi=n-1;
        int m;
        while(lo < hi)
        {
            m=lo+((hi-lo)/2);

            if(nums[m]==nums[m^1])
            {
                lo=m+1;
            }
            else
            {
                hi=m;
            }
        }
        return nums[lo];
    }
};
```
* * *
SEARCH ELEMENT IN A SORTED AND ROTATED ARRAY/ FIND PIVOT WHERE IT IS ROTATED
https://leetcode.com/problems/search-in-rotated-sorted-array/

Solution-1
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        
        int low=0,high=nums.size()-1,mid;

        while(low<=high)
        {
            mid=low+((high-low)/2);

            if(target==nums[mid]) return mid;

            if(nums[low]<=nums[mid])
            {
                if(nums[low]<=target && nums[mid]>=target)
                    high=mid-1;
                else
                    low=mid+1;
            }
            else
            {
                if(nums[mid]<=target && nums[high] >=target)
                    low=mid+1;
                else
                    high=mid-1;
            }
        }
        return -1;
    }
};
```

Solution-2
```
class Solution {
public:
    int search(vector<int>& nums, int target) {
    int lo = 0, hi = nums.size();
    while (lo < hi) {
        int mid = (lo + hi) / 2;
        int num;   
        if((nums[mid] < nums[0])==(target < nums[0]))
            num=nums[mid];
        else if(target <nums[0])
            num=INT_MIN;
        else
            num=INT_MAX;
                   
        
        if (num == target)
            return mid;
        else if(num < target)    
            lo = mid + 1;
        else
            hi = mid;
    }
    return -1;
    }
};
```
* * *
MEDIAN OF 2 SORTED ARRAYS
https://leetcode.com/problems/median-of-two-sorted-arrays/

```
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        
        int n=nums1.size();
        int m=nums2.size();
        
        if(n>m)
          return findMedianSortedArrays(nums2,nums1);

        int low=0,high=n,k=(m+n+1)/2;
        
        if(n==0)
            return m%2?nums2[m/2]:(nums2[m/2]+nums2[m/2-1])/2.0;
    
        if(m==0)
            return n%2?nums1[n/2]:(nums1[n/2]+nums1[n/2-1])/2.0;
        
        while(low<=high)
        {
            int cut1=(low+high)>>1;
            int cut2=k-cut1;

            int l1= (cut1==0)?INT_MIN:nums1[cut1-1];
            int l2= (cut2==0)?INT_MIN:nums2[cut2-1];
            int r1= (cut1==n)?INT_MAX:nums1[cut1];
            int r2= (cut2==m)?INT_MAX:nums2[cut2];

            if(l1<=r2 && l2<=r1)
            {
                if((m+n)%2!=0)
                    return max(l1,l2);
                else
                    return (max(l1,l2)+min(r1,r2))/2.0;
            }
            else if(l1 > r2)
                high=cut1-1;
            else
                low=cut1+1;
        }
        return 0.0;
    }
};
```
* * *
KTH ELEMENT OF TWO SORTED ARRAYS
https://practice.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array1317/1

```
class Solution{
    public:
int kthElement(int arr1[], int arr2[], int n, int m, int k)
    {
        if(n>m)return kthElement(arr2,arr1,m,n,k);
        int low=max(0,k-m),high=min(k,n);
        while(low<=high){
            int cut1=(low+high)>>1;
            int cut2=k-cut1;
            int l1=cut1==0?INT_MIN:arr1[cut1-1];
            int l2=cut2==0?INT_MIN:arr2[cut2-1];
            int r1=cut1==n?INT_MAX:arr1[cut1];
            int r2=cut2==m?INT_MAX:arr2[cut2];
            if(l1<=r2&&l2<=r1)return max(l1,l2);
            else if(l1>r2) high=cut1-1;
            else low= cut1 +1;
        }
        return 1;
    }
};
```
* * *
ALLOCATE MINIMUM NUMBER OF PAGES
https://www.interviewbit.com/problems/allocate-books/

```
bool ispossible(vector<int> &A,int pages,int students)
{
    int counter=0;
    int allocated=0;
    for(int i=0;i<A.size();i++)
    {
        if(allocated+A[i] > pages)
        {
            counter++;
            allocated=A[i];
            if(allocated > pages) return false;
        }
        else
            allocated+=A[i];
    }
    if(counter < students) 
        return true;
    else    
        return false;
}

int Solution::books(vector<int> &A, int B) {
    if(A.size() < B) return -1;
    int low=A[0],high=0;
    int n=A.size();
    for(int i=0;i<n;i++)
    {
        low=min(low,A[i]);
        high+=A[i];
    }
	
    while(low<=high)
    {
        int mid=low+((high-low)/2);      
        if(ispossible(A,mid,B))
            high=mid-1;
        else
            low=mid+1;
    }
    return low;
}
```
* * *

AGGRESSIVE COWS
https://www.spoj.com/problems/AGGRCOW/

```
#include <bits/stdc++.h>
using namespace std;
 
bool check(int n,vector<int> &stalls,int d,int c)
{
	int counts=1;
	int last=stalls[0];
 
	for(int i=1;i<n;i++)
	{
		if(stalls[i]-last >= d)
		{
			counts++;
			last=stalls[i];
		}
    }
		if(counts>=c) 
			return true;
		
return false;
}
 
int solve()
{
	int n,c;
	cin>>n>>c;
	vector<int> stalls(n,0);
 
	for(auto &i:stalls)
		cin>>i;
	sort(stalls.begin(),stalls.end());
 
	int low=1;
	int high=stalls[n-1]-stalls[0];
 
	while(low<=high)
	{
		int mid=low+((high-low)/2);
 
		if(check(n,stalls,mid,c))
			low=mid+1;
		else
			high=mid-1;
	}
	return high;
}
 
int main() {
	// your code goes here
	int t;
	cin>>t;
	while(t--)
	{
		cout<<solve()<<endl;
	}
	return 0;
}

```
* * *