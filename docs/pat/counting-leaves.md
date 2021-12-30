# Counting Leaves
题目链接[1004 Counting Leaves (30 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805521431773184)

## 题干大意

输出树的叶节点个数。

## 思路

用BFS也就是层序遍历

## 问题

一些迭代器、索引的问题，还是写注释要好，思路清晰，不会乱

## AC代码（待写注释）
```cpp
    #include <iostream>
    #include <vector>
    #include <queue>
    using namespace std;

    int traverse(vector<vector<int>> nodes, vector<int>& cnt) {
        queue<int> Q;
        Q.push(1);
        int layer = 1;
        vector<int> num;
        num.push_back(nodes[1].size());
        while (!Q.empty()) {
            int size = int(num.size());
            auto p = Q.front();
            for (int i = 0; i < size; ++i) { // num.size()为孩子个数
                if (nodes[p].empty())
                    ++cnt[layer];
                ++p;
            }
            num.clear();
            for (int i = 0; i < size; ++i) {
                auto q = Q.front();
                Q.pop();
                if (!nodes[q].empty()) {
                    for (auto it = nodes[q].begin(); it != nodes[q].end(); ++it) {
                        Q.push(*it);
                        num.push_back(nodes[*it].size());
                    }
                }
            }
            ++layer;
        }
        return --layer;
    }
    int main()
    {
        int N, M;
        cin >> N >> M;
        vector<vector<int>> nodes(N + 1);
        for (int i = 0; i != M; ++i) {
            int parent, K, child;
            cin >> parent >> K;
            for(int j = 0; j < K; ++j) {
                cin >> child;
                nodes[parent].push_back(child);
            }
        }
        vector<int> cnt(N + 1, 0);
        auto layer = traverse(nodes, cnt);
        for (auto i = 1; i <= layer; ++i) {
            cout << cnt[i];
            if (i != layer)
                cout << " ";
        }
        return 0;
    }
```
