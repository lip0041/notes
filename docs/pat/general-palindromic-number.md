# General Palindromic Number
题目链接：[1019 General Palindromic Number (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805487143337984)

## 题干大意

D进制问题+判断回文数

## 思路

很常规，只是两个问题结合在一起而已

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    using namespace std;

    int main() {
        int n, b;
        cin >> n >> b;
        vector<int> ans;
        do {
            ans.push_back(n % b);
            n /= b;
        } while (n != 0);
        bool flag = true;
        for (auto i = 0; i != ans.size() / 2; ++i) {
            if (ans[i] != ans[ans.size() - i - 1]) {
                flag = false;
                break;
            }
        }
        flag ? (cout << "Yes\n") : (cout << "No\n");
        for (auto i = ans.size() - 1; i != -1; --i) {
            cout << ans[i];
            if (i)
                cout << " ";
        }
        return 0;
    }
```
