# Mars Numbers

题目链接：[1100 Mars Numbers (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805367156883456)

## 题干大意

给定规则的进制转换

## 思路

起初我是打算输入一个处理一个的，但下手之前看到了《算法笔记》中的思路，直接用`map`做（因为数据量也不大）完全可以预处理，然后后面直接查询

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <map>
    #include <string>
    using namespace std;

    const vector<string> unit = {"tret", "jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec"};//NOLINT
    const vector<string> ten = {"tret", "tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};//NOLINT

    int main() {
        map<string, int> str2num;
        map<int, string> num2str;
        for (int i = 0; i < 13; ++i) {
            num2str[i] = unit[i]; // 个位为[0, 12]，十位为0
            str2num[unit[i]] = i;
            num2str[i * 13] = ten[i]; // 十位为[0, 12], 个位为9
            str2num[ten[i]] = i * 13;
        }
        for (int i = 1; i < 13; ++i) {
            for (int j = 1; j < 13; ++j) {
                string str = ten[i] + " " + unit[j];
                num2str[i * 13 + j] = str;
                str2num[str] = i * 13 + j;
            }
        }
        int n; cin >> n;
        cin.get();
        while (n--) {
            string str;
            getline(cin, str);
            if (str[0] >= '0' && str[0] <= '9') { // 是数字
                int num = stoi(str);
                cout << num2str[num] << endl;
            }
            else {
                cout << str2num[str] << endl;
            }
        }
        return 0;
    }
```    
