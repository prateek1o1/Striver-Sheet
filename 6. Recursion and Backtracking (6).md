# RECURSION AND BACKTRACKING

PRINT ALL PERMUTATIONS OF STRING/ARRAY
https://leetcode.com/problems/permutations/
```
class Solution {
public:
    void recursion(int i,vector<int> &nums,vector<vector<int>> &answer)
    {
        if(i==nums.size())
        {
            answer.push_back(nums);
            return;
        }

        for(int j=i;j<nums.size();j++)
        {
            swap(nums[i],nums[j]);
            recursion(i+1,nums,answer);
            swap(nums[i],nums[j]);
        }
    }    
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> answer;
        recursion(0,nums,answer);
        return answer;
    }
};
```
TC=$O(N! * N)$

Iterative approach
```
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        sort(nums.begin(),nums.end());
        do{
            ans.emplace_back(nums);
        }while(next_permutation(nums.begin(),nums.end()));
        return ans;
    }
};
```
Time complexity: O(n!+nlogn) ~ O(n!)
Space complexity: O(1)
* * *
N QUEENS PROBLEM
https://leetcode.com/problems/n-queens/
```
class Solution {
public:
    void recursion(int col,int n,vector<vector<string>> &answer,vector<string> &board,vector <int>&ldiag,vector <int>&udiag,vector <int>&lrow)
    {
        if(col==n)
        {
            answer.push_back(board);
            return;
        }

        for(int row=0;row<n;row++)
        {
            if(ldiag[row+col]==0 && udiag[n-1+row-col]==0 && lrow[row]==0)
            {
                board[row][col]='Q';
                lrow[row]=1;
                ldiag[row+col]=1;
                udiag[n-1+row-col]=1;
                recursion(col+1,n,answer,board,ldiag,udiag,lrow);
                board[row][col]='.';
                lrow[row]=0;
                ldiag[row+col]=0;
                udiag[n-1+row-col]=0;
            }
        }
    }

    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> answer;
        vector<string> board(n);
        vector<int> ldiag(2*n-1,0),udiag(2*n-1,0),lrow(n,0);
        string s(n,'.');
        for(int i=0;i<n;i++)
        {
            board[i]=s;
        }

        recursion(0,n,answer,board,ldiag,udiag,lrow);
        return answer;
    }
};
```
TC=$O(N! * N)$
* * *
SUDOKU SOLVER
https://leetcode.com/problems/sudoku-solver/
```
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {
        recursion(board);
    }
    bool recursion(vector<vector<char>> &board)
    {
        for(int i=0;i<board.size();i++)
        {
            for(int j=0;j<board[0].size();j++)
            {
                if(board[i][j]=='.')
                {
                    for(char c='1';c<='9';c++)
                    {
                        if(iscorrect(board,i,j,c))
                        {
                            board[i][j]=c;
                            if(recursion(board)==true)
                                return true;
                            else
                                board[i][j]='.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    bool iscorrect(vector<vector<char>> &board,int row,int col,char c)
    {
        for(int i=0;i<9;i++)
        {
            if(board[row][i]==c) return false;

            if(board[i][col]==c) return false;

            if(board[3 * (row/3) + i/3][3 * (col/3) + i%3]==c) return false;
        }
            return true;
    }
};
```
TC= $O(9^{n^2})$
* * *
M COLORING PROBLEM
https://practice.geeksforgeeks.org/problems/m-coloring-problem-1587115620/1#
```
class Solution{
public:
    // Function to determine if graph can be coloured with at most M colours such
    // that no two adjacent vertices of graph are coloured with same colour.
    bool check(int node,int color[],bool graph[101][101],int i,int n)
    {
        for(int k=0;k<n;k++)
        {
            if(k!=node && graph[k][node]==1 && color[k]==i)
            {
                return false;
            }
        }
        return true;
    }
    bool recursion(int node,int color[],bool graph[101][101],int m,int n)
    {
        if(node==n)
        return true;
        
        for(int i=1;i<=m;i++)
        {
            if(check(node,color,graph,i,n))
            {
                color[node]=i;
                if(recursion(node+1,color,graph,m,n)) return true;
                color[node]=0;
            }
        }
        return false;
        
    }
    bool graphColoring(bool graph[101][101], int m, int n) {
        // your code here
        int color[n]={0};
        
        return recursion(0,color,graph,m,n);
        
    }
};
```
TC=$O(N^M)$
* * *
RAT IN A MAZE
https://practice.geeksforgeeks.org/problems/rat-in-a-maze-problem/1
```
// User function template for C++

class Solution{
    public:
    void recursion(int i,int j,int n,int di[],int dj[],string s,vector<string> &paths,vector<vector<int>> &m,vector <vector<int>> &visited)
    {
        if(i==n-1 && j==n-1)
        {
            paths.push_back(s);
            return;
        }
        string where="LRDU";
        
        for(int k=0;k<4;k++)
        {
            int l=i+di[k];
            int r=j+dj[k];
            
            if(l>=0 && l<n && r>=0 && r<n && m[l][r]==1 && !visited[l][r])
            {
                 visited[i][j]=1;
                 recursion(l,r,n,di,dj,s+where[k],paths,m,visited);
                 visited[i][j]=0;
            }
        }
        
        
    }
    vector<string> findPath(vector<vector<int>> &m, int n) {
        // Your code goes here
        vector<string> paths;
        string s;
        int di[]={0,0,1,-1};
        int dj[]={-1,1,0,0};
        
        vector<vector<int>> visited(n,vector<int>(n,0));
      
        if(m[0][0]==1)
        recursion(0,0,n,di,dj,s,paths,m,visited);
        
        return paths;
    }
};
```

TC=$O(4^{m*n})$
* * *
WORD BREAK
https://www.codingninjas.com/codestudio/problems/word-break_1094901?topList=striver-sde-sheet-problems
```
#include <bits/stdc++.h>
bool recursion(int i,string & target,unordered_set <string> &wordset,vector<int> &dp)
{
    if(i==target.size())
    {
        return dp[i]=1;
    }
    if(dp[i]!=-1)
    { return dp[i];
    }
    
    for(int j=i+1;j<=target.size();j++)
    {
     if (wordset.find(target.substr(i,j-i))!=wordset.end()) {
          if(recursion(j,target, wordset,dp))
            {    
              return dp[i]=1;
            }
         }
    }
    return dp[i]=0;
}
bool wordBreak(vector < string > & arr, int n, string & target) {
    // Write your code here.
    unordered_set <string> wordset;
    for(s:arr)
    {
        wordset.insert(s);
    }
    vector<int> dp(target.size()+1,-1);
    return recursion(0,target,wordset,dp);
}
```
TC=$O(N^2)$
* * *