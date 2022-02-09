# Hello World for U
题目链接[1031 Hello World for U (20 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805462535356416)

## 题干大意

将给定的字符串，按照U 型输出

## 思路

计算出`n1`、`n2`、`n3`，然后按行输出即可。由`n1 = n3`且不大于`n2`则有`n1 = n3  = (n + 2) / 3`的下整。

## AC代码

```cpp linenums="1"
#include <iostream>
using namespace std;

int main() {
  string str;
  cin >> str;
  int len = int(str.length());
  int n1 = (len + 2) / 3, n3 = n1, n2 = len + 2 - n1 - n3;
  for (int i = 0; i < n1 - 1; ++i) { // n1 - 1 rows
    cout << str[i];
    for (int j = 0; j < n2 - 2; ++j)
      cout << " ";
    cout << str[len - i - 1] << endl;
  }
  for (int i = 0; i < n2; ++i)
    cout << str[n1 + i - 1];
  return 0;
}
```
