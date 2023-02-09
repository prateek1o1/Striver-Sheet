# BINARY TREE
INORDER TRAVERSAL
https://leetcode.com/problems/binary-tree-inorder-traversal/

1. Iterative
```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> t;
        stack <TreeNode *> s;
        while(true)
        {
            if(root!=NULL)
            {
                s.push(root);
                root=root->left;            
            }
            else
            {
                if(s.empty()) break;
                
                else
                {
                    root=s.top();
                    t.push_back(root->val);
                    s.pop();
                    root=root->right;
                }
            }
        }
        
        return t;
    }
};
```
2. Recursive
```
class Solution {
public:
    void inorder(TreeNode* root, vector<int> &t)
    {
        if(root==NULL)
            return;
        
        inorder(root->left,t);
        t.push_back(root->val);
        inorder(root->right,t);
        
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> t;
        inorder(root,t);
        return t;
    }
};
```

***
PREORDER TRAVERSAL
https://leetcode.com/problems/binary-tree-preorder-traversal/

1. Iterative
```
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        
        stack <TreeNode *> s;
        vector <int> t;
        
        while(true)
        {
         if(root!=NULL)
            {
             s.push(root);
             t.push_back(root->val);
             root=root->left;
            }
        else
            {
                if(s.empty()) break;
                root=s.top();
                s.pop();
                root=root->right;
            }
        }
        return t;
    }
};
```
2. Recursive
```
class Solution {
public:
    void preorder(TreeNode* root, vector<int> &t)
    {
        if(root==NULL)
            return;
			
        t.push_back(root->val);
        preorder(root->left,t);
        preorder(root->right,t);
        
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> t;
        preorder(root,t);
        return t;
    }
};
```
***
POSTORDER TRAVERSAL
https://leetcode.com/problems/binary-tree-postorder-traversal/

1. Iterative
```
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
     
        stack <TreeNode *> A;
        stack <TreeNode *> B;
        vector <int> T;
        if(root==NULL) return T;
		
        A.push(root);
        while(!A.empty())
        {
            root= A.top();
            A.pop();
            B.push(root);
            
            if(root->left!=NULL) A.push(root->left);
            if(root->right!=NULL) A.push(root->right);
        }
        while(!B.empty())
        {
            T.push_back(B.top()->val);
            B.pop();
        }
        
        return T;
    }
};
```
2. Recursive
```
class Solution {
public:
    void postorder(TreeNode* root, vector<int> &t)
    {
        if(root==NULL)
            return;
        
        postorder(root->left,t);
        postorder(root->right,t);
				 t.push_back(root->val);        
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> t;
        postorder(root,t);
        return t;
    }
};
```
***
MORRIS INORDER TRAVERSAL
https://leetcode.com/problems/binary-tree-inorder-traversal/

TC=$O(N)$
SC=$O(1)$
Note- Threaded binary tree

```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> inorder;
        TreeNode * cur=root;
        
        while(cur!=NULL)
        {
            if(cur->left==NULL)
            {
                inorder.push_back(cur->val);
                cur=cur->right;
            }
            else
            {
                TreeNode * temp=cur->left;
                
                while(temp->right && temp->right!=cur)
                {
                    temp=temp->right;
                }
                if(temp->right==NULL)
                {
                    temp->right=cur;
                    cur=cur->left;
                }
                else
                {
                    temp->right=NULL;
                    inorder.push_back(cur->val);
                    cur=cur->right;
                }
            }
        }
        return inorder;
    }
};
```
***

MORRIS PREORDER TRAVERSAL
https://leetcode.com/problems/binary-tree-preorder-traversal/

```
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        
        vector<int> inorder;
        TreeNode * cur=root;
        
        while(cur!=NULL)
        {
            if(cur->left==NULL)
            {
                inorder.push_back(cur->val);
                cur=cur->right;
            }
            else
            {
                TreeNode * temp=cur->left;
                
                while(temp->right && temp->right!=cur)
                {
                    temp=temp->right;
                }
                if(temp->right==NULL)
                {
                    temp->right=cur;
                    inorder.push_back(cur->val);
                    cur=cur->left;
                }
                else
                {
                    temp->right=NULL;
                    cur=cur->right;
                }
            }
        }
        return inorder;
        
    }
};
```
***
LEFT VIEW OF BINARY TREE
https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1
Note- 
- First node of every level is left side view. (Root Left Right)
- Last node of every level is right side view. (Root Right Left)

```
void LeftView(Node *root, int level ,vector<int> &left)
{
    if(root==NULL)
    return;

    if(left.size()==level)
    {
        left.push_back(root->data);
    }
    LeftView(root->left,level+1,left);
    LeftView(root->right,level+1,left);
}
vector<int> leftView(Node *root)
{
   // Your code here
   vector<int> left;
   
   LeftView(root,0,left);
   
   return left;
   
}
```
TC-$O(N)$
SC-$O(H)$

RIGHT VIEW OF BINARY TREE
https://leetcode.com/problems/binary-tree-right-side-view/submissions/

```
class Solution {
    
public:
    
    void find(TreeNode * root,int level,vector<int> &view)
    {
        if(root==NULL)
            return;
    
        if(view.size()==level)
        {
            view.push_back(root->val);
        }
        
        find(root->right,level+1,view);
        find(root->left,level+1,view);
    }
    vector<int> rightSideView(TreeNode* root) {
        
        vector<int> view;
        find(root,0,view);
        
        return view;
    }
};
```
TC-$O(N)$
SC-$O(H)$
***
BOTTOM VIEW OF BINARY TREE
https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1
Level order traversal (Queue(Node,Parallel line)) + Map(Parallel line, Node)

```
class Solution {
  public:
    vector <int> bottomView(Node *root) {
        // Your Code Here
        map <int,int> M;
        queue <pair<Node*,int>> Q;
        
        vector<int> answer;
        
        if(root==NULL)
        return answer;
        
        Q.push({root,0});
        
        while(!Q.empty())
        {
            auto k=Q.front();
            Q.pop();
            
            Node * node=k.first;
            int line=k.second;
            M[line]=node->data;
            
            if(node->left!=NULL)
            {
                Q.push({node->left,line-1});
            }
            
            if(node->right!=NULL)
            {
                Q.push({node->right,line+1});
            }
        }
        for(auto i:M)
        {
            answer.push_back(i.second);
        }
        return answer;
    }
};
```
TC-$O(N)$
SC-$O(N)$
***
TOP VIEW OF BINARY TREE
https://practice.geeksforgeeks.org/problems/top-view-of-binary-tree/1

```
class Solution
{
    public:
    //Function to return a list of nodes visible from the top view 
    //from left to right in Binary Tree.
    vector<int> topView(Node *root)
    {
        //Your code here
        map <int,int> M;
        queue <pair<Node*,int>> Q;
        
        vector<int> answer;
        
        if(root==NULL)
        return answer;
        
        Q.push({root,0});
        
        while(!Q.empty())
        {
            auto k=Q.front();
            Q.pop();
            
            Node * node=k.first;
            int line=k.second;
            
            if(M.find(line)==M.end())
            M[line]=node->data;
            
            if(node->left!=NULL)
            {
                Q.push({node->left,line-1});
            }
            
            if(node->right!=NULL)
            {
                Q.push({node->right,line+1});
            }
        }
        for(auto i:M)
        {
            answer.push_back(i.second);
        }
        return answer;
    }

};
```
***

PREORDER INORDER POSTORDER IN A SINGLE TRAVERSAL
https://www.codingninjas.com/codestudio/problems/981269?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website

```
vector<vector<int>> getTreeTraversal(BinaryTreeNode<int> *root){
    // Write your code here.
    vector<vector<int>> answer;
    vector<int> pre,in,post;
    
    stack <pair<BinaryTreeNode<int> *,int>> s;
    s.push({root,1});
    if(root==NULL) return answer;
    while(!s.empty())
    {
        auto k=s.top();
        s.pop();
        
        BinaryTreeNode<int> * node=k.first;
        int number=k.second;
        if(number==1)
        {
            pre.push_back(node->data);
            s.push({node,number+1});
            
            if(node->left!=NULL)
                s.push({node->left,1});
        }
        else if(number==2)
        {
            in.push_back(node->data);
            s.push({node,number+1});
            if(node->right!=NULL)
                s.push({node->right,1});
        }
        else
        {
            post.push_back(node->data);
        }
    }
    answer.push_back(in);
    answer.push_back(pre);
    answer.push_back(post);
    return answer;
}

```
***

VERTICAL ORDER TRAVERSAL
https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/

Used Level order Traversal(QUEUE) + MAP
```
class Solution {
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
     
        queue <pair<TreeNode *, pair<int,int>>> Q;
        map <int, map<int , multiset<int>>> MAP;
        
        Q.push({root,{0,0}});
        
        while(!Q.empty())
        {
            auto item= Q.front();
            TreeNode* node=item.first;
            
            int a= item.second.first;
            int b= item.second.second;
            Q.pop();
            
            MAP[a][b].insert(node->val);
            
            if(node->left) Q.push({node->left,{a-1,b+1}});
                
            if(node->right) Q.push({node->right,{a+1,b+1}});
        }
        
        vector<vector<int>> answer;
        
        for(auto m:MAP)
        {
            vector<int> vo;
            for(auto n:m.second)
            {
                vo.insert(vo.end(),n.second.begin(),n.second.end());
            }
            answer.push_back(vo);
        }
        return answer;
    }
};
```
***

ROOT TO NODE PATH IN A BINARY TREE
https://www.interviewbit.com/problems/path-to-given-node/

```
bool find(TreeNode* root,vector<int>&a,int B)
{
    if(root==NULL)
    return false;
    
    a.push_back(root->val);
    
    if(root->val==B)
        return true;
        
    if(find(root->left,a,B) || find(root->right,a,B))
        return true;
    
    a.pop_back();
    return false;
}
vector<int> Solution::solve(TreeNode* A, int B) {
    
    vector<int> a;
    if(A==NULL)
    return a;
    
    find(A,a,B);
    
    return a;
}
```
***
TC-$O(N)$
SC-$O(N)$

MAXIMUM WIDTH OF A BINARY TREE
https://leetcode.com/problems/maximum-width-of-binary-tree/

Think of levels with indexing -> Level order traversal -> Queue< pair<TreeNode *,double> >
```
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        
        if(!root) return 0;
        
        queue< pair<TreeNode *,double> > Q;
        Q.push({root,0});
        double maximum_width=-1e9;
        
        while(!Q.empty())
        {
        auto item=Q.front();
        double mi=item.second;
        int size=Q.size();
        double first=0,last=0;
            
        for(int i=0;i<size;i++)    
        {
            auto object= Q.front();
            TreeNode *t= object.first;
            double index= object.second - mi;
            Q.pop();
            
            if(i==0) first= index;
            if(i==size-1) last=index;
            
            if(t->left) Q.push({t->left,2*index+1});
            if(t->right) Q.push({t->right,2*index+2});
        }
            maximum_width=max(maximum_width,(last-first+1));
            
        }
        return maximum_width;
    }
};
```
***