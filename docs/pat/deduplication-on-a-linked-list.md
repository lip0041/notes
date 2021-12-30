# Deduplication on a Linked List

题目链接：[1097 Deduplication on a Linked List (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805369774129152)

## 题干大意

链表的去重，绝对值相同即为重复

## 思路

设两个结果链表，分别存储，注意重复的链表不一定存在，要先判断是否为空才能输出

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <iomanip>
    #include <algorithm>
    using namespace std;

    const int MaxN = 1e6 + 10;
    const int MaxK = 1e4 + 10;
    struct node {
        int data{};
        int next{};
    }l[MaxN];
    int status[MaxK]{0};

    int main() {
        int N, first;
        vector<int> res1, res2;
        cin >> first >> N;
        int address;
        for(int i = 0; i < N; ++i) {
            cin >> address >> l[address].data >> l[address].next;
        }
        while(first != -1) {
            if (status[abs(l[first].data)] == 0) {
                res1.emplace_back(first);
                status[abs(l[first].data)] = 1; // 标记此数的绝对值已经出现
            }
            else
                res2.emplace_back(first);
            first = l[first].next;
        }
        for(int i = 0; i != res1.size() - 1; ++i)
            cout << setw(5) << setfill('0') << res1[i] << " "
                << l[res1[i]].data << " "
                << setw(5) << setfill('0')  << res1[i + 1] << "\n";
            cout << setw(5) << setfill('0') << res1[res1.size() - 1] << " "
                << l[res1[res1.size() - 1]].data << " " << -1 << "\n";
        if (!res2.empty()){
            for(int i = 0; i != res2.size() - 1; ++i)
                cout << setw(5) << setfill('0') << res2[i] << " "
                    << l[res2[i]].data << " "
                    << setw(5) << setfill('0')  << res2[i + 1] << "\n";
                cout << setw(5) << setfill('0') << res2[res2.size() - 1] << " "
                    << l[res2[res2.size() - 1]].data << " " << -1;
        }
        return 0;
    }
```
