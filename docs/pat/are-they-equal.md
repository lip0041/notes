# Are They Equal
题目链接：[1060 Are They Equal (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805413520719872)

## 题干大意

给定精度，判断两个存储浮点数的字符串是否科学表达式相等

## 思路

> 参考了《算法笔记》,做的时候由于药物，脑子晕晕的，不能动脑分析情况，就直接看书了。

根据书中分析，要将字符串中保存的分为大于1和小于1两种，总体上是一个一个判断，然后删除前导零和小数点，由于`erase`的复杂度为`O(n)`，所以我采取了不删除的做法，实则是每个字符串最多删除一次（即删除小数点），运行速度更快。

## AC代码
```cpp
#include <iostream>
#include <string>
using namespace std;

int n;
bool isZero(string &s) {
  bool zero = true;
  for (auto &c : s) {
    if (c != '0') {
      zero = false;
      break;
    }
  }
  return zero;
}

void process(string &s, int &e) {
  int k = 0; // 记录第一个不为0的数字的下标
  while (s.length() > k && s[k] == '0') // 跳过前导零
    ++k;
  // 去除小数点（如果有）
  if (s[k] == '.') { // s为小于1的小数
    s.erase(s.begin() + k);
    while(s.length() > k && s[k] == '0') { // 去掉小数点后面的前导零
      ++k;
      --e; // 每去掉一个指数减一
    }
  }
  else { // s大于1，则此时k已经确定了
    while (k + e < s.length() && s[k + e] != '.') // 寻找小数点
      ++e; // e 是指数，也表示小数点离第一个不为零的数的距离
    if (k + e < s.length()) // 找到小数点，删除
      s.erase(s.begin() + k + e);
  }
  if (isZero(s)) // 判断是否为0
    e = 0;
  while (s.length() - k < n) // 如果有必要，补充精度
    s += '0';
  s = s.substr(k, n); // 取n个字符组成处理后的结果
}

int main() {
  string s1, s2;
  cin >> n >> s1 >> s2;
  int e1 = 0, e2 = 0;
  // 处理输入的字符串，去掉小数点（如果有），并计算指数e
  // 即最多仅执行一次erase
  process(s1, e1);
  process(s2, e2);
  if (s1 == s2 && e1 == e2)
    cout << "YES 0." << s1 << "*10^" << e1 << endl;
  else
    cout << "NO 0." << s1 << "*10^" << e1 << " 0." << s2 << "*10^" << e2 << endl;
  return 0;
}
```
