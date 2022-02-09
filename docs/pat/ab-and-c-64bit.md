---
# A+B and C (64bit)
题目链接[1065 A+B and C (64bit) (20 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805406352654336)

## 不能用cin的原因

链接：
[[C++]--PAT-A1065 & cin与scanf](https://www.lip0041.top/2021/02/cpp-pat-a1065/ "[C++]--PAT-A1065 & cin与scanf")

## 题干大意

给出三个64位的整数，A,B,C，判断$A+B>C$是否成立

## 思路

使用`long long`存储，进行判断计算即可。

## 问题

此题用`cin`最后一个测试样例过不了，只能用`scanf`具体分析见
[[C++]--PAT-A1065 & cin与scanf](https://www.lip0041.top/2021/02/cpp-pat-a1065/ "[C++]--PAT-A1065 & cin与scanf")

## AC代码

```cpp linenums="1"
#include <iostream>
#include <cstdio>
using namespace std;

int main()
{
  int T;
  cin >> T;
  for(auto k = 0; k != T; ++k)
  {
    long long a, b, c;
    //cin >> a >> b >> c;
    scanf("%lld%lld%lld", &a, &b, &c);
    auto res = a + b;
    bool flag;
    if(a > 0 && b > 0 && res < 0)
      flag = true;
    else if(a < 0 && b < 0 && res >= 0)
      flag = false;
    else if(res > c)
      flag = true;
    else 
      flag = false;
    if(flag)
      cout << "Case #" << k+1 << ": true" << endl;
    else
      cout << "Case #" << k+1 << ": false" << endl;
  }
  return 0;
}
```
