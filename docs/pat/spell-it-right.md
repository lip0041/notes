# Spell it Right
题目链接：[1005 Spell It Right (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805519074574336)

## 题干大意

将给定的数每一位加起来，输出和的每一位的英文

## 思路

字符串处理，用好`to_string`。另外，学习了如何在`auto`遍历中判断是最后一个元素

## AC代码
```cpp linenums="1"
#include <iostream>
using namespace std;

char number[11][6] = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten"};
int main() {
  string str;
  cin >> str;
  int sum = 0;
  for (auto &s : str) {
    sum += s - '0';
  }
  string ans = to_string(sum);
  for (auto &s : ans) {
    cout << number[s - '0'];
    if (&s != &ans.back()) // 判断是否是最后一个元素，比较地址
      cout << " ";
  }
  return 0;
}
```
