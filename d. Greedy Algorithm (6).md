# GREEDY ALGORITHM

N MEETINGS IN ONE ROOM 
https://practice.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1
```
class Solution
{
    public:
    //Function to find the maximum number of meetings that can
    //be performed in a meeting room.
   
   int maxMeetings(int start[], int end[], int n)
    {
        // Your code here
    vector<pair<int,int>> v;
    
    for(int i=0;i<n;i++)
    {
            v.push_back({start[i],end[i]});
    }
    
    sort(v.begin(), v.end(), [](auto &left, auto &right) {return left.second < right.second;});
 
    int count=1;
    int j=0;
    for(int i=1;i<v.size();i++)
    {
        if(v[j].second < v[i].first)
        {
            j=i;
            count++;
        }
    }
    return count;
    }
};
```
****
MINIMUM NUMBER OF PLATFORMS REQUIRED FAR A RAILWAY https://practice.geeksforgeeks.org/problems/minimum-platforms-1587115620/1#

## Note: Naive approach is to have two nested for loops and count maximum overlaps at any time.

```
class Solution{
    public:
    //Function to find the minimum number of platforms required at the
    //railway station such that no train waits.
    int findPlatform(int arr[], int dep[], int n)
    {
    	// Your code here
    	sort(arr,arr+n);
    	sort(dep,dep+n);
    	
    	int count=1;
    	int mxm=0;
    	int i=1,j=0;
    	
    	while(i<n && j<n)
    	{
    	    if(arr[i] <= dep[j])
    	    {
    	        count++;
    	        i++;
    	    }
    	    else
    	    {
    	        count--;
    	        j++;
    	    }
    	    
    	    mxm=max(count,mxm);
    	}
    	return mxm;
    }
};
```
****
JOB SEQUENCING PROBLEM 
https://practice.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1#
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
****
FRACTIONAL KNAPSACK PROBLEM https://practice.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1
```
class Solution
{
    public:
    //Function to get the maximum total value in the knapsack.
    bool static comparision(Item a, Item b)
    {
        double x = (double)a.value/(double)a.weight;
        double y = (double)b.value/(double)b.weight;
        
        return x > y;
    }
    
    double fractionalKnapsack(int W, Item arr[], int n)
    {
        // Your code here
        sort(arr,arr+n,comparision);
        
        double totalprofit=0;
        int i=0;
        
        while(W>0 && i<n)
        {
            if(W >= arr[i].weight)
            {
                totalprofit+=arr[i].value;
                W=W-arr[i].weight;
            }
            else
            {
                totalprofit+=((double)arr[i].value/(double)arr[i].weight)*W;
                W=0;
            }
            i++;
        }  
        return totalprofit;
    }
        
};
```
****
GREEDY ALGORITHM TO FIND MINIMUM NUMBER OF COINS 
https://www.codingninjas.com/codestudio/problems/975277
```
#include <bits/stdc++.h> 
int findMinimumCoins(int amount) 
{
    // Write your code here
    int arr[9]={1,2,5,10,20,50,100,500,1000};
    int i=8;
    int coins=0;
    int total=0;
    while(amount>0)
    {
        if(amount>=arr[i])
        {
            coins+=amount/arr[i];
            amount=amount%arr[i];
        }
            i--;
    }
    return coins;
}
```
****