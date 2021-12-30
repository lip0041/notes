# Tree Traversals

题目链接：[1020 Tree Traversals (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805485033603072)

## 题干大意

给定一棵二叉树的节点数、后续遍历序列、中序遍历序列，要求输出其层序遍历序列

## 思路

中序遍历可以确定左右子树，后续遍历可以确定子树的根，先构造出二叉树，然后做层序遍历即可

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <queue>
    using namespace std;

    struct node {
        int data;
        struct node* left;
        struct node* right;
    };
    int n;
    vector<int> post; // NOLINT
    vector<int> in; // NOLINT
    vector<int> layer;

    node* construct(int in_l, int in_r, int post_l, int post_r) {
        if (in_r - in_l < 1) {
            return nullptr;
        }
        int key = post_r - 1;
        node *root = new node;
        root->data = post[key];
        int i = in_l;
        for (; i != in_r; ++i) {
            if (in[i] == post[key])
                break;
        }
        root->left = construct(in_l, i, post_l, post_r - in_r + i);
        root->right = construct(i + 1, in_r, post_r - in_r + i, post_r - 1);
        return root;
    }

    void traverse(node* & tree) {
        if (!tree)
            return;
        queue<node*> q;
        q.push(tree);
        while (!q.empty()) {
            node* front = q.front();
            q.pop();
            layer.emplace_back(front->data);
            if (front->left)
                q.push(front->left);
            if (front->right)
                q.push(front->right);
        }
    }

    int main()
    {
        cin  >> n;
        post.resize(n);
        in.resize(n);
        for (auto & it : post)
            cin >> it;
        for (auto & it : in)
            cin >> it;
        node *tree = construct(0, n, 0, n);
        traverse(tree);
        for (auto & it : layer) {
            cout << it;
            if (&it != &layer.back()) {
                cout << " ";
            }
        }
        return 0;
    }
```    
