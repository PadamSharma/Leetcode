# 1379. Find a Corresponding Node of a Binary Tree in a Clone of That Tree
Easy

Given two binary trees original and cloned and given a reference to a node target in the original tree.

The cloned tree is a copy of the original tree.

Return a reference to the same node in the cloned tree.

Note that you are not allowed to change any of the two trees or the target node and the answer must be a reference to a node in the cloned tree.

> ### Recursive DFS

```c++
class Solution {
public:
    void dfs(TreeNode* cloned, TreeNode* target, TreeNode* &ans){
        if(!cloned){
            return;
        }
        if(cloned->val==target->val){
            ans = cloned;
            return;
        }
        dfs(cloned->left, target, ans);
        dfs(cloned->right, target, ans);
    }
    TreeNode* getTargetCopy(TreeNode* original, TreeNode* cloned, TreeNode* target) {
        TreeNode* ans;
        dfs(cloned, target, ans);
        return ans;
    }
};
```

# 938. Range Sum of BST
Easy

Given the root node of a binary search tree and two integers low and high, return the sum of values of all nodes with a value in the inclusive range [low, high].

> As this is a BST, right of a node has higher value and vice versa, so using this fact to make a recursive call.

```c++
class Solution {
public:
    int rangeSumBST(TreeNode* root, int low, int high) {
        if(!root){
            return 0;
        }
        if(root->val>high){
            return rangeSumBST(root->left, low, high);
        }
        if(root->val<low){
            return rangeSumBST(root->right, low, high);
        }
        return root->val + rangeSumBST(root->left, low, high) + rangeSumBST(root->right, low, high);
    }
};
```

# 

```c++

```