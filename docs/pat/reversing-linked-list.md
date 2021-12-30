# Reversing Linked List
题目链接：[1074 Reversing Linked List (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805394512134144)

## 题干大意

翻转链表

## 思路

利用`reverse`函数即可。注意喜欢使用`cout`的，如何控制输出格式，以及用`"\n"`输出换行会减少时间。

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

    int main() {
        int first, N, K;
        vector<int> res;
        cin >> first >> N >> K;
        int address;
        for(int i = 0; i < N; ++i) {
            cin >> address >> l[address].data >> l[address].next;
        }
        while(first != -1) {
            res.emplace_back(first);
            first = l[first].next;
        }
        for(int i = 0; i + K <= res.size(); i += K)
            reverse(res.begin() + i, res.begin() + i + K);
        for(int i = 0; i < res.size() - 1; ++i)
            cout << setw(5) << setfill('0') << res[i] << " "
                << l[res[i]].data << " "
                << setw(5) << setfill('0')  << res[i + 1] << "\n";

        cout << setw(5) << setfill('0') << res[res.size() - 1] << " "
            << l[res[res.size() - 1]].data << " " << -1;
        return 0;
    }
```    
