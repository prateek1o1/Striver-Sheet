# DYNAMIC PROGRAMMING 2

MINIMUM SUM PATH IN THE MATRIX
https://leetcode.com/problems/minimum-path-sum/

1. Memoization
```
class Solution {
public:

    int Memoization(int i,int j,vector<vector<int>>& grid,vector<vector<int>> &dp)
    {
        int infinity= 1e9+7;
        
        if(i==0 && j==0) return grid[i][j];
        
        if(i < 0 || j < 0) return infinity; 
        
        if(dp[i][j]!=-1) return dp[i][j];

        int left=Memoization(i,j-1,grid,dp)+grid[i][j];
        int up=Memoization(i-1,j,grid,dp)+grid[i][j];

        return dp[i][j]=min(left,up);
    }
    int minPathSum(vector<vector<int>>& grid) {

        int m=grid.size();
        int n=grid[0].size();

        vector<vector<int>>dp(m,vector<int>(n,-1));
        
        return Memoization(m-1,n-1,grid,dp);
        //return dp[m-1][n-1];   
    }
};
```

2. Tabulation
```
class Solution {
public:

    int minPathSum(vector<vector<int>>& grid) {

        int m=grid.size();
        int n=grid[0].size();

        vector<vector<int>>dp(m,vector<int>(n,0));

        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(i==0 && j==0) dp[i][j]=grid[i][j];

                else
                {
                
                int left=1e9+7;
                int up=1e9+7;
                if(j>0) left=dp[i][j-1] + grid[i][j]; 
                if(i>0) up=dp[i-1][j] + grid[i][j];

                dp[i][j]=min(left,up);
                }
            }
        }

        return dp[m-1][n-1];   
    }
};
```
COIN CHANGE
https://leetcode.com/problems/coin-change/
```
class Solution {
public:
    int Memoization(int i,int j,vector<vector<int>> &dp,vector<int>& coins)
    {
        if(i==0)
        {
            if(j%coins[i]==0) 
                return j/coins[i];
            return 1e9;
        }
        if(dp[i][j]!=-1) return dp[i][j];

    int take=1e9;
    if(coins[i]<=j) take=1+Memoization(i,j-coins[i],dp,coins);
    
    int leave= Memoization(i-1,j,dp,coins);
    
    return dp[i][j]=min(take,leave);

    }
        
    int coinChange(vector<int>& coins, int amount) {
        int n=coins.size();
        vector<vector<int>> dp(n,vector<int>(amount+1,-1));
        int x=Memoization(n-1,amount,dp,coins);
        if(x>=1e9) 
            return -1;
        else
            return x;
    }
};
```

SUBSET SUM
https://leetcode.com/problems/partition-equal-subset-sum/

1. Memoization
```
class Solution {
public:

    bool Memoization(int i,int j,vector<int> &nums,vector<vector<int>> &dp)
    {
        if(j==0)
            return true;

        if(i==0)
        {
            return nums[i]==j;
        }
        if(dp[i][j]!=-1) return dp[i][j];

        bool include=false;
        bool exclude=Memoization(i-1,j,nums,dp);

        if(j>=nums[i]) 
            include=Memoization(i-1,j-nums[i],nums,dp);
        
        return dp[i][j]=include || exclude;
        
    }
    bool canPartition(vector<int>& nums) {
        
        int k;
        for(auto i:nums)
        {
            k+=i;
        }
        if((k&1) == 1) 
            return false;
        k=k/2;
        int n=nums.size();
        vector<vector<int>> dp(n,vector<int>(k+1,-1));
        return Memoization(n-1,k,nums,dp);
    }
};
```

ROD CUTTING
https://leetcode.com/problems/minimum-cost-to-cut-a-stick/

```
class Solution {
public:

    int Memoization(int i,int j,vector<vector<int>> &dp,vector<int> &cuts)
    {

        if(i>j) return 0;
        if(dp[i][j]!=-1)
            return dp[i][j];
        int small=INT_MAX;
        int T=0;
        for(int k=i;k<=j;k++)
        {
            T=(cuts[j+1]-cuts[i-1])+Memoization(i,k-1,dp,cuts)+Memoization(k+1,j,dp,cuts);
            small=min(small,T);
        }
        return dp[i][j]=small;
    }
    int minCost(int n, vector<int>& cuts) {
        
        int c=cuts.size();
        cuts.insert(cuts.begin(),0);
        cuts.push_back(n);
        sort(cuts.begin(),cuts.end());
        vector<vector<int>> dp(c+1,vector<int>(c+1,-1));
        return Memoization(1,c,dp,cuts);
    }
};
```

EGG DROPPING
https://practice.geeksforgeeks.org/problems/egg-dropping-puzzle-1587115620/1
```
class Solution
{
    public:
    //Function to find minimum number of attempts needed in 
    //order to find the critical floor.
    int Memoization(int i,int j,vector<vector<int>> &dp)
    {
        if(j==0 || j==1)
            return j;
            
        if(i==1)
            return j;
        
        if(dp[i][j]!=-1) 
            return dp[i][j];
            
        int crack,survive,small=INT_MAX,big;
        for(int index=1;index<=j;index++)
        {
            crack=1+Memoization(i-1,index-1,dp);
            survive=1+Memoization(i,j-index,dp);
            
            big=max(crack,survive);
            small=min(small,big);
        }
        return dp[i][j]=small;
    }
    
    int eggDrop(int n, int k) 
    {
        // your code here
        vector<vector<int>> dp(n+1,vector<int>(k+1,-1));
        return Memoization(n,k,dp);
    }
};
```
$TC=O(N*(K^2))$

WORD BREAK
https://practice.geeksforgeeks.org/problems/word-break1352/1
```
class Solution
{
public:
    int Memoization(string A,unordered_set<string> &US,int i,vector<int>&dp)
    {
        if(i==A.size())
            return dp[i]=1;
        if(dp[i]!=-1)
            return dp[i];
            
        for(int k=i+1;k<=A.size();k++)
        {
            if(US.find(A.substr(i,k-i))!=US.end())
            {
                if(Memoization(A,US,k,dp))
                    {
                        return dp[i]=1;
                    }
            }
        }
        return dp[i]=0;
    }
    
    int wordBreak(string A, vector<string> &B) {
        unordered_set<string> US;
        for(auto s:B)
            US.insert(s);
            
        vector<int> dp(A.size()+1,-1);    
        return Memoization(A,US,0,dp);
    }
};
```

PALINDROME PARTITIONING
https://practice.geeksforgeeks.org/problems/palindromic-patitioning4845/1

Memoization
```
// User function Template for C++

class Solution{
public:
    bool check(int i,int j,string s)
    {
         while(i<j)
            {
                if(s[i]!=s[j])
                    return false;
                else
                {   i++;
                    j--;
                }
            }
        return true;
    }
    
int Memoization(int i,int n, vector<int> &dp,string str)
    {    
        if(i==n)
            return 0;
        
        if(dp[i]!=-1)
            return dp[i];
        
        int small=INT_MAX;
        
            for(int j=i;j<n;j++)
            {
                if(check(i,j,str))
                {
                    int cost=1+Memoization(j+1,n,dp,str);
                    
                    small=min(small,cost);
                }
            }
            return dp[i]=small;
    }
    
    int palindromicPartition(string str)
    {
        // code here
        int n=str.size();
        vector<int> dp(n,-1);
        return Memoization(0,n,dp,str)-1;
    }
};
```

MAXIMUM PROFIT IN JOB SCHEDULING
https://practice.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1

```
class Solution 
{
    public:
    //Function to find the maximum profit and the number of jobs done.
    static bool comparision(Job a,Job b)
    {
        return (a.profit > b.profit);
    }
    
    vector<int> JobScheduling(Job arr[], int n) 
    { 
        // your code here
        vector<int> answer;
        sort(arr,arr+n,comparision);
        int last=0;
        
        for(int i=0;i<n;i++)
        {
            last=max(arr[i].dead,last);
        }
        int slots[last+1];
        
        for(int i=0;i<last+1;i++)
        {
            slots[i]=-1;
        }
        
        int number=0;
        int profit=0;
        
        for(int i=0;i<n;i++)
        {
            for(int j=arr[i].dead;j>0;j--)
            {
                if(slots[j]==-1)
                {
                    slots[j]=i;
                    number+=1;
                    profit+=arr[i].profit;
                    break;
                }
            }
        }
        answer.push_back(number);
        answer.push_back(profit);
        
        return answer;
    } 
};
```