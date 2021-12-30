# World Cup Betting
题目链接[1011 World Cup Betting (20 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805504927186944)
## 题干大意

这个题，题目写的不明不白，我没太读懂，看了算法笔记，才知道，，，反正就是，选出每行最大的，按照公式输出就好。。。

## 思路

用一个`char`存放结果的字符，重新回顾一下`cout`的精度控制

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <iomanip> // 精度控制头文件
    using namespace std;

    char S[3] = {'W', 'T', 'L'};
    int main() {
        double ans = 1.0, max;
        int index;
        for (int i = 0; i < 3; ++i) {
            max = 0.0;
            for (int j = 0; j < 3; ++j) { // 每行分别处理
                double temp;
                cin >> temp;
                if (temp > max) {
                    max = temp;
                    index = j;
                }
            }
            ans *= max;
            cout << S[index] << " ";
        }
        cout << setiosflags(ios::fixed) << setprecision(2) << (ans * 0.65 - 1) * 2; // 精度处理格式
        return 0;
    }
```
