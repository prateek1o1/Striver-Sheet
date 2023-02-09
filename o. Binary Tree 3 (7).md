# BINARY TREE 3

MAXIMUM PATH SUM
https://leetcode.com/problems/binary-tree-maximum-path-sum/

```
public:
    int solve(TreeNode* root,int &sum)
    {
        if(root==NULL) return 0;
        
        int leftadd,rightadd;
     		//Neglect Negative Return Value
        leftadd=max(0,solve(root->left,sum));
        rightadd=max(0,solve(root->right,sum));
        
        sum=max(sum,leftadd+rightadd+root->val);
        
        return root->val+max(leftadd,rightadd);
        
    }
    int maxPathSum(TreeNode* root) {
    
        int sum=-1e9;
        solve(root,sum);
        return sum;
    }
};
```
***
CONSTRUCT BINARY TREE FROM INORDER AND PREORDER
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

```
class Solution {
public:
    TreeNode * BobTheBuilder(vector<int>& preorder,int prestart,int preend, vector<int>& inorder,int instart,int inend,unordered_map<int,int>& inmap)
    {
        
        if(prestart>preend || instart>inend) return NULL;
        
        TreeNode * root=new TreeNode(preorder[prestart]);
        
        int inroot=inmap[root->val];
        int length=inroot-instart;
        
        root->left=BobTheBuilder(preorder,prestart+1,prestart+length,inorder,instart,inroot-1,inmap);
        root->right=BobTheBuilder(preorder,prestart+length+1,preend,inorder,inroot+1,inend,inmap);
        
        return root;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        
        unordered_map<int,int> inmap;
        
      int  n=inorder.size();
        for(int i=0;i<n;i++)
        {
            inmap[inorder[i]]=i;
        }
        return BobTheBuilder(preorder,0,n-1,inorder,0,n-1,inmap);
    }
};
```
***
CONSTRUCT BINARY TREE FROM INORDER AND POSTORDER
https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

int inroot=inmap[root->val];
int length=inend-inroot;
```
class Solution {
public:
    TreeNode *BobTheBuilder(vector<int>& inorder, int instart,int inend,vector<int>& postorder,int poststart,int postend,map<int,int> &inmap)
    {
        if(instart>inend || poststart>postend ) return NULL;
        TreeNode * root=new TreeNode(postorder[postend]);
        
        int inroot=inmap[root->val];
        int length=inend-inroot;
        
        root->left=BobTheBuilder(inorder,instart,inroot-1,postorder,poststart,postend-length-1,inmap);
        root->right=BobTheBuilder(inorder,inroot+1,inend,postorder,postend-length,postend-1,inmap);
        
            return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        
        map<int,int> inmap;
        
        for(int i=0;i<inorder.size();i++)
        {
            inmap[inorder[i]]=i;
        }
        int n=inorder.size();
        return BobTheBuilder(inorder,0,n-1,postorder,0,n-1,inmap);
    }
};
```

int inroot=inmap[root->val];
int length=inroot-instart;
```
class Solution {
public:
    TreeNode *BobTheBuilder(vector<int>& inorder, int instart,int inend,vector<int>& postorder,int poststart,int postend,map<int,int> &inmap)
    {
        if(instart>inend || poststart>postend ) return NULL;
        TreeNode * root=new TreeNode(postorder[postend]);
        
        int inroot=inmap[root->val];
        int length=inroot-instart;
        
        root->left=BobTheBuilder(inorder,instart,inroot-1,postorder,poststart,poststart+length-1,inmap);
        root->right=BobTheBuilder(inorder,inroot+1,inend,postorder,poststart+length,postend-1,inmap);
        
            return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        
        map<int,int> inmap;
        
        for(int i=0;i<inorder.size();i++)
        {
            inmap[inorder[i]]=i;
        }
        int n=inorder.size();
        return BobTheBuilder(inorder,0,n-1,postorder,0,n-1,inmap);
    }
};
```

***
SYMMETRIC BINARY TREE
https://leetcode.com/problems/symmetric-tree/

```
class Solution {
public:
    bool helper(TreeNode* LEFT,TreeNode* RIGHT)
    {
        if(LEFT==NULL || RIGHT==NULL) return LEFT==RIGHT;
        
        if(LEFT->val!=RIGHT->val) return false;
        
        return helper(LEFT->left,RIGHT->right) && helper(LEFT->right,RIGHT->left);
        
    }
    bool isSymmetric(TreeNode* root) {
        
        return root==NULL || helper(root->left,root->right);
    }
};
```
***
FLATTEN BINARY TREE TO LINKED LIST
https://leetcode.com/problems/flatten-binary-tree-to-linked-list/
	
```
class Solution {
public:
    void flat(TreeNode* root, TreeNode*& previous)
    {
         if(root==NULL) return;
        
        flat(root->right,previous);
        flat(root->left,previous);
        
        root->right=previous;
        root->left=NULL;
        previous=root;
    }
    
    void flatten(TreeNode* root) {
        
        TreeNode* previous=NULL;
        flat(root,previous);
    }
};
```
Morris Traversal

```
class Solution {
public:
    void flatten(TreeNode* root)
    {
    TreeNode* current=root;
        
        while(current!=NULL)
        {
            if(current->left!=NULL)
            {
              TreeNode* previous=current->left;
                
                while(previous->right)
                {
                    previous=previous->right;
                }
                previous->right=current->right;
                current->right=current->left;
                current->left=NULL;
            }
            current=current->right;
        }
    }
};

```
***
CHECK IF BINARY TREE IS THE MIRROR OF ITSELF OR NOT
https://practice.geeksforgeeks.org/problems/mirror-tree/1

```
class Solution {
  public:
    // Function to convert a binary tree into its mirror tree.
    void mirror(Node* node) {
        // code here
        if(node==NULL) return;
        
        mirror(node->left);
        mirror(node->right);
        Node* temporary;
        temporary=node->left;
        node->left=node->right;
        node->right=temporary;
    }
};
```
***
CHECK FOR CHILDREN SUM PROPERTY
https://www.codingninjas.com/codestudio/problems/childrensumproperty_790723?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website

```
void changeTree(BinaryTreeNode < int > * root) {
    // Write your code here.
    if(root==NULL) return;
    int child=0;
    if(root->left) child+=root->left->data;
    if(root->right) child+=root->right->data;
    
    if(child >= root->data) root->data=child;
    else
    {
      if(root->left) root->left->data = root->data;
      if(root->right) root->right->data = root->data;
    }
    changeTree(root->left);
    changeTree(root->right);
    
    int total=0;
    if(root->left) total+=root->left->data;
    if(root->right) total+=root->right->data;
    if(root->left || root->right) root->data=total;
}  
```
***