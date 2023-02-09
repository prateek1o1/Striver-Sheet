# BINARY SEARCH TREE 2

FLOOR IN A BST
https://www.codingninjas.com/codestudio/problems/floor-from-bst_920457?source=youtube&campaign=Striver_Tree_Videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=Striver_Tree_Videos
```
int floorInBST(TreeNode<int> * root, int X)
{
    // Write your code here.
    TreeNode<int>* cur=root;
    int floor=-1;
    while(cur!=NULL)
    {
        if(cur->val < X)
        {
            floor=cur->val;
            cur=cur->right;
        }
        else if(cur->val > X)
        {
            cur=cur->left;
        }
        else
        {
            return cur->val;
        }
    }
    return floor;
}
```
***
CEIL IN A BST
https://www.codingninjas.com/codestudio/problems/ceil-from-bst_920464?source=youtube&campaign=Striver_Tree_Videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=Striver_Tree_Videos

```
int findCeil(BinaryTreeNode<int> *node, int x){
    // Write your code here.
    //if(node==NULL || node->val==x) return node->val;
    int ceil=-1;
    BinaryTreeNode<int> *cur=node;
    while(cur!=NULL)
    {
        if(cur->data > x)
        {
            ceil=cur->data;
            cur=cur->left;
        }
        else if (cur->data < x)
        {
            cur=cur->right;
        }
        else
        {
            return cur->data;
        }
    }
    return ceil;
}
```
***
FIND KTH SMALLEST ELEMENT IN BST
https://leetcode.com/problems/kth-smallest-element-in-a-bst/
```
class Solution {
public:
    void Inorder(TreeNode* root, int &k,int &counter,int &answer)
    {  
        if(root==NULL) return;
        
        Inorder(root->left,k,counter,answer);
        counter++;
        if(counter==k)
        {
            answer=root->val;
        }
        Inorder(root->right,k,counter,answer);
        
    }
    int kthSmallest(TreeNode* root, int k) 
    {   
        int counter=0;
        int answer;
        Inorder(root,k,counter,answer);
        return answer;
    }
};
```
***
FIND KTH LARGEST ELEMENT IN BST
https://practice.geeksforgeeks.org/problems/kth-largest-element-in-bst/1
```
class Solution
{
    public:
    void RightRootLeft(Node* root,int K,int &counter,int &answer)
    {
        if(root==NULL) return;
        
        RightRootLeft(root->right,K,counter,answer);
        if(++counter==K)
        {
            answer=root->data;
        }
        RightRootLeft(root->left,K,counter,answer);
    }
    int kthLargest(Node *root, int K)
    {
        //Your code here
        int counter=0;
        int answer=0;
        RightRootLeft(root,K,counter,answer);
        return answer;
    }
};
```
***
FIND A PAIR WITH A GIVEN SUM IN BST
https://leetcode.com/problems/two-sum-iv-input-is-a-bst/

`BST ITERATOR (NOT ALLOWED TO STORE INORDER)
STACK <INT> S; //O(Height)
`

```
class BSTIterator {
stack<TreeNode *> mystack;
bool reverse=true;    
public:
    BSTIterator(TreeNode* root,bool isreverse) 
    {
        reverse=isreverse;
        pushall(root);
    }
    
    bool hasnext()
    {
        return !mystack.empty();
    }
    int next()
    {
        TreeNode * node=mystack.top();
        mystack.pop();
       if(!reverse) pushall(node->right);
        else pushall(node->left);
        
        return node->val;
    }
private:
    void pushall(TreeNode *node)
    {
        for(;node!=NULL;)
        {
              mystack.push(node);
            if(!reverse)
            {
            node=node->left;
            }
            else
            {
            node=node->right;
            }
        }
    }
};


class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        
        if(root==NULL) return false;      
        
        BSTIterator left(root,false);
        BSTIterator right(root,true);
         
        int i=left.next();
        int j=right.next();
        while(i<j)
        {
            int add=i+j;
            
            if(i+j==k) return true;
            else if(i+j < k) i=left.next();
            else j=right.next();
        }
        return false;
    }
};
```
***
BST ITERATOR
https://leetcode.com/problems/binary-search-tree-iterator/
```
class BSTIterator {
public:
    stack <TreeNode *>S; 
    BSTIterator(TreeNode* root) {
        
        pushall(root);
    }
    
    int next() {
        TreeNode *node=S.top();
        S.pop();
        pushall(node->right);
        return node->val;
    }
    
    bool hasNext() {
        return !S.empty();
    }
    void pushall(TreeNode * node)
    {
        for(;node!=NULL;)
        {
            S.push(node);
            node=node->left;
        }
    }
};
```
***
 Maximum Sum BST in Binary Tree
https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/

1- Track smallest of all node in right subtree.
2- Track largest of all node in left subtree.
3- Postorder traversal Left->Right->Root
4 [size,smallest,largest,addition]
```
class Solution {
public:
    vector<int> search(TreeNode* root, int &answer)
    {
        if(root==NULL) return {INT_MAX,INT_MIN,0};
        
        vector<int> left,right;
        
        left=search(root->left,answer);
        right=search(root->right,answer);
        
        if(left.empty() || right.empty() || left[1] >= root->val || root->val >= right[0]) return {};
        
        int add=left[2]+right[2]+root->val;
        answer=max(answer,add);
        return {min(left[0],root->val),max(right[1],root->val),add};
    }
    
    int maxSumBST(TreeNode* root) {
        
        int answer=0;
        search(root,answer);
        return answer;
    }
};
```
***
SERIALIZE AND DESERIALIZE BINARY TREE
https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

Note- LEVEL ORDER TRAVERSAL

```
# include<bits/stdc++.h>
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(root==NULL) return "";
        
        string s;
        queue <TreeNode *> Q;
        Q.push(root);
        while(!Q.empty())
        {
            auto node=Q.front();
            Q.pop();
            if(node==NULL) s.append("#,");
            
            else s.append(to_string(node->val)+",");
            
            if(node!=NULL)
            {
            Q.push(node->left);
            Q.push(node->right);
            }            
        }
        return s;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        
        if(data.size()==0) return NULL;
        stringstream s(data);
        string str;
        getline(s, str, ',');
        TreeNode *root=new TreeNode(stoi(str));
        queue <TreeNode*> Q;
        Q.push(root);
        
        while(!Q.empty())
        {
            TreeNode* node=Q.front();
            Q.pop();
            getline(s,str,',');
            if(str=="#")
                node->left=NULL;
            else
            {
                TreeNode* left=new TreeNode(stoi(str));
                node->left=left;
                Q.push(left);
             
             }   
            getline(s,str,',');
            
            if(str=="#")
                node->right=NULL;
            else
            {
                 TreeNode* right=new TreeNode(stoi(str));
                node->right=right;
                Q.push(right); 
            }
        }
        return root;
    }
};
```
***