# Linked List Sorting
题目链接：[1052 Linked List Sorting (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805425780670464)

## 题干大意

给给定链表排序

## 思路

调用`sort`函数，注意，题目中给的节点不一定都在链表上，且不一定给定的节点一定会组成一个链表，需要特殊判断

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <iomanip>
    #include <algorithm>
    using namespace std;

    const int MaxN = 1e6 + 10;
    struct node {
        int data{};
        int next{};
    }l[MaxN];

    bool cmp(int a, int b) {
        return l[a].data < l[b].data;
    }

    int main() {
        int N, first;
        vector<int> res;
        cin >> N >> first;
        int address;
        for(int i = 0; i < N; ++i) {
            cin >> address >> l[address].data >> l[address].next;
        }
        while(first != -1) {
            res.emplace_back(first);
            first = l[first].next;
        }
        if (res.empty()) { // 有效节点为0
            cout << 0 << " " << -1;
            return 0;
        }
        sort(res.begin(), res.end(), cmp);
        cout << res.size() << " " << setw(5) << setfill('0') << res[0] << "\n";
        for(int i = 0; i < res.size() - 1; ++i)
            cout << setw(5) << setfill('0') << res[i] << " "
                << l[res[i]].data << " "
                << setw(5) << setfill('0')  << res[i + 1] << "\n";

        cout << setw(5) << setfill('0') << res[res.size() - 1] << " "
            << l[res[res.size() - 1]].data << " " << -1;
        return 0;
    }
```    
