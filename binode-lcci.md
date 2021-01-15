## 面试题 17.12. BiNode
#### 题目描述
把二叉搜索树转换为单向链表（左孩子空，右孩子为后继），要求依然符合二叉搜索树的性质。  

#### 前置知识
二叉搜索树： 左子树不空的话，小于根节点；右子树不空的话，大于根节点；左右子树都是二叉搜索树。  

#### 分析
题目的样例输入是二叉搜索树。但是直接转化的话，就不符合大小关系了。如果单链表符合二叉搜索树的话，其实就是要从小到大的排序的。  
这个问题肯定是递归去做了，递归关系在哪儿呢？

#### 官方思路
关键点：众所周知，对二叉搜索树采用中序遍历就能得到一个升序序列。  
所以这个题就是，中序遍历，一边中序遍历一边改变指针。
第二个需要注意的就是，怎么找到这个返回值。  

#### 代码
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* ans = new TreeNode(-1); // 为了返回单向链表的头节点而多设的一个节点
    TreeNode* prev = NULL; // 指向当前节点的前一个节点
    TreeNode* convertBiNode(TreeNode* root) {
        dfs(root);
        return ans->right;
    }
    void dfs(TreeNode* root){
        if (root==NULL){return;}
        dfs(root->left);
        if(prev==NULL){// 第一个节点
            prev=root;// 记录第一个节点
            ans->right=root;// 记录它，它将作为单链表的表头
        }
        else{// 第一个节点之后的节点
            prev->right=root;// 前一个节点的右指针指向当前节点
            prev=root;// 更新perv指向
        }
        root->left=NULL;// 当前节点的左指针设为null
        dfs(root->right);
    }
};
```

#### 遇到报错问题
- C++的 new 得到的 return 是指针。  
```cpp
TreeNode* ans = new TreeNode(-1);  
```

- 和 null 做比较的东西要确保它是指针。