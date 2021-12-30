# Scientific Notation 
题目链接：[1073 Scientific Notation (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805395707510784)

## 题干大意

将科学计数法的数字表示成正常的形式

## 思路

限定为`E`的位置，然后根据指数正负分情况，总结规律

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <string>
    using namespace std;

    int main() {
        string str;
        cin >> str;
        if (str[0] == '-')
            cout << '-';
        int pos = 0;
        while (str[pos] != 'E')
            ++pos;
        int exp = 0; // 计算指数
        for (int i = pos + 2; i < str.length(); ++i) {
            exp = exp * 10 + (str[i] - '0');
        }
        if (exp == 0) {
            for (int i = 1; i < pos; ++i)
                cout << str[i];
        }
        if (str[pos + 1] == '-') {
            cout << "0.";
            for (int i = 0; i < exp - 1; ++i)
                cout << 0;
            cout << str[1];
            for (int i = 3; i < pos; ++i)
                cout << str[i];
        }
        else {
            for (int i = 1; i < pos; ++i) {
                if (str[i] == '.')
                    continue;
                cout << str[i];
                if (i == exp + 2 && pos - 3 != exp) // 3为原小数点位置
                    cout << ".";
            }
            for (int i = 0; i < exp - (pos - 3); ++i)
                cout << 0;
        }
        return 0;
    }
```    
