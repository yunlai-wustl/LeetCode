# Binary Tree

## Binary Tree Traversal

### 144 Preorder Traversal (DFS)

[leetcode](https://leetcode.com/problems/binary-tree-preorder-traversal/)

Given the `root` of a binary tree, return *the preorder traversal of its nodes' values*.

```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> s;
        vector<int> result;
        if(root==nullptr) return result;
        s.push(root);

        while(!s.empty())
        {
            TreeNode* tmp=s.top();
            s.pop(); //note that this is right afer s.top; cannot be moved to after s.push
            result.push_back(tmp->val);
            if(tmp->right!=NULL)
                s.push(tmp->right);
            if(tmp->left!=NULL)
                s.push(tmp->left);
        }
        return result;
    }
};
```



### 145 Postorder Traversal (DFS)

[leetcode](https://leetcode.com/problems/binary-tree-postorder-traversal/submissions/)

Given the `root` of a binary tree, return *the postorder traversal of its nodes' values*.

similar with preorder traversal except 2 points:

- push left child first 
- reverse result

```c++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*> s;
        vector<int> result;
        if(root==nullptr) return result;
        s.push(root);

        while(!s.empty())
        {
            TreeNode* tmp=s.top();
            s.pop(); //note that this is right afer s.top; cannot be moved to after s.push
            result.push_back(tmp->val);
            if(tmp->left!=NULL)
                s.push(tmp->left);
            if(tmp->right!=NULL)
                s.push(tmp->right);
        }
        reverse(result.begin(),result.end());
        return result;
    }
};
```



### 94 Binary Tree inorder Traversal (need review)

[leetcode](https://leetcode.com/problems/binary-tree-inorder-traversal/)

iterative Method

```c++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        if(!root) return result;
        helper(root,result);
        return result;
    }
    void helper(TreeNode* node, vector<int> &v)
    {
        if(node==nullptr) return;
        helper(node->left,v);
        v.push_back(node->val);
        helper(node->right,v);
    }
};
```



### 102. Binary Tree Level Order Traversal (BFS)



Iterative

Time complexity: O(N), since every node is visited once

Space complexity: O(N) to keep the output structure which contains N node values

```c++
class Solution {
public:
    map<int,vector<int>> m;
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        BFS(root,0);
        for(auto tmp=m.begin();tmp!=m.end();tmp++)
            result.push_back(tmp->second);
        return result;
    }
    void BFS(TreeNode* root, int depth)
    {
        
        if(!root)
            return;
        m[depth].push_back(root->val);
        BFS(root->left,depth+1);
        BFS(root->right,depth+1);

    }
};
```

## Properties of Binary Tree

### 101.  Symmetric Tree

[leetcode](https://leetcode.com/problems/symmetric-tree/)

Recursive

time complexity: O(N) since go over each element

```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return helper(root->left,root->right);
    }
    bool helper(TreeNode* node1,TreeNode* node2)
    {
        if(node1==nullptr && node2==nullptr)
            return true;
        if(node1==nullptr || node2==nullptr)
            return false;
        return(node1->val==node2->val && helper(node1->left,node2->right) && helper(node1->right,node2->left));
    }
};
```

### 104. Max Depth of tree

[leetcode](https://leetcode.com/problems/maximum-depth-of-binary-tree/solution/) 

```c++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==nullptr)
            return 0;
        return max(maxDepth(root->left),maxDepth(root->right))+1;
    }
};
```

### 111. Minimum Depth of Binary Tree

[leetcode](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

Just replace the max with min

```c++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root==nullptr)
            return 0;
        return min(minDepth(root->left),minDepth(root->right))+1;
    }
};
```

### 222. Count Complete Tree Nodes

[leetcode](https://leetcode.com/problems/count-complete-tree-nodes/)

similar with the previous 

```c++
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root==nullptr)
            return 0;
        return countNodes(root->left)+countNodes(root->right)+1;
    }
};
```

### 110.Balanced Binary Tree (need review)

[leetcode](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of *every* node differ in height by no more than 1

```c++
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        if(root==nullptr)
            return true;
        return (abs(depth(root->left)-depth(root->right))<2)&&(isBalanced(root->left))&&(isBalanced(root->right));   
    }
    int depth(TreeNode* root)
    {
        if(root==nullptr)
            return 0;
        return max(depth(root->left),depth(root->right))+1;
    }
};
```



### 404. Sum of Left Leaves (need review)

Given the `root` of a binary tree, return *the sum of all left leaves.*

A **leaf** is a node with no children. A **left leaf** is a leaf that is the left child of another node.

2 points:

- no children
- left child of its parent

 ```c++
 class Solution {
 public:
     int sumOfLeftLeaves(TreeNode* root, bool isleft=false) {
         if(root==nullptr)
              return 0;
         if(root->left==nullptr && root->right==nullptr)
             return isleft? root->val:0;  
         return sumOfLeftLeaves(root->left,true)+sumOfLeftLeaves(root->right,false);
     }
 };
 ```



### 513.

### 112.

## edit Binary tree

### 226.

### 106.

### 654.

### 617.



# Binary Search Tree

