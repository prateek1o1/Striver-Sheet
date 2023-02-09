# TRIE
IMPLEMENT TRIE (PREFIX TREE)
https://leetcode.com/problems/implement-trie-prefix-tree/
```
struct Node{
		Node *links[26];
		bool flag=false;
		bool containkey(char ch)
		{return (links[ch-'a']!=NULL);
        }
		void put(char ch, Node *node)
		{links[ch-'a']=node;
        }
		Node *get(char ch)
		{return links[ch-'a'];
        }
		void setEnd()
		{flag=true;
        }
		bool isEnd()
		{return flag;
        }
};   

class Trie {
private: Node *root;
public:
    Trie() {
        root=new Node();
    }
    
    void insert(string word) {
        Node *node=root;
        for(int i=0;i<word.size();i++)
        {
            if(!node->containkey(word[i])){
                node->put(word[i],new Node());
            }
            node=node->get(word[i]);
        }
        node->setEnd();
    }
    
    bool search(string word) {
        Node* node=root;
        for(int i=0;i<word.length();i++)
        {
            if(!node->containkey(word[i]))
            {
                return false;
            }
            node=node->get(word[i]);
        }
        return node->isEnd();
    }
    
    bool startsWith(string prefix) {
        
        Node *node=root;
        for(int i=0;i<prefix.size();i++)
        {
            if(!node->containkey(prefix[i]))
            {
                return false;
            }
            node=node->get(prefix[i]);
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```
***

IMPLEMENT TRIE 2
https://www.codingninjas.com/codestudio/problems/implement-trie_1387095
```
#include <bits/stdc++.h> 
struct Node{
    Node *links[26];
    int ce=0;
    int cp=0;

    bool containsKey(char ch)
    {
        return (links[ch-'a']!=NULL);
    }
    Node *get(char ch)
    {
        return links[ch-'a'];
    }
    void put(char ch,Node *node)
    {
        links[ch-'a']=node;
    }
    void increaseEnd()
    {
        ce++;
    }
    void increasePrefix()
    {
        cp++;
    }
    void deleteEnd()
    {
        ce--;
    }
    void reducePrefix()
    {
        cp--;
    }
    int getEnd()
    {
        return ce;
    }
    int getPrefix()
    {
        return cp;
    }
};

class Trie{
    private:
        Node *root;
    public:

    Trie(){
        root=new Node();
    }

    void insert(string &word){
        // Write your code here.
        Node *node=root;
        for(int i=0;i<word.length();i++)
        {
            if(!node->containsKey(word[i]))
            {
                node->put(word[i],new Node());
            }
            node=node->get(word[i]);
            node->increasePrefix();
        }

        node->increaseEnd();
    }

    int countWordsEqualTo(string &word){
        // Write your code here.
        Node *node=root;
        for(int i=0;i<word.length();i++)
        {
            if(node->containsKey(word[i]))
            {
                node=node->get(word[i]);
            }
            else
            {
                return 0;
            }
        }
        return node->getEnd();
    }

    int countWordsStartingWith(string &word){
        // Write your code here.
        Node* node=root;
        for(int i=0;i<word.length();i++)
        {
            if(node->containsKey(word[i]))
            {
                node=node->get(word[i]);
            }
            else
            {
                return 0;
            }
        }
        return node->getPrefix();
    }

    void erase(string &word){
        // Write your code here.
        Node *node=root;

        for(int i=0;i<word.length();i++)
        {
            if(node->containsKey(word[i]))
            {
                node=node->get(word[i]);
                node->reducePrefix();
            }
            else
            {
                return;
            }
        }
        node->deleteEnd();
    }
};

```
***

LONGEST STRING WITH ALL PREFIXES
https://www.codingninjas.com/codestudio/problems/complete-string_2687860
```
#include <bits/stdc++.h> 
using namespace std;

struct Node{
		Node *links[26];
		bool flag=false;
		bool containkey(char ch)
		{return (links[ch-'a']!=NULL);
        }
		void put(char ch, Node *node)
		{links[ch-'a']=node;
        }
		Node *get(char ch)
		{return links[ch-'a'];
        }
		void setEnd()
		{flag=true;
        }
		bool isEnd()
		{return flag;
        }
};   

class Trie{
    private: Node *root;

    public:
        Trie()
        {
            root=new Node();
        }
        
    void insert(string word) {
        Node *node=root;
        for(int i=0;i<word.size();i++)
        {
            if(!node->containkey(word[i])){
                node->put(word[i],new Node());
            }
            node=node->get(word[i]);
        }
        node->setEnd();
    }

    bool checkIfPrefixExists(string word)
    {
        bool flag=true;
        Node *node=root;
        for(int i=0;i<word.length() && flag;i++)
        {
            if(node->containkey(word[i]))
            {
                node=node->get(word[i]);

                flag=flag & node->isEnd();
            }
            else
            {
                return false;
            }
        }
        return flag;
    }

};

string completeString(int n, vector<string> &a){
    // Write your code here.
    Trie trie;
    for(auto &it:a)
    {
        trie.insert(it);
    }
    string longest="";

    for(auto &it:a)
    {
        if(trie.checkIfPrefixExists(it))
        {
            if(it.length() > longest.length())
            {
                longest=it;
            }
            else if(it.length()==longest.length() && it < longest)
            {
                longest=it;
            }
        }
    }

    if(longest=="")
        return "None";
    return longest;
}
```
***

NUMBER OF DISTINCT SUBSTRINGS IN A STRING
https://www.codingninjas.com/codestudio/problems/count-distinct-substrings_985292
```
#include <bits/stdc++.h>
using namespace std;
struct Node{
		Node *links[26];
		bool containkey(char ch)
		{return (links[ch-'a']!=NULL);
        }
		void put(char ch, Node *node)
		{links[ch-'a']=node;
        }
		Node *get(char ch)
		{return links[ch-'a'];
        }
};   
int countDistinctSubstrings(string &s)
{
    //    Write your code here.
    int distinct=0;
    Node *root=new Node();
    for(int i=0;i<s.size();i++)
    {   
        Node *node=root;
        for(int j=i;j<s.size();j++)
        {
            if(!node->containkey(s[j]))
            {
                distinct++;
                node->put(s[j],new Node());
            }
            node=node->get(s[j]);
        }
    }
    return distinct+1;
}
```
***

POWER SET
https://practice.geeksforgeeks.org/problems/power-set4302/1#
```
class Solution{
	public:
		vector<string> AllPossibleStrings(string s){
		    // Code here
		    vector<string> R;
		    int n=s.size();
		    for(int i=0;i< (1<<n);i++)
		    {
		        string k="";
		        for(int j=0;j<n;j++)
		        {
		            if(i&(1<<j))
		            {
		                k+=s[j];
		            }
		        }
		        if(k.length()>0)
		            R.push_back(k);
		    }
		    sort(R.begin(),R.end());
		    return R;
		}
};
```
$O(2^N * N)$
***

MAXIMUM XOR OF TWO NUMBERS IN AN ARRAY
https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/
```
struct Node{
		Node *links[2];
		bool containkey(int bit)
		{return (links[bit]!=NULL);
        }
		void put(int bit, Node *node)
		{links[bit]=node;
        }
		Node *get(int bit)
		{return links[bit];
        }
};
class Trie{
    private: Node *root;
    public:
    Trie()
    {
         root=new Node();
    }

    void insert(int N) {
        Node *node=root;
        for(int i=31;i>=0;i--)
        {
            int bit=(N>>i)&1;
            if(!node->containkey(bit)){
                node->put(bit,new Node());
            }
            node=node->get(bit);
        }
    }
    int getMax(int N){
        Node *node=root;
        int maxnumber=0;
        for(int i=31;i>=0;i--)
        {
            int bit=(N>>i)&1;
            if(node->containkey(!bit))
            {
                maxnumber= maxnumber + (1<<i);
                node=node->get(!bit);
            }
            else
            {
                node=node->get(bit);
            }
        }
        return maxnumber;
    }
};
class Solution {

public:
    int findMaximumXOR(vector<int>& nums) {
        
        Trie trie;
        for(int i=0;i<nums.size();i++)
        {
            trie.insert(nums[i]);
        }
        int m=0;
        for(int i=0;i<nums.size();i++)
        {
            m=max(m,trie.getMax(nums[i]));
        }
        return m;
    }
};
```
***
$TC=O(N*32) + O(M*32)$
***
MAXIMUM XOR WITH AN ELEMENT FROM ARRAY
https://leetcode.com/problems/maximum-xor-with-an-element-from-array/
```
struct Node{
		Node *links[2];
		bool containkey(int bit)
		{return (links[bit]!=NULL);
        }
		void put(int bit, Node *node)
		{links[bit]=node;
        }
		Node *get(int bit)
		{return links[bit];
        }
};
class Trie{
    private: Node *root;
    public:
    Trie()
    {
         root=new Node();
    }

    void insert(int N) {
        Node *node=root;
        for(int i=31;i>=0;i--)
        {
            int bit=(N>>i)&1;
            if(!node->containkey(bit)){
                node->put(bit,new Node());
            }
            node=node->get(bit);
        }
    }
    int getMax(int N){
        Node *node=root;
        int maxnumber=0;
        for(int i=31;i>=0;i--)
        {
            int bit=(N>>i)&1;
            if(node->containkey(1-bit))
            {
                maxnumber= maxnumber | (1<<i);
                node=node->get(1-bit);
            }
            else
            {
                node=node->get(bit);
            }
        }
        return maxnumber;
    }
};

class Solution {
public:
    vector<int> maximizeXor(vector<int>& nums, vector<vector<int>>& queries) {
        Trie trie;
        sort(nums.begin(),nums.end());
        vector< pair<int,pair<int,int>> > offline;
        int q=queries.size();
        for(int i=0;i<q;i++)
        {
            offline.push_back({queries[i][1],{queries[i][0],i}});
        }
        sort(offline.begin(),offline.end());
        vector<int> answer(q,0);
        int ind=0;
        int n=nums.size();

        for(int i=0;i<q;i++)
        {
            int mi=offline[i].first;
            int xi=offline[i].second.first;
            int qind=offline[i].second.second;

            while(ind<n && nums[ind] <= mi)
            {
                trie.insert(nums[ind]);
                ind++;
            }
            if(ind==0) answer[qind]=-1;
            else answer[qind]=trie.getMax(xi);
            
        }
        return answer;
    }
};
```
***
### Note
OPERATING SYSTEMS/ DATABASE/ COMPUTER NETWORKS/ PROJECT OVERVIEW