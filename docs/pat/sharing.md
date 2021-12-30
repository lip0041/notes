# Sharing

题目链接：[1032 Sharing (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805460652113920)

## 题干大意

单词中的字母由链表指视，公共字母公用，找出第一个公共字母的地址

## 思路

先遍历一个单词，将其中的字母设为已被访问的状态，然后遍历另一个单词，当碰到已被访问的字母时表明，当前的字母即为所求字母

## AC代码
```cpp
    #include <iostream>
    #include <iomanip>
    using namespace std;

    struct node {
        int next{};
        bool status = false;
    }l[100010];

    int main() {
        int s1, s2, n;
        cin >> s1 >> s2 >> n;
        int address, next;
        char c;
        for (int i = 0; i < n; ++i) {
            cin >> address >> c >> next;
            l[address].next = next;
        }
        int p;
        for (p = s1; p != -1; p = l[p].next)
            l[p].status = true;
        for (p = s2; p != -1; p = l[p].next)
            if (l[p].status)
                break;
        if (p == -1)
            cout << -1;
        else
            cout << setw(5) << setfill('0') << p;
        return 0;
    }
```
