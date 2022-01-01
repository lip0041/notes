# AB-Format
题目链接：[1001 A+B Format (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805528788582400)

## 题干大意

将`a+b`的值按照美式？的格式输出

## 思路

刚开始打算用求余运算做的，草率了，没有考虑到为0时应该输出连续的0，只拿了15分。然后考虑到按照字符串处理，用`to_string`函数，即可，除了最前面的，其他按照3个一输出即可。

## AC代码
```cpp linenums="1"
#include <iostream>
using namespace std;

int main() {
  int a, b;
  cin >> a >> b;
  int sum = a + b;
  if (sum < 0) {
    cout << "-";
    sum = -sum;
  }
  string ans = to_string(sum);
  int m = ans.length() % 3;
  for (auto i = 0; i < ans.length(); ++i) {
    cout << ans[i];
    if ((i - m + 1) % 3 == 0 && i != ans.length() - 1)
      cout << ',';
  }
  return 0;
}
```
