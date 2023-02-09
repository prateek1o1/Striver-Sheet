# ARRAYS 

SET MATRIX ZERO
https://leetcode.com/problems/set-matrix-zeroes/

```
class
public:
    void setZeroes(vector<vector<int>>& arr) {
        int rowZero = 1;
        int colZero = 1;
        int n = arr.size() , m = arr[0].size();
        for(int i = 0 ; i < n ; i++) {
            if(arr[i][0] == 0){
                rowZero = 0;
                break;
            }
        }
        for(int j = 0 ; j < m ; j++){
            if(arr[0][j] == 0){
                colZero = 0;
                break;
            }
        }
        for(int i = 1 ; i < n ; i++){
            for(int j = 1 ; j < m ; j++){
                if(!arr[i][j]){
                    arr[i][0] = 0;
                    arr[0][j] = 0;
                }
            }
        }
        for(int i = 1 ; i < n ; i++){
            if(!arr[i][0]){
                for(int j = 1 ; j < m ; j++)
                    arr[i][j] = 0;
            }
        }
        for(int j = 1 ; j < m ; j++){
            if(!arr[0][j]){
                for(int i = 1 ; i < n ; i++){
                    arr[i][j] = 0;
                }
            }
        }
      if(!rowZero) for(int i = 0 ; i < n ; i++) arr[i][0] = 0;
      if(!colZero) for(int j = 0 ; j < m ; j++) arr[0][j] = 0;
    }
};
```

* * *

PASCAL’S TRIANGLE
https://leetcode.com/problems/pascals-triangle/

```
class Solution {
public:
    vector<vector<int> > generate(int numRows) {
        vector<vector<int>> r(numRows);

        for (int i = 0; i < numRows; i++) {
            r[i].resize(i + 1);
            r[i][0] = r[i][i] = 1;
  
            for (int j = 1; j < i; j++)
                r[i][j] = r[i - 1][j - 1] + r[i - 1][j];
        }
        
        return r;
    }
};
```

* * *

NEXT PERMUTATION
https://leetcode.com/problems/next-permutation/

```
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
    	int n = nums.size(), k, l;
    	for (k = n - 2; k >= 0; k--) {
            if (nums[k] < nums[k + 1]) {
                break;
            }
        }
    	if (k < 0) {
    	    reverse(nums.begin(), nums.end());
    	} else {
    	    for (l = n - 1; l > k; l--) {
                if (nums[l] > nums[k]) {
                    break;
                }
            } 
    	    swap(nums[k], nums[l]);
    	    reverse(nums.begin() + k + 1, nums.end());
        }
    }
}; 
```

* * *
KADANE’S ALGORITHM 
https://leetcode.com/problems/maximum-subarray/
```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        
        int start=0;
        int current_subarray_sum=0;
        int maximum_sum=INT_MIN;

        int nums_length=nums.size();
        
        for(int i=0;i<nums_length;i++)
        {
            current_subarray_sum+=nums[i];
            
            if(current_subarray_sum>maximum_sum)
            {
                maximum_sum=current_subarray_sum;
            }
            if(current_subarray_sum<0)
            {
                current_subarray_sum=0;
            }
            
        }
        return maximum_sum;
    }
};
```
***
SORT AN ARRAY OF 0’S 1’S 2’S
https://leetcode.com/problems/sort-colors/

```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        
        int freq[3]={0};
        
        for(int i=0;i<nums.size();i++)
        {
            freq[nums[i]]++;
        }
        int j=0;
        for(int i=0;i<3;i++)
        {
          
            while(freq[i]!=0)
            {
                nums[j++]=i;
                freq[i]-=1;
            
            } 
        }
    }
};
```

* * *

STOCK BUY AND SELL
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int i=0;
        int Highest=INT_MIN;
        for(int j=1;j<prices.size();j++)
        {
            if(prices[j]-prices[i]>Highest)
            {
                Highest=prices[j]-prices[i];
            }
            
            if(prices[j]-prices[i]<0)
                i=j;
        }
        if(Highest>0)
        return Highest;
        
        else return 0;
    }
};
```

* * *

# ARRAY 2

ROTATE MATRIX
https://leetcode.com/problems/rotate-image/

```
void rotate(vector<vector<int>>& matrix) {  
int N=matrix.size();
for(int i=1;i<N;i++)
     {
         for(int j=0;j<i;j++)
         {
             swap(matrix[i][j],matrix[j][i]);
         }
     }
for(int k=0;k<N;k++)
        {
           reverse(matrix[k].begin(),matrix[k].end());
        } }
```

* * *

MERGE OVERLAPPING SUBINTERVALS
https://leetcode.com/problems/merge-intervals/

```
vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> born;
        int N=intervals.size();
        sort(intervals.begin(),intervals.end());
                for(int i=0;i<N;i++)
        {
            if(born.empty() || born.back()[1]<intervals[i][0])
            {
                vector <int> v = {intervals[i][0],intervals[i][1]};
                born.push_back(v);
            }
            else
            {
                born.back()[1]=max(intervals[i][1],born.back()[1]);
            }
        }
        return born;
    }
```

* * *

MERGE TWO SORTED ARRAYS WITHOUT EXTRA SPACE

https://leetcode.com/problems/merge-sorted-array/

```
temp[m]=(INT_MAX);
nums2.push_back(INT_MAX);
int l=0,r=0,i=0;   
while(i<(m+n))
        {
       if(temp[l]<=nums2[r] ) {nums1[i]=temp[l]; l++; }
       else {  nums1[i]=nums2[r]; r++; }
       i++;
       }
```

* * *

```
int gap = ceil((float)(n + m) / 2); 
while (gap > 0) { int i = 0; int j = gap; 
while (j < (n + m)) 
{ if (j < n && ar1[i] > ar1[j]) { swap(ar1[i], ar1[j]); } 
else if (j >= n && i < n && ar1[i] > ar2[j - n]) { swap(ar1[i], ar2[j - n]); } 
else if (j >= n && i >= n && ar2[i - n] > ar2[j - n]) { swap(ar2[i - n], ar2[j - n]); } j++; i++; } 
if (gap == 1) 
{ gap = 0; } 
else { gap = ceil((float) gap / 2); } }
```

* * *

FIND DUPLICATE IN AN ARRAY OF N+1 INTEGERS

https://leetcode.com/problems/find-the-duplicate-number/

```
int findDuplicate(vector<int>& nums) {
        unordered_set <int> h;
        int x;
        for(int i=0;i < nums.size();i++)
        { if(h.find(nums[i])==h.end())
            {    h.insert(nums[i]);
            }
            else
            {
                x=nums[i];
            }}
        return x;
       }
```

* * *

REPEAT AND MISSING NUMBER
https://www.interviewbit.com/problems/repeat-and-missing-number-array

```
long long int n,S1,SQ1,a=0,b=0; 
n=A.size(); S1=(n*(n+1))/2; 
SQ1=(n*(n+1)*(2*n+1))/6; 
for(int i=0;i<n;i++) 
{ SQ1-=(long long int) A[i]* (long long int) A[i]; 
S1-=(long long int) A[i]; } 
b = (SQ1/S1 + S1)/2; 
a= b-S1;
```

* * *

COUNT INVERSION
https://www.codingninjas.com/codestudio/problems/count-inversions_615

```
long long merge (long long * arr,long long *temp,int left,int mid,int right)
{
    long long int inversion=0;
    long long int i,j,k;
    i=left,j=mid,k=left;
    while((i<=mid-1) && (j<=right))
    {
        if(arr[i]<=arr[j])
            temp[k++]=arr[i++];
        else
        {
            temp[k++]=arr[j++];
            inversion=inversion+(mid-i);
        }
    }
    while(i <= mid - 1)
        temp[k++] = arr[i++];

    while(j <= right)
        temp[k++] = arr[j++];

    for(long long int r = left ; r <= right ; r++)
        arr[r] = temp[r];
    
    return inversion;
}

long long mergesort (long long * arr,long long *temp,int left,int right)
{
    long long int mid,inversion=0;
    if(left<right)
    {
        mid=(left+right)/2;
        inversion+=mergesort(arr,temp,left,mid);
        inversion+=mergesort(arr,temp,mid+1,right);
        inversion+=merge(arr,temp,left,mid+1,right);
    }
    return inversion;
}

long long getInversions(long long *arr, int n){
    // Write your code here.
    long long int temp[n];
    mergesort(arr,temp,0,n-1);
}
```

* * *

# ARRAY 3

SEARCH IN A 2-D MATRIX

https://leetcode.com/problems/search-a-2d-matrix/

```
bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m,n,mid,left,right;      
        m=matrix.size();
        n=matrix[0].size();
        left=0;
        right=(m*n)-1;
        while(left<=right)
        {
            mid=(left+right)/2;
            if(matrix[mid/n][mid%n]==target)
                return true;
             else if(matrix[mid/n][mid%n]>target)
                right=mid-1;
            else
                left=mid+1;
        }
       return false;
    }
```

* * *

POW(X,N)
https://leetcode.com/problems/powx-n/

```
while(t_exp>0)
        {
            if(t_exp%2==1)
                y=y*x_num;
            
            x_num=x_num*x_num;
            t_exp=t_exp/2;
        }
```

* * *

MAJORITY ELEMENT(>N/2)
https://leetcode.com/problems/majority-element/

# MOORE’S VOTING ALGORITHM

```
int majorityElement(vector<int>& nums) {
        int n=nums.size();
        int numerate=0,key;
        for(int i=0;i<n;i++)
        {  if(numerate== 0)
                key= nums [i];    
            if(key==nums[i])
                numerate+=1;
            else
                numerate-=1;
        }
       return key; 
    }
```

* * *

MAJORITY ELEMENT(>N/3)
https://leetcode.com/problems/majority-element-ii/

# EXTENDED MOORE’S VOTING ALGORITHM

```
vector<int> majorityElement(vector<int>& nums) {
        int count1=0,count2=0,num1=INT_MIN,num2=INT_MIN;
        int len=nums.size();
        for(int i=0;i<len;i++)
        {
        if(num1== nums[i])
           count1++;     
       else if(num2== nums[i])
            count2++;     
        else if(count1== 0)
        {
          num1=nums[i];
          count1=1;
        }
         else if(count2== 0)
         {
            num2=nums[i];
            count2=1;   
         }     
        else
        {  count1-=1;
            count2-=1;
        }
        }
        count1=0;
        count2=0;
        for(int i=0;i<len;i++)
        {
            if(num1== nums[i])
                count1++;
            if(num2== nums[i])
                count2++;
        }
        vector <int> resp;
        if(count1 > len/3)
            resp.push_back(num1);
        if(count2 > len/3)
            resp.push_back(num2);
        
        return resp; 
    }
```

* * *

GRID UNIQUE PATHS
https://leetcode.com/problems/unique-paths/

```
int uniquePaths(int m, int n) {
        int p=m+n-2, q=n-1;
        double result=1;
        for(int k=1;k<=q;k++)
        {result=result*(p-q+k)/k;
        }
        return result;
    }
```

* * *

REVERSE PAIRS
https://leetcode.com/problems/reverse-pairs/

```
int merge (vector<int> &arr,int left,int mid,int right)
{
    int t=0;
    int i,j,k;
    int w=mid+1;
    for (int q = left; q <= mid; q++) 
{
    while (w <= right && arr[q] > 2 * (long long) arr[w]) 
    {
  	    	w++;
  	}
    t += (w - (mid+1));
  }
    i=left,j=mid+1,k=left;
    vector<int> temp;
    while((i<=mid) && (j<=right))
    {
        if(arr[i]<=arr[j])
        {
            temp.push_back(arr[i++]);
        }
        else
        {
            temp.push_back(arr[j++]);
        }
    }
    while(i <= mid)
        temp.push_back(arr[i++]);
    while(j <= right)
        temp.push_back(arr[j++]);
    for(int r = left ; r <= right ; r++)
        arr[r] = temp[r-left];
    return t;
}
int mergesort (vector <int> &arr,int left,int right)
{
    int mid,inversion=0;
    if(left<right)
    {
        mid=(left+right)/2;
        inversion=mergesort(arr,left,mid);
        inversion+=mergesort(arr,mid+1,right);
        inversion+=merge(arr,left,mid,right);
    }
    return inversion;
}

int reversePairs(vector<int>& nums) {
    return mergesort(nums,0,nums.size()-1);
    }
```

* * *

# ARRAY 4

2-SUM PROBLEM
https://leetcode.com/problems/two-sum/

```
vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map <int,int> h;
        int last=nums.size();
        vector <int> answer;
        for(int i=0;i<last;i++)
        {
            if(h.find(target-nums[i])!=h.end())
            {
                answer.push_back(i);
                answer.push_back(h[target-nums[i]]);
                break;
            }
            h[nums[i]]=i;
        }     
        return answer;
```

* * *

4-SUM PROBLEM
https://leetcode.com/problems/4sum/

```
vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int N= nums.size();  
        sort(nums.begin(),nums.end());
       set<vector<int>> myset;
        for(int i=0;i<N;i++)
        {
            for(int j=i+1;j<N;j++)
            {
                for(int k=j+1;k<N;k++)
                { long long int x = (long long)target-                   (long long)nums[i]-
                  (long long)nums[j]-                                     (long long)nums[k];      
                        if(binary_search(nums.begin()+k+1,nums.end(),x))
                                                    {
                            vector<int> p;
                            p.push_back(nums[i]);
                            p.push_back(nums[j]);
                            p.push_back(nums[k]);
                            p.push_back(x);
                            sort(p.begin(),p.end());
                            myset.insert(p);
                        }
                }
            }
        }
        vector<vector<int>> ans(myset.begin(),myset.end());
        return ans;
```

* * *

TWO POINTER APPROACH

```
vector<vector<int>> fourSum(vector<int>& num, int target) 
{ 
vector<vector<int> > res; 
if (num.empty()) return res; 
int n = num.size(); 
sort(num.begin(),num.end());
 
for (int i = 0; i < n; i++) 
{ int target_3 = target - num[i]; 
for (int j = i + 1; j < n; j++) 
{ 
int target_2 = target_3 - num[j]; 
int front = j + 1; int back = n - 1; 

while(front < back) { 
int two_sum = num[front] + num[back]; 
if (two_sum < target_2) front++; 
else if (two_sum > target_2) back--; 
else { vector<int> quadruplet(4, 0); 
quadruplet[0] = num[i]; quadruplet[1] = num[j]; 
quadruplet[2] = num[front]; quadruplet[3] = num[back]; res.push_back(quadruplet); 

// Processing the duplicates of number 3 
while (front < back && num[front] == quadruplet[2]) ++front; 

// Processing the duplicates of number 4 
while (front < back && num[back] == quadruplet[3]) --back; 
} } 
// Processing the duplicates of number 2 
while(j + 1 < n && num[j + 1] == num[j]) ++j; } 

// Processing the duplicates of number 1 
while (i + 1 < n && num[i + 1] == num[i]) ++i; } 
return res; 
}
```

* * *

LONGEST CONSECUTIVE SEQUENCE
https://leetcode.com/problems/longest-consecutive-sequence/

```
int longestConsecutive(vector<int>& nums) {
        unordered_set <int> star;
        for(int i=0;i<nums.size();i++){ star.insert(nums[i]);}
        int maxc=INT_MIN;
        for(int j=0;j<nums.size();j++)
        {   if(star.count(nums[j]-1)==1)
                continue;    
            int k=1;
            int count=1;
            while(star.count(nums[j]+k)==1)
            {  count++; k++;
 	}    
            if(count>maxc)
                maxc=count;
        }
        if(nums.size()==0)
            return  0;
        return maxc;
    }
```

* * *

LARGEST SUB-ARRAY WITH 0 SUM

https://practice.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1

```
int maxLen(vector<int>&A, int n)
   {  vector <int> pfx;
       int p=0;
       for(int i=0;i<n;i++)
       {   p=p+A[i];
           pfx.push_back(p);
       }
       unordered_map <int,int> fun;
       int large=0;
       fun[0]=-1;
       for(int j=0;j<n;j++)
       {
           if(fun.find(pfx[j])!=fun.end())
           {
               if((j-fun[pfx[j]])>large)
               large=j-fun[pfx[j]];
           }
           else
               fun[pfx[j]]=j;
       }
       return large;
       }
```

* * *

COUNT NUMBER OF SUB-ARRAY WITH XOR K

https://www.interviewbit.com/problems/subarray-with-given-xor/

```
int Solution::solve(vector<int> &A, int B) { int n=A.size(); 
vector <int> pfx; int p=0; 
for(int i=0;i<n;i++) 
{ p=p^A[i]; pfx.push_back(p); 
} 
unordered_map <int,int> fish; 
fish[0]=1; int subarr=0; 
for(int i=0;i<n;i++) 
{ if( fish.find(pfx[i]^B)!=fish.end()) 
{ subarr+=fish[pfx[i]^B]; 
} 
fish[pfx[i]]++; 
} 
return subarr; 
}
```

* * *

LONGEST SUBSTRING WITHOUT REPEATING CHARACTERS https://leetcode.com/problems/longest-substring-without-repeating-characters/

```
int lengthOfLongestSubstring(string s) {
        int n=s.length(); unordered_set <int> dupe; int maxc=INT_MIN; int left=0;
        for(int i=0;i<n;i++)
        {  if(dupe.find(s[i])!=dupe.end())
            {  while(left<i && dupe.find(s[i])!=dupe.end())
            {   dupe.erase(s[left]);      left++;
           }}
            dupe.insert(s[i]); maxc=max(maxc,i-left+1);}    
    if(n==0)return 0;
    else  return maxc; }
***
```