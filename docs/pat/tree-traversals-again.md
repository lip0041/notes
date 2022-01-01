# Tree Traversals Again
题目链接：[1086 Tree Traversals Again (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805380754817024)

## 题干大意

给定二叉树的节点数，以及用栈实现的中序遍历的操作序列，要求给出后序遍历序列

## 思路

根据栈的操作序列我们很容易得出这棵树的前序遍历序列（即，`push`的顺序）和中序遍历序列（即，`pop`的顺序），然后根据前序和中序得出二叉树然后再后序遍历即可。

但，我第一反应没有想着这样子弄，可能是邓公的数据结构让我对中序遍历的迭代实现的形式有了更多的了解，我第一反应是直接根据栈的操作序列构造一棵树，即第一个一定是`push`然后这个`push`的一定的根节点，然后第一个`push`后紧跟的`push`一定都是一个左侧链，即均是上一个的左孩子；当上一个操作是`push`而当前操作是`pop`时，表明，此时已达当前左侧链的最底端，当前节点的左孩子为空，且当前节点已经被`pop`，此时应当转向其右孩子进行考察，当右孩子考察完毕后应该顺着父节点，一直找到未被`pop`的父节点，`pop`它然后转向它的右孩子。

详见代码

## AC代码
```cpp linenums="1"
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct node {
  int data;
  struct node *left;
  struct node *right;
  struct node *parent; // 方便回溯
  bool status{false}; // 为true时表示当前节点已被栈操作pop掉，即应当考察其右孩子（如果存在）
};
int n;
vector<int> post; // NOLINT

vector<string> op;
node* construct() {
  node *root = new node;
  root->data = op[0][5] - '0';
  if (op[0].size() == 7) // 一个坑，n取值可以是两位数，我采用的是字符串的处理方法，所以要考虑到这种情况。
    root->data = root->data * 10 + op[0][6] - '0';
  node *temp = root;
  bool flag = true;
  for (auto it = op.begin() + 1; it != op.end(); ++it) {
    if (flag && (*it)[1] == 'u') { // 此时表示temp要接入左孩子
      node *left = new node;
      int num = (*it)[5] - '0';
      if (it->size() == 7)
        num = num * 10 + (*it)[6] - '0';
      left->data = num;
      temp->left = left;
      left->parent = temp;
      temp = temp->left;
    }
    else if (flag && (*it)[1] == 'o') { // 表示temp左孩子为空，且temp被pop掉了
      flag = !flag;
      temp->status = true;
      temp->left = nullptr;
    }
    else if (!flag && (*it)[1] == 'o') { // 表示temp右孩子为空，且temp的最近一个未被pop的祖父该被pop
      temp->right = nullptr;
      temp = temp->parent;
      while (temp->status) // 找到还未被pop的祖父
        temp = temp->parent;
      temp->status = true; // 将其pop
    }
    else if (!flag && (*it)[1] == 'u') { // 表示temp存在右子树，接入
      flag = !flag;
      node *right = new node;
      int num = (*it)[5] - '0';
      if (it->size() == 7)
        num = num * 10 + (*it)[6] - '0';
      right->data = num;
      temp->right = right;
      right->parent = temp;
      temp = temp->right;
    }
  }
  return root;
}

void traverse(node* &tree) {
  if (!tree)
    return;
  traverse(tree->left);
  traverse(tree->right);
  post.emplace_back(tree->data);
}

int main()
{
  cin  >> n;
  cin.get();
  op.resize(2 * n);
  for (int i = 0; i < 2 * n; ++i)
    getline(cin, op[i]);
  node *tree = construct();
  traverse(tree);
  for (auto &it : post) {
    cout << it;
    if (&it != &post.back())
      cout << " ";
  }
  return 0;
}
```
