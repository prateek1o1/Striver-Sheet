# GRAPHS
# CLONE A GRAPH
https://leetcode.com/problems/clone-graph/
```
class Solution {
public:
    unordered_map <Node *,Node *> map;
    void dfs(Node* node)
    {
        Node* dummy=new Node(node->val);
        map[node]=dummy;
        
        for(auto k:node->neighbors)
        {
            if(map.find(k)==map.end())
            {
                dfs(k);
            }
            dummy->neighbors.push_back(map[k]);
        }
    }
    
    Node* cloneGraph(Node* node) {
        
        if(node ==NULL) return NULL;
        dfs(node);
        return map[node];
    }
};
```
***
# DFS
https://practice.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1
```
  public:
    void dfs(int node, vector <int> &visited, vector <int> adj[],vector <int> &traversal)
    {
        traversal.push_back(node);
        visited[node]=1;
        for(auto j:adj[node])
        {
            if(!visited[j])
            {
                dfs(j,visited,adj,traversal);
            }
        }
    }
    vector<int> dfsOfGraph(int V, vector<int> adj[]) {
        vector <int> traversal;
        vector <int> visited(V,0);
        dfs(0,visited,adj,traversal);
        
        return traversal;
    }
};
```
***
# BFS
https://practice.geeksforgeeks.org/problems/bfs-traversal-of-graph/1
```
class Solution {
  public:
    vector<int> bfsOfGraph(int V, vector<int> adj[]) {
     
        vector <int> traversal;
        vector <int> visited(V,0);
        
        queue <int> q;
        q.push(0);
        visited[0]=1;
        while(!q.empty())
        {
            int node=q.front();
            q.pop();
            traversal.push_back(node);
            
            for(auto j:adj[node])
            {
                if(!visited[j])
                    {
                        q.push(j);
                        visited[j]=1;
                    }
            }
        }
    return traversal;
    }
};

```
***
# DETECT A CYCLE IN UNDIRECTED GRAPH USING BFS
https://www.codingninjas.com/codestudio/problems/1062670?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website
```
bool Cycle(int k,vector<int> adj[],vector<int>& visited)
{  
    queue <pair<int,int>> q;
        q.push({k,-1});
        visited[k]=true;
        
        while(!q.empty())
        {
            pair<int,int> node=q.front();
            q.pop();
            for(auto j:adj[node.first])
            {
                if(!visited[j])
                {
                    q.push({j,node.first});
                    visited[j]=1;
                }
                else
                {
                    if(j!=node.second)
                        return true;
                }
            }
        }
 return false;
}
string cycleDetection (vector<vector<int>>& edges, int n, int m)
{
    // Write your code here.
    vector <int> adj[n+1];
    vector <int> visited(n+1,0);
    
    for(int i=0;i<m;i++)
    {adj[edges[i][0]].push_back(edges[i][1]);
     adj[edges[i][1]].push_back(edges[i][0]);
    }

    for(int i=1;i<=n;i++)
    {if(!visited[i])
    {
        if(Cycle(i,adj,visited)) return "Yes";
    }
    }
return "No";
}
```
***
DETECT A CYCLE IN UNDIRECTED GRAPH USING DFS
https://www.codingninjas.com/codestudio/problems/1062670?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website&leftPanelTab=0
```
bool CycleWithDfs(int k,int parent,vector<int> adj[],vector<int>& visited)
{  
    visited[k]=1;
    for(auto j:adj[k])
    {
        if(!visited[j])
        {
            if(CycleWithDfs(j,k,adj,visited)) return true;
        }
        else
        {
            if(j!=parent) return true;
        }
    }
    return false;
}
string cycleDetection (vector<vector<int>>& edges, int n, int m)
{
    // Write your code here.
    vector <int> adj[n+1];
    vector <int> visited(n+1,0);
    
    for(int i=0;i<m;i++)
    {adj[edges[i][0]].push_back(edges[i][1]);
     adj[edges[i][1]].push_back(edges[i][0]);
    }

    for(int i=1;i<=n;i++)
    {if(!visited[i])
    {
        if(CycleWithDfs(i,-1,adj,visited)) return "Yes";
    }
    }
return "No";
}
```
***
DETECT A CYCLE IN DIRECTED GRAPH USING BFS (Kahn's Algorithm)
https://www.codingninjas.com/codestudio/problems/1062626?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website
```
int detectCycleInDirectedGraph(int n, vector < pair < int, int >> & edges) {
  // Write your code here.
    vector <int> adj[n+1];
    vector <int> indegree(n+1,0);
  
    for(int i=0;i<edges.size();i++)
    {adj[edges[i].first].push_back(edges[i].second);
    }
    
    for(int i=1;i<=n;i++)
    {
        for(auto j:adj[i])
            indegree[j]++;
    }
    
    queue <int> q;
    for(int i=1;i<=n;i++)
        if(indegree[i]==0)
            q.push(i);
    
    int counter=0;
    while(!q.empty())
    {
        int node=q.front();
        q.pop();
        counter++;
        for(auto k:adj[node])
        {
            indegree[k]--;
            if(indegree[k]==0)
                q.push(k);
        }
    }
    if(counter==n) return 0;
    else  return 1;
}
```
***
DETECT A CYCLE IN DIRECTED GRAPH USING DFS
https://www.codingninjas.com/codestudio/problems/1062626?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website
```
bool CycleWithDfs(int node,vector <int> &visited,vector <int> &dfsvisited,vector <int> adj[])
{
    visited[node]=1;
    dfsvisited[node]=1;
    for(auto k:adj[node])
    {
        if(!visited[k])
        {
            if(CycleWithDfs(k,visited,dfsvisited,adj)) return true;
        }
        else if(dfsvisited[k]==1){ return true;}
    }
    dfsvisited[node]=0;
    return false;
}

int detectCycleInDirectedGraph(int n, vector < pair < int, int >> & edges) {
  // Write your code here.
    vector <int> adj[n+1];
    vector <int> visited(n+1,0);
    vector <int> dfsvisited(n+1,0);
    
    for(int i=0;i<edges.size();i++)
    {adj[edges[i].first].push_back(edges[i].second);
    }
    
    for(int i=1;i<n+1;i++)
    {
        if(!visited[i])
        {
            if(CycleWithDfs(i,visited,dfsvisited,adj))
                return true;
        }
    }
    return false;
}
```
***
TOPOLOGICAL SORT BFS
https://practice.geeksforgeeks.org/problems/topological-sort/1
```
{
	public:
	//Function to return list containing vertices in Topological order. 
	vector<int> topoSort(int V, vector<int> adj[]) 
	{
	    // code here
	    vector <int> indegree(V,0);
	    vector <int> answer;
	    
	    for(int i=0;i<V;i++)
	    {
	        for(auto j:adj[i])
	        {
	            indegree[j]+=1;
	        }
	        
	    }   
	            
	   queue <int> q;
	   for(int i=0;i<V;i++)
	       {
	       if(indegree[i]==0)
	       q.push(i);
	       }
	    
		while(!q.empty())
	            {
	                int node=q.front();
	                q.pop();
	                answer.push_back(node);
	                
	                for(auto k:adj[node])
	                {
	                    indegree[k]--;
	                    if(indegree[k]==0)
	                        q.push(k);
	                }
	                
	            }
	  return answer;      
	    }
};
```
***
TOPOLOGICAL SORT DFS
https://practice.geeksforgeeks.org/problems/topological-sort/1
```
#include <bits/stdc++.h>
using namespace std;
class Solution
{
	public:
	void dfs(int node,vector<int> &visited,vector<int> adj[],stack <int> &s)
	{
	    visited[node]=1;
	    for(auto k:adj[node])
	    {
	        if(!visited[k])
	        {
	            dfs(k,visited,adj,s);
	        }
	    }
	    s.push(node);
	}
	vector<int> topoSort(int V, vector<int> adj[]) 
	{
	    // code here
	    vector <int> visited(V,0);
	    stack <int>  s;
	    vector <int> answer;
	    for(int i=0;i<V;i++)
	    {
	        if(!visited[i])
	        dfs(i,visited,adj,s);
	    }
	
	    while(!s.empty())
	    {
	        int x=s.top();
	        s.pop();
	        answer.push_back(x);
	        
	    }
	    return answer;
	}
};
```
***
NUMBER OF ISLANDS
https://leetcode.com/problems/number-of-islands/
```
class Solution {
public:
    void dfs(vector<vector<char>>& grid,int i,int j)
    {
if(i<0 || j<0 || i>=grid.size() || j>=grid[0].size() || grid[i] [j]=='0' ) return;
        
        grid[i][j]='0';
    
        dfs(grid,i+1,j);
        dfs(grid,i,j+1);
        dfs(grid,i-1,j);
        dfs(grid,i,j-1);
    }
    
    int numIslands(vector<vector<char>>& grid) {
        int n=grid.size();
        int m=grid[0].size(); 
        int islands=0;
      
        if(n==0) return 0;
        
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(grid[i][j]=='1')
                {
                    dfs(grid,i,j);
                    islands++;
                }
            }
        }
       return islands; 
    }
};
```
***
 BIPARTITE CHECK USING BFS
https://leetcode.com/problems/is-graph-bipartite/
```
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        
        vector <int> color(graph.size(),-1);
        vector <int> adj[graph.size()];
        int t=0;
        for(auto edges:graph)
        {   
            for(auto j:edges)
            {
                adj[t].push_back(j);
            }
            t++;
        }
        
        for(int i=0;i<graph.size();i++)
        {   
            if(color[i]==-1)
            {   queue <int> q;
                q.push(i);
                color[i]=0;
                
                while(!q.empty())
                {
                    int node=q.front();
                    q.pop();

                    for(auto k:adj[node])
                    {
                        if(color[k]==-1)
                        {
                            q.push(k);
                            color[k]=color[node]^1;
                        }
                        else
                        {
                            if(color[k]==color[node])
                                return false;
                        }
                    }
                }
            }
        }
        return true;
    }
};
```
***
BIPARTITE CHECK USING DFS
https://leetcode.com/problems/is-graph-bipartite/
```
class Solution {
public:
    bool DFS(int node,vector <int> &color, vector <int> adj[])
    {
        if(color[node]==-1) color[node]=0;
        
        for(auto k:adj[node])
        {
            if(color[k]==-1)
            {
                color[k]=1-color[node];
                if(!DFS(k,color,adj)) 
                    return false;
            }
            else
            {
                if(color[k]==color[node])
                    return false;
            }
        }
        return true;
    }
    
    bool isBipartite(vector<vector<int>>& graph) {
        
        int N=graph.size();
        vector <int> color(N,-1);
        vector <int> adj[N];
        int t=0;
        
        for(auto edges : graph)
        {
            for(auto u : edges)
            {
                adj[t].push_back(u);
            }
            t++;
        }
        
        for(int i=0;i<N;i++)
        {
            if(color[i]==-1)
            {
                if(!DFS(i,color,adj))
                    return false;
            }
        }
    return true;
    }
};
```
***