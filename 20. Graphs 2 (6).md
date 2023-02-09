# GRAPHS 2
Kosaraju's Algorithm (SCC)
Step 1- Sort the nodes according to the finishing time.(Topological Sort gives a stack)
Step 2- Transpose the graph.
Step 3- DFS according to finishing time.

STRONGLY CONNECTED COMPONENTS (KOSARAU’S ALGORITHM)
https://www.codingninjas.com/codestudio/problems/985311?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website
```
#include <bits/stdc++.h>
using namespace std;

void DFSWITHTOPOLOGICAL(int node,stack <int> &s,vector <int> &visited,vector <int> adj[])
{
    visited[node]=1;
    for(auto j:adj[node])
    {
        if(!visited[j])
        DFSWITHTOPOLOGICAL(j,s,visited,adj);
    }
    s.push(node);
}

void DFSWITHREVERSE(int node,vector <int> &visited,vector <int> transpose[],vector <int>&x)
{
    x.push_back(node);
    visited[node]=1;
    for(auto j:transpose[node])
    {
        if(!visited[j])
        DFSWITHREVERSE(j,visited,transpose,x);
    }
}

vector<vector<int>> stronglyConnectedComponents(int n, vector<vector<int>> &edges)
{
    // Write your code here.
    vector <int> adj[n];
    vector <int> transpose[n];
 
    for(int i=0;i<edges.size();i++)
    {
            adj[edges[i][0]].push_back(edges[i][1]);
            transpose[edges[i][1]].push_back(edges[i][0]);
    }
    stack<int> s;
    vector<int> visited(n,0);
    for(int i=0;i<n;i++)
    {
        if(!visited[i])
        {
            DFSWITHTOPOLOGICAL(i,s,visited,adj);
        }
    }
    vector <vector<int>> answer;
    fill(visited.begin(),visited.end(),0);
    while(!s.empty())
    {
        vector <int> x;
        int node=s.top();
        s.pop();
        if(!visited[node])
        {
            DFSWITHREVERSE(node,visited,transpose,x);
        }
        answer.push_back(x);
    }
    return answer;
}
```
***
DIJKSTRA’S ALGORITHM
Dijkstra's Algorithm is one example of a single-source shortest or SSSP algorithm, i.e., given a source vertex it finds shortest path from source to all other vertices.

 https://practice.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/1
```
 {
	public:
	//Function to find the shortest distance of all the vertices
    //from the source vertex S.
    vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        // Code here
        vector <int> distance(V+1,INT_MAX);
        priority_queue < pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>> > minheap; 
        
        distance[S]=0;
        minheap.push(make_pair(0,S));
        
        while(!minheap.empty())
        {
            int prevdistance= minheap.top().first;
            int prev= minheap.top().second;
            minheap.pop();
            
            for(auto j:adj[prev])
            {
                int next=j[0];
                int nextdistance=j[1];
                
    if(distance[next] > prevdistance /*distance[prev]*/+ nextdistance)
                {
 distance[next]=prevdistance /*distance[prev]*/+ nextdistance;               
 minheap.push(make_pair(distance[next],next));
                }
            }
        }
    
    return distance;    
    }
};
```
***
BELLMAN FORD ALGORITHM
The Bellman-Ford algorithm is a way to find single source shortest paths in a graph with negative edge weights (but no negative cycles). The second for loop in this algorithm also detects negative cycles. The first for loop relaxes each of the edges in the graph n − 1 times.

Key Points of Bellman Ford Algorithm-
It will work for Negative weights.
Helps to detect negative cycle.
Will not work for negative cycle.
Will only work for directed graph.
In case of undirected graph ,convert it into directed graph.

Time complexity is -O(N-1)*E which is more than Dijkstra's algorithm but this algo helps to detect negative cycle in graph

https://practice.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/0?fbclid=IwAR2_lL0T84DnciLyzMTQuVTMBOi82nTWNLuXjUgahnrtBgkphKiYk6xcyJU
```
class Solution {
  public:
    /*  Function to implement Bellman Ford
    *   edges: vector of vectors which represents the graph
    *   S: source vertex to start traversing graph with
    *   V: number of vertices
    */
    vector<int> bellman_ford(int V, vector<vector<int>>& edges, int S) {
        // Code here
        
        vector <int> distance(V,100000000);
        distance[S]=0;
        vector <int> negativecycle(1,-1);
        for(int i=0;i<V-1;i++)
        {
            for(auto j:edges)
            {
                int u=j[0];
                int v=j[1];
                int w=j[2];
                if(distance[u]+w < distance[v])
                    distance[v]=distance[u]+w;
                    
            }
        }
        
        for(auto j:edges)
        {
                int u=j[0];
                int v=j[1];
                int w=j[2];
                if(distance[u]+w<distance[v])
                    {distance[v]=distance[u]+w;
                    
                    return negativecycle;        
                    }
        }
        
    
     return distance;   
    }
};
```
***
FLOYD WARSHALL ALGORITHM
https://practice.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1
```
class Solution {
  public:
	void shortest_distance(vector<vector<int>>&matrix){
	    // Code here
	    int N=matrix.size();
	    for(int i=0;i<N;i++)
	        {
	            for(int j=0;j<N;j++)
	            {
	                if(matrix[i][j]==-1)
	                {
	                    matrix[i][j]=1e9;       
	                }
	            }    
	       }
	    
	    for(int k=0;k<N;k++)
	    {
	        for(int i=0;i<N;i++)
	        {
	            for(int j=0;j<N;j++)
	            {
	            matrix[i][j]=min(matrix[i][j],matrix[i][k]+matrix[k][j]);   
	            }     
	       }
	    }
		
	    /*
	    for(int i=0;i<N;i++)
	    {
	        if(matrix[i][i]<0)
	        {
	            NEGATIVE CYCLE
	        }
	    }
	    */
	 for(int i=0;i<N;i++)
	        {
	            for(int j=0;j<N;j++)
	            {
	                if(matrix[i][j]==1e9)
	                {
	                    matrix[i][j]=-1;       
	                }
	            }        
	       }
	}
};
```
***
MST USING PRIM’S ALGORITHM
https://practice.geeksforgeeks.org/problems/minimum-spanning-tree/1
```
{
	public:
	//Function to find sum of weights of edges of the Minimum Spanning Tree.
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        // code here
        vector <int> key(V,1e9);
        vector <int> parent(V);
        vector <bool> mstset(V,false);
        
        priority_queue < pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>> > minheap;
        
        key[0]=0;
        parent[0]=-1;
        minheap.push({0,0});
        
        while(!minheap.empty())
        {
                int u=minheap.top().second;
                minheap.pop();
                mstset[u]=true;
                
                for(auto j: adj[u])
                {
                    int v=j[0];
                    int weight=j[1];
                    
                    if(mstset[v]==false && weight <key[v])
                    {
                        parent[v]=u;
                        key[v]=weight;
                        minheap.push({key[v],v});
                        
                    }
                }
        }
        
        int s=0;
        for(int i=0;i<V;i++)
        s+=key[i];
        
        return s;
    }
};
```
***
MST USING KRUSKAL’S ALGORITHM
https://practice.geeksforgeeks.org/problems/minimum-spanning-tree/1
```
 class node{
    public:
  int u;
  int v;
  int wt;
  
  node(int first, int second, int weight){
      u = first;
      v = second;
      wt = weight;
  }
};

class Solution
{
	public:
	
	int findPar(int node, vector<int> &parent){
	    if(parent[node] == node) return node;
	    return parent[node] = findPar(parent[node], parent); //PATH COMPRESSION
	}
	
	void Union(int u, int v, vector<int> &rank, vector<int> &parent){
	        u = findPar(u, parent);
            v = findPar(v, parent);
    	    if(rank[u] > rank[v])
    	    {
    	        parent[v] = u;
    	    }
    	    else if(rank[u] < rank[v]) parent[u] = v;
    	    else
    	    {
    	        parent[u] = v;
    	        rank[v]++;
    	    }
	    
	}
	
	static bool compare(node a, node b)
	{
	    return a.wt < b.wt;
	}
	
	//Function to find sum of weights of edges of the Minimum Spanning Tree.
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        vector<node> edges;
        
        for(int i=0; i<V; i++)
        {
            for(auto x : adj[i])
            {
                edges.push_back(node(i, x[0], x[1]));
            }
        }
        
        sort(edges.begin(), edges.end(), compare);
        
        vector<int> parent(V, -1);
        
        vector<int> rank(V, 0);
        for(int i=0; i<V; i++) 
            parent[i] = i;
        
        int sum = 0;
        for(auto x : edges){
            
            if(findPar(x.u, parent) != findPar(x.v, parent)){
                sum += x.wt;
                Union(x.u, x.v, rank, parent);
            }
            
        }
        return sum;
    }
};
```
***