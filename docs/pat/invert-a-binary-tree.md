# Invert a Binary Tree

题目链接：[1102 Invert a Binary Tree (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805365537882112)

## 题干大意

给出二叉树节点个数，以及各个节点的孩子信息，要求输出反转后的二叉树的层序与中序遍历结果

## 思路

关键在于构建二叉树，我还是习惯于用动态形式的树，所以详细看代码吧，很常规

## AC代码
```cpp linenums="1"
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct node {
  int data{};
  struct node* left{nullptr};
  struct node* right{nullptr};
  struct node *parent{nullptr}; // 受邓公的教诲，现在我是真感觉多用一个父节点是多么的明了
};
int n;
vector<int> in; // NOLINT
vector<int> layer; // NOLINT
vector<string> str;

node* construct() {
  node** p = new node*[n]; // 存储所有的指向节点的指针
  for (int i = 0; i < n; ++i) { // 注意二维数组建立的时候，每一行都要在申请一下空间
    p[i] = new node; // 给每一行开辟一个节点
    p[i]->data = i;
  }
  for (int i = 0; i < n; ++i) {
    if (str[i][0] != '-') { // 给出了孩子信息，也就给出了父亲信息
      p[i]->left = p[str[i][0] - '0'];
      p[str[i][0] - '0']->parent = p[i];
    }
    if (str[i][2] != '-') {
      p[i]->right = p[str[i][2] - '0'];
      p[str[i][2] - '0']->parent = p[i];
    }
  }
  node *root;
  for (int i = 0; i < n; ++i) { // 找出根节点
    if (p[i]->parent == nullptr) {
      root = p[i];
      break;
    }
  }
  queue<node*> q;
  q.push(root);
  while (!q.empty()) {
    node* temp = q.front();
    q.pop();
    if (temp->left)
      q.push(temp->left);
    if (temp->right)
      q.push(temp->right);
    swap(temp->left, temp->right); // 翻转树，即将每个节点的左右子树交换
  }
  return root;
}

void in_traverse(node* &tree) { // 常规
  if (!tree)
    return;
  in_traverse(tree->left);
  in.emplace_back(tree->data);
  in_traverse(tree->right);
}

void layer_traverse(node* &tree) { // 常规
  queue<node*> q;
  q.push(tree);
  while (!q.empty()) {
    node* temp = q.front();
    q.pop();
    if (temp->left)
      q.push(temp->left);
    if (temp->right)
      q.push(temp->right);
    layer.emplace_back(temp->data);
  }
}

int main()
{
  cin  >> n; cin.get();
  str.resize(n);
  for (int i = 0; i < n; ++i)
    getline(cin, str[i]);
  node* tree = construct();
  in_traverse(tree);
  layer_traverse(tree);
  for (auto &it : layer) {
    cout << it;
    if (&it != &layer.back())
      cout << " ";
    else
      cout << "\n";
  }
  for (auto &it : in) {
    cout << it;
    if (&it != &in.back())
      cout << " ";
    else
      cout << "\n";
  }
  return 0;
}
```
