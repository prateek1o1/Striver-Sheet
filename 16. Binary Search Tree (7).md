# BINARY SEARCH TREE

POPULATE NEXT RIGHT POINTERS OF TREE
https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
1. Recursive
```
class Solution {
public:
    Node* connect(Node* root) {
        
        if(root==NULL) return root;
        

       if(root->left)    
       {
        root->left->next = root->right;
        if(root->next!=NULL) root->right->next= root->next->left;
        else root->right->next=NULL;    
        connect(root->left);
        connect(root->right);
       }
        return root;
    }
};
```
2. Iterative
```
class Solution {
public:
    Node* connect(Node* root) {
        
        if(root==NULL) return root;
        Node* pre=root;
        Node* cur=NULL;
            
        while(pre->left)
        {
            Node * cur=pre;
            
            while(cur)
            {
                cur->left->next = cur->right;
                if(cur->next) 
                    cur->right->next = cur->next->left;
                
                cur = cur->next;
            }
            
            pre=pre->left;
        }
        return root;
    }
};
```
***
SEARCH GIVEN KEY IN BST
https://leetcode.com/problems/search-in-a-binary-search-tree/
1. Recursive
```
class Solution {
public:
    void search(TreeNode* root,int val,TreeNode* &item)
    {
        
        if(root==NULL) return;
        
        if(root->val > val) search(root->left,val,item);
        
        else if (root->val < val) search(root->right,val,item);
        
        else item=root;
    }
    TreeNode* searchBST(TreeNode* root, int val) {
        
        TreeNode* item=NULL;
        search(root,val,item);
        return item;
    }
};
```

2. Iterative
```
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        
        while(root !=NULL && root->val!=val)
        {
            root=(root->val < val) ? root->right:root->left;
        }
        return root;
    }
};
```
***
CONSTRUCT BST FROM GIVEN KEYS
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/
```
class Solution {
public:
    Node* connect(Node* root) {
        if(root==NULL) return root;
        Node* pre=root;
        Node* cur=NULL;
            
        while(pre->left)
        {
            Node * cur=pre;
            while(cur)
            {
                cur->left->next = cur->right;
                if(cur->next) 
                cur->right->next = cur->next->left;
                cur = cur->next;
            }
            pre=pre->left;
        }
        return root;
    }
};
```
***
CONSTRUCT BST FROM PREORDER TRAVERSAL
https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/
```
public:
    TreeNode * build(vector<int>& preorder,int &i,int upperbound)
    {
        if(i==preorder.size() || preorder[i]>upperbound) return NULL;
        
        TreeNode * root=new TreeNode(preorder[i++]);
        
        root->left=build(preorder,i,root->val);
        root->right=build(preorder,i,upperbound);
        
        return root;
    }
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        
        int i=0;
        return build(preorder,i,INT_MAX);
    }
};
```
***
CHECK IF A BT IS BST OR NOT
https://leetcode.com/problems/validate-binary-search-tree/
```
class Solution {
public:
    bool check(TreeNode* root,double low,double high)
    {
        if(root==NULL) return true;
        
        if(root->val <= low) return false;
        
        if(root->val >= high) return false;
        
        if(check(root->left,low,root->val) && check(root->right,root->val,high))
            return true;
        else
            return false;
        
    }
    bool isValidBST(TreeNode* root) {
        
      return check(root,-1e11,1e11);
 
    }
};
```
***
FIND LCA OF TWO NODES IN BST
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        
        if(root==NULL) return root;
        int current=root->val;
        
        if(current > p->val && current > q->val) return lowestCommonAncestor(root->left,p,q);
        if(current < p->val && current < q->val) return lowestCommonAncestor(root->right,p,q);
        return root;
    }
};
```
***
FIND THE INORDER PREDECESSOR/SUCCESSOR OF A GIVEN KEY IN BST
https://practice.geeksforgeeks.org/problems/predecessor-and-successor/1

BRUTE FORCE- Find inorder traversal and do linear search or binary search=O(N)+O(N)/log(N)

```
void findPreSuc(Node* root, Node*& pre, Node*& suc, int key)
{

// Your code goes here
Node* temporary=root;
pre=NULL;
suc=NULL;

while(temporary!=NULL)
{
    if(temporary->key <= key)
    {
        temporary=temporary->right;
    }
    else
    {
        suc=temporary;
        temporary=temporary->left;
    }
}
temporary=root;

while(temporary!=NULL)
{
    if(temporary->key >= key)
    {
        temporary=temporary->left;
    }
    else
    {
        pre=temporary;
        temporary=temporary->right;
    }
}

}
```
***
$TC=O(Height)$
$SC=O(1)$