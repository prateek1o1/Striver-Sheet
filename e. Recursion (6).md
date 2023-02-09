# RECURSION
SUBSET SUMS
https://practice.geeksforgeeks.org/problems/subset-sums2234/1
```
class Solution
{
public:

    void pickornot(int i,vector<int> &answer,vector<int> &arr,int sum,int N)
    {
        if(i==N)
        {
            answer.push_back(sum);
            return;
        }
        pickornot(i+1,answer,arr,sum+arr[i],N);
        pickornot(i+1,answer,arr,sum,N);
    }
    vector<int> subsetSums(vector<int> arr, int N)
    {
        // Write Your Code here
        vector <int> answer;
        pickornot(0,answer,arr,0,N);
        
        return answer;
    }
};
```
* * *
SUBSET 2
https://leetcode.com/problems/subsets-ii/
```
class Solution {
public:
    void subsetswithoutduplicate(int i,vector<int> &temp,vector<int> &nums,vector<vector<int>>&answer)
    {
        answer.push_back(temp);
        for(int j=i;j<nums.size();j++)
        {
            if(j!=i && nums[j]==nums[j-1]) continue;
            temp.push_back(nums[j]);
            subsetswithoutduplicate(j+1,temp,nums,answer);
            temp.pop_back();
        }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        
        vector<int> temp;
        vector<vector<int>> answer;
        sort(nums.begin(),nums.end());

        subsetswithoutduplicate(0,temp,nums,answer);
        return answer;
    }
};
```
* * *
COMBINATION SUM 1
https://leetcode.com/problems/combination-sum/
```
class Solution {
public:
    void recursion(int i,int target,vector<int> &candidates,vector<int> &tempo,vector<vector<int>> &answer)
    {
        if(i==candidates.size())
        {
            if(target==0)
            answer.push_back(tempo);
            
            return;
        }
    if(target-candidates[i]>=0)
    {   tempo.push_back(candidates[i]);
        recursion(i,target-candidates[i],candidates,tempo,answer);
        tempo.pop_back();
    }
        recursion(i+1,target,candidates,tempo,answer);
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        
        vector<vector<int>> answer;
        vector<int> tempo;
        recursion(0,target,candidates,tempo,answer);
        return answer;
    }
};
```
* * *
COMBINATION SUM 2
https://leetcode.com/problems/combination-sum-ii/
```
class Solution {
public:
    void recursion(int i,int target,vector<int> &candidates,vector<vector<int>> &answer,vector<int> &tempo)
    {
            if(target==0)
            {
            answer.push_back(tempo);
            return;
            }

        for(int j=i;j<candidates.size();j++)
        {
            if(j!=i && candidates[j]==candidates[j-1]) continue;
            if(target < candidates[j]) break;

            tempo.push_back(candidates[j]);
            recursion(j+1,target-candidates[j],candidates,answer,tempo);
            tempo.pop_back();
            
        }
    }
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
       vector<vector<int>> answer;
       vector<int> tempo;
        sort(candidates.begin(),candidates.end());
       recursion(0,target,candidates,answer,tempo);
       return answer; 
    }
};
```
* * *
PALINDROME PARTITIONING
https://leetcode.com/problems/palindrome-partitioning/
```
class Solution {
public:
    bool checkpalindrome(string s,int l,int r)
    {
        while(l<r)
        {
            if(s[l++]!=s[r--]) return false;
        }
        return true;
    }

    void recursion(int i,string s,vector<vector<string>> &result,vector<string> &path)
    {
        if(i==s.size())
        {
            result.push_back(path);
            return;
        }

        for(int j=i;j<s.size();j++)
        {
            if(checkpalindrome(s,i,j))
            {
                path.push_back(s.substr(i,j-i+1));
                recursion(j+1,s,result,path);
                path.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        vector<vector<string>> result;
        vector<string> path;

        recursion(0,s,result,path);

        return result;
    }
};
```
* * *
KTH PERMUTATION SEQUENCE
https://leetcode.com/problems/permutation-sequence/

### Note - The extreme naive solution is to generate all the possible permutations of the given sequence.  This is achieved using recursion and every permutation generated is stored in some other data structure (here we have used a vector). Finally, we sort the data structure in which we have stored all the sequences and return the Kth sequence from it.

```
class Solution {
public:
    string getPermutation(int n, int k) {
        int f=1;
        vector<int> sequence;
        string permutation;
        k=k-1; // 0-based indexing
        for(int i=1;i<n;i++)
        {
            f=f*i;
            sequence.push_back(i);
        }
        sequence.push_back(n);
    while(true)
    {    
        permutation+=to_string(sequence[k/f]);
        sequence.erase(sequence.begin()+k/f);
        if(sequence.size()==0) break;

        k=k%f;
        f=f/sequence.size();
    }
    return permutation;
    }
};
```
* * *