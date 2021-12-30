# Kuchiguse

题目链接：[1077 Kuchiguse (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805390896644096)

## 题干大意

输出最长公共后缀

## 思路

利用`algorithm`中的`reverse`函数，变为最长公共前缀，中间学习了一下`lambda`表达式

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <algorithm>
    using namespace std;

    bool fit(vector<string> spoken, int k) {
        bool flag = true;
        for (auto it = spoken.begin(); it != spoken.end() - 1; ++it) {
            string a = *it, b = *(it + 1);
            if (a[k] != b[k]) {
                flag = false;
                break;
            }
        }
        return flag;
    }

    int main() {
        int n; cin >> n;
        cin.get();
        vector<string> spoken(n);
        int min = 257;
        for (auto& s : spoken) { // 读入、翻转变为最长公共前缀，计算最短的长度
            getline(cin, s);
            reverse(s.begin(), s.end());
            if (min < s.length())
                min = s.length();
        }
        int k;
        for (k = -1; k < min;) {
            if (fit(spoken, k + 1))
                ++k;
            else
                break;
        }
        // 学习使用lambda表达式
        k < 0 ? cout << "nai" : 
                cout << [k](const string& str)->string { 
                        string ans = str.substr(0, k + 1); 
                        reverse(ans.begin(), ans.end()); 
                        return ans; 
                    } (spoken[0]);
        return 0;
    }
```
