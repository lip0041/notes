# Read Number in Chinese

题目链接：[1082 Read Number in Chinese (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805385053978624)

## 题干大意

以中文的习惯读出数字。

## 思路

> 参考了《算法笔记》这本书。

由于中文中，有亿、万，在万中又有千、百、十，故每四个一组处理。其中需要特别注意的是空格的输出，先输出空格在输出字符串比较好。

## AC代码

```cpp linenums="1"
#include <iostream>
#include <vector>
using namespace std;

const char nums[10][5] = {"ling", "yi", "er", "san", "si", "wu", "liu", "qi", "ba", "jiu"};
const char wei[5][5] = {"Shi", "Bai", "Qian", "Wan", "Yi"};
int main() {
  int n; cin >> n;
  string ans = to_string(n);
  int left = 0, right = ans.length();
  if (n < 0) {
    cout << "Fu";
    ++left;
  }
  // 我的规范：一组的下标范围为 [left, right)
  while (right - left > 4)
    right -= 4;
  while (left < ans.length()) { 
    bool flag = false; // 表示一组中是否含有0
    bool group = false; // 表示该组是否有数
    while (left < right) { // 处理每一组
      if (left > 0 && ans[left] == '0')
        flag = true;
      else {
        if (flag) { // 一组中存在0， 输出0即处理完毕
          cout << " ling";
          flag = false;
        }
        if (n > 0 && left != 0 '' n < 0)
          cout << " ";
        cout << nums[ans[left] - '0'];
        group = true; // 表示该组有数
        if (left != right - 1) {
          cout << " " << wei[right - left - 2];
        }
      }
      ++left;
    }
    if (group && right != ans.length()) {
      cout << " " << wei[(ans.length() - right) / 4 + 2];
    }
    right += 4;
  }
  return 0;
}
```
