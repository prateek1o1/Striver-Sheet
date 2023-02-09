# DYNAMIC PROGRAMMING

MAXIMUM PRODUCT SUBARRAY
https://leetcode.com/problems/maximum-product-subarray/
```
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        
        int n=nums.size();
        int p=1;
        int t=INT_MIN;

        for(int i=0;i<n;i++)
        {   
            p=p*nums[i];
            t=max(p,t);
            if(nums[i]==0)
                p=1;
        }
        p=1;
        for(int i=n-1;i>=0;i--)
        {   
            p=p*nums[i];
            t=max(p,t);

            if(nums[i]==0)
                p=1;
        }
        return t;
    }
};
```

```
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        
        int n=nums.size();
        int small=nums[0];
        int big=nums[0];
        int t=nums[0];

        for(int i=1;i<n;i++)
        {   
            if(nums[i]<0)
                swap(big,small);
            
            big=max(nums[i],nums[i]*big);
            small=min(nums[i],nums[i]*small);

            t=max(t,big);
        }
        return t;
    }
};
```

LONGEST INCREASING SUBSEQUENCE
https://leetcode.com/problems/longest-increasing-subsequence/
```
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n=nums.size();
        vector<int> dp(n,1);
        int answer=0;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<i;j++)
                {
                    if(nums[i] > nums[j] && 1+dp[j] > dp[i])
                        {
                            dp[i]=1+dp[j];
                        }
                }
                  answer=max(answer,dp[i]);
        }
        return answer;
    }
};
```
TC=$O(n)$
```
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n=nums.size();
        vector<int> K;
        int answer=0;
        int length=1;
        K.push_back(nums[0]);

        for(int i=1;i<n;i++)
        {
            if(nums[i]>K.back())
            {
                K.push_back(nums[i]);
                length++;
            }
            else
            {
                int j=lower_bound(K.begin(),K.end(),nums[i]) - K.begin();
                K[j]=nums[i];
            }
        }
        return length;
    }
};
```
TC= $O(n*log(n))$

LONGEST COMMON SUBSEQUENCE
https://leetcode.com/problems/longest-common-subsequence/

Memoization
```
class Solution {
public:
    int recursion(int i,int j,string &text1, string &text2,vector<vector<int>> &dp)
    {
        if(i<0 || j<0)
            return 0;

        if(dp[i][j] != -1) return dp[i][j];

        if(text1[i]==text2[j])
        {
            return dp[i][j]=1+recursion(i-1,j-1,text1,text2,dp);
        }
        else
        {
            return dp[i][j]=max(recursion(i,j-1,text1,text2,dp),recursion(i-1,j,text1,text2,dp));
        }
    }
    int longestCommonSubsequence(string text1, string text2) {
        int n=text1.size();
        int m=text2.size();

        vector<vector<int>> dp(n,vector<int>(m,-1));
       return recursion(n-1,m-1,text1,text2,dp);
    }
};
```
Tabulation
```
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n=text1.size();
        int m=text2.size();

        vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
        for(int i=0;i<n+1;i++)
            dp[i][0]=0;

        for(int j=0;j<m+1;j++)
            dp[0][j]=0;

        for(int i=1;i<=n;i++)
            {
                for(int j=1;j<=m;j++)
                    {
                        if(text1[i-1]==text2[j-1])
                        {
                            dp[i][j]=1+dp[i-1][j-1];
                        }
                        else
                        {
                            dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
                        }
                    }
            }
       return dp[n][m];
    }
};
```

0-1 KNAPSACK
https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1

Memoization
```
class Solution
{
    public:
    //Function to return max value that can be put in knapsack of capacity W.
    int recursion(int i, int j,vector<vector<int>> &dp,int wt[],int val[],int n,int W)
    {
        if(i==0)
        {
        if(wt[i]<=j) return val[i];
        
        return 0;
        }
        
        
        if(dp[i][j]!=-1) return dp[i][j];
        int take=-1e9;
        
        if(j-wt[i]>=0)   
            take=recursion(i-1,j-wt[i],dp,wt,val,n,W)+val[i];
            
            int nottake=recursion(i-1,j,dp,wt,val,n,W);
        
            return dp[i][j]=max(take,nottake);
        
    }
    int knapSack(int W, int wt[], int val[], int n) 
    { 
       // Your code here
       vector<vector<int>> dp(n,vector<int>(W+1,-1));
       return recursion(n-1,W,dp,wt,val,n,W);
    }
};
```

Tabulation
```
class Solution
{
    public:
    //Function to return max value that can be put in knapsack of capacity W.

    int knapSack(int W, int wt[], int val[], int n) 
    { 
       // Your code here
       vector<vector<int>> dp(n,vector<int>(W+1,0));
       //return recursion(n-1,W,dp,wt,val,n,W);
        
        int k=wt[0];
        for(;k<W+1;k++)
            dp[0][k]=val[0];
            
        for(int i=1;i<n;i++)
        {
            for(int j=1;j<=W;j++)
            {
                int take=-1e9;
                if(j-wt[i]>=0) take=dp[i-1][j-wt[i]]+val[i];
                
                int nottake=dp[i-1][j];
                
                dp[i][j]=max(take,nottake);
            }
        }
        return dp[n-1][W];
    }
};
```

EDIT DISTANCE
https://leetcode.com/problems/edit-distance/
```
class Solution {
public:

    int Memoization(int i,int j,vector<vector<int>> &dp,string &word1,string &word2)
    {
        if(i<0) return j+1;
        
        if(j<0) return i+1;

        if(dp[i][j]!=-1) return dp[i][j];

        if(word1[i]==word2[j]) return dp[i][j]=Memoization(i-1,j-1,dp,word1,word2);

        return dp[i][j]=min(min(1+Memoization(i-1,j,dp,word1,word2),1+Memoization(i,j-1,dp,word1,word2)),1+Memoization(i-1,j-1,dp,word1,word2));
          
    }
    int minDistance(string word1, string word2) {
        
        int m=word1.size();
        int n=word2.size();
         
         vector<vector<int>> dp(m,vector<int>(n,-1));

         return Memoization(m-1,n-1,dp,word1,word2);
    }
};
```

MAXIMUM SUM INCREASING SUBSEQUENCE
https://practice.geeksforgeeks.org/problems/maximum-sum-increasing-subsequence4749/1
```
class Solution{
	public:
	int Memoization(int i,int j, int arr[],int n,vector<vector<int>> &dp)
	{
	    if(i==n) return 0;
	    
	    if(dp[i][j+1]!=-1) return dp[i][j+1];
	    
	    int take=-1e9;
	    if(arr[i]>arr[j])
	        take=arr[i]+Memoization(i+1,i,arr,n,dp);
	    
	    int nottake=Memoization(i+1,j,arr,n,dp);
	    
	    return dp[i][j+1]=max(take,nottake);
	}
	int maxSumIS(int arr[], int n)  
	{  
	    // Your code goes here
	    vector<vector<int>> dp(n,vector<int>(n+1,-1));
	    return Memoization(0,-1,arr,n,dp);
	    
	}  
};
```

MATRIX CHAIN MULTIPLICATION (Partitioning Dynamic Programming)
https://practice.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1

```
class Solution{
public:
    int matrixMultiplication(int N, int arr[])
    {
        vector<vector<int>> dp(N,vector<int>(N,0));
        
        for(int i=N-1;i>=1;i--)
        {
            for(int j=i+1;j<=N-1;j++)
            {
                int m=1e9;
                for(int k=i;k<j;k++)
                {
                    int x=arr[i-1]*arr[k]*arr[j]+dp[i][k]+dp[k+1][j];
                    
                    if(m > x)
                        m=x;
                }
                dp[i][j]=m;
            }
        }
        return dp[1][N-1];
    }
};
```