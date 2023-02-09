# BINARY TREE 2
LEVEL ORDER TRAVERSAL/LEVEL ORDER TRAVERSAL IN SPIRAL FORM
https://leetcode.com/problems/binary-tree-level-order-traversal/

```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        
        queue <TreeNode *> Q;
        vector<vector<int>> L;
        
        if(root==NULL) return L;
        
        Q.push(root);
        while(!Q.empty())
        {
            int size=Q.size();
            
            vector<int> t;
            
            for(int i=0;i<size;i++)
            {
                TreeNode * node=Q.front();
                t.push_back(node->val);           
                Q.pop();
                if(node->left) Q.push(node->left);
                
                if(node->right) Q.push(node->right);
            }
            L.push_back(t);
        }
       return L; 
    }
};
```
***
HEIGHT OF A BINARY TREE
https://leetcode.com/problems/maximum-depth-of-binary-tree/

```
class Solution {
public:
    int maxDepth(TreeNode* root) {
        
        if(!root) return 0;
        
        int l=1+maxDepth(root->left);
        int r=1+maxDepth(root->right);
        
        return max(l,r);
        
        
    }
};
```
***
DIAMETER OF BINARY TREE
https://leetcode.com/problems/diameter-of-binary-tree/

```
class Solution {
public:
    int diameter(TreeNode *root, int& answer)
    {
        if(root==NULL) return 0;
        
        int lh = diameter(root->left,answer);
            
        int rh = diameter(root->right,answer);
        
        answer=max(answer,lh+rh);
        
        return 1+max(lh,rh);
    }
    int diameterOfBinaryTree(TreeNode* root) {
        
        int answer=0;
        diameter(root,answer);
        return answer;
    }
};
```
***
CHECK IF THE BINARY TREE IS HEIGHT BALANCED OR NOT
https://leetcode.com/problems/balanced-binary-tree/

```
class Solution {
public:
    int height(TreeNode* root)
    {
        if(root==NULL) return 0;
        
        int lh=height(root->left);
        int rh=height(root->right);
        
        if(lh==-1 || rh==-1) return -1;
        if(abs(lh-rh)>1) return -1;
        
        return 1+max(lh,rh);
    }
    bool isBalanced(TreeNode* root) {
    
        if(height(root)!=-1)
            return true;
        else
            return false;
        
    }
};
```
***
LEAST COMMON ANCESTOR IN BINARY TREE
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        
        if(root==NULL || root==p || root==q)
            return root;
        
        TreeNode * left=lowestCommonAncestor(root->left,p,q);
        TreeNode * right=lowestCommonAncestor(root->right,p,q);
        
        if(left==NULL)
            return right;
        if(right ==NULL)
            return left;
        else
        {
            return root;
        }
    }
};
```
***
CHECK IF TWO TREES ARE IDENTICAL OR NOT
https://leetcode.com/problems/same-tree/

Note- inorder/preorder/postorder are all same.

```
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
     //preorder
     if(p==NULL || q==NULL)
         return (p==q);
        
     return p->val==q->val && isSameTree(p->left,q->left) && isSameTree(p->right,q->right);
    }
};
```
***
ZIGZAG TRAVERSAL OF BINARY TREE
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

```
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
     
        vector<vector<int>> answer;
        if(root==NULL)
            return answer;
        
        queue<TreeNode *> Q;
        Q.push(root);
        bool LR=true;
        while(!Q.empty())
        {
            int size=Q.size();
            vector<int> t(size);
            for(int i=0;i<size;i++)
            {   
                int index;
                TreeNode * node=Q.front();
                Q.pop();
                if(LR==true) 
                {
                    index=i;
                }
                else
                {
                    index=size-1-i;
                }
                
                t[index]=node->val;
                
                if(node->left) Q.push(node->left);
                
                if(node->right) Q.push(node->right);
                    
            }
            LR=!LR;
            answer.push_back(t);
            
        }
        return answer;
    }
};

```
***
BOUNDARY TRAVERSAL OF BINARY TREE
https://practice.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1

```
class Solution {
public:
    bool isleaf(Node *root)
    {
        if(root->left==NULL && root->right==NULL) return true;
        else return false;
    }
    void addleft(Node * root , vector<int> &result)
    {
        Node *cur=root->left;
        while(cur!=NULL)
        {
        if(!isleaf(cur)) result.push_back(cur->data);
        
        if(cur->left) cur=cur->left;
        else cur=cur->right;
        }
        
    }
    void addleaf(Node * root , vector<int> &result)
    {
        if(isleaf(root))
        {
            result.push_back(root->data);
            return;
        }
        else
        {
        if(root->left) addleaf(root->left,result);
        if(root->right) addleaf(root->right,result);
        }
    }
    void addright(Node * root , vector<int> &result)
    {
        vector<int> dummy;
        Node *cur=root->right;
        while(cur!=NULL)
        {
        if(!isleaf(cur)) dummy.push_back(cur->data);
        
        if(cur->right) cur=cur->right;
        else cur=cur->left;
        }
        for(int i=dummy.size()-1;i>=0;i--)
        result.push_back(dummy[i]);
        
    }
    vector <int> boundary(Node *root)
    {
        vector <int> result;
        if(root==NULL) return result;
        if(!isleaf(root)) result.push_back(root->data);
        
        addleft(root,result);
        addleaf(root,result);
        addright(root,result);
        
        return result;
    }
};
```
***