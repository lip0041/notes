# Proper Rebuild
## 题目大意

由给定的先序遍历、后序遍历序列，确定唯一的真二叉树的中序遍历序列

## 思路

真二叉树即每个内部节点都有两个孩子的二叉树。利用递归的思路创建树，然后中序遍历一下。
先序遍历的头一个节点一定是根结点，下一个一定是左孩子

## 问题

我过于想用c++写了，但是对c++又仅仅是入门阶段，以为`struct`不应该出现在一个成熟的c++代码中，后来才发现我错了，，

## AC代码
```cpp linenums='1'
//  main.cpp
//  ProperRebuild
//
//  Created by lip0041 on 2021/1/21.
//

#include <iostream>
#include <cstdio>
using namespace std;

const int MAX = 4e6 + 10;
int pre[MAX];
int post[MAX];

struct Node
{
    int data;
    struct Node *left;
    struct Node *right;
};

//创建树
struct Node * buildtree(int l1, int r1, int l2, int r2)
{
    //当前根结点
    struct Node *root = new struct Node;
    root->data = pre[l1];
    root->left = root->right = nullptr;
    //p为当前根的左孩子在后序遍历中的位置
    int p = 0;
    if(r2 == l2)
        return root;
    // 找下一个左根在post中的位置
    for(int i = l2; i <= r2; ++i)
        if(post[i] == pre[l1 + 1])
        {
            p = i;
            break;
        }
    //由p将post序列分开，t为左边子树的个数
    int t = p - l2 + 1;
    root->left = buildtree(l1+1, l1+t, l2, p);
    root->right = buildtree(l1+t+1, r1, p+1, r2-1);
    return root;
}

//中序遍历
void traversal(struct Node *root)
{
    if(root == nullptr)
        return;
    traversal(root->left);
    cout << root->data << " ";
    traversal(root->right);
}

int main()
{
    int n;
    cin >> n;
    for(int i = 0; i < n; ++i)
        cin >> pre[i];
    for(int i = 0; i < n; ++i)
        cin >> post[i];
    struct Node *root = buildtree(0, n-1, 0, n-1);
    traversal(root);
    return 0;
}
```

