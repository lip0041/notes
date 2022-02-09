# The Dominant Color

题目链接：[1054 The Dominant Color (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805422639136768)

## 题干大意

统计一个矩阵中超过半数（本题保证了），出现次数最多的值

## 思路

本来可以开辟一个很大的数组，m * n来保存每个可能的值，但是题目中的值范围为[0, 2^24]，过于大了，所以采用`map`映射的办法。

## AC代码

```cpp linenums="1"
#include <iostream>
#include <map>
using namespace std;

int main() {
  int m, n;
  ios::sync_with_stdio(false);
  cin >> m >> n;
  int color;
  map<int, int> count; // color与count次数的映射
  for (int i = 0; i < n; ++i) {
    for (int j = 0; j < m; ++j) {
      cin >> color;
      if (count.find(color) == count.end()) // 还未被统计
        count[color] = 1; // 计数为1
      else
        ++count[color];
    }
  }
  // 遍历map，求出最大的那个color
  int maxColor = 0, maxCount = 0;
  for (auto it = count.begin(); it != count.end(); ++it) {
    if (it->second > maxCount) {
      maxCount = it->second;
      maxColor = it->first;
    }
  }
  cout << maxColor << endl;
  return 0;
}
```
