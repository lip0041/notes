# Dating

题目链接：[1061 Dating (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805411985604608)

## 题干大意

前两个字符串第一个相同的表示星期，第二个相同的表示小时，后两个字符串第一个相同的位置表示分钟

## 思路

遍历，找符合要求的字符即可

## AC代码
```cpp linenums="1"
#include <iostream>
#include <vector>
#include <string>
using namespace std;

const vector<string> week{"MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"}; //用于转换星期
int main() {
  string str1, str2, str3, str4;
  cin >> str1 >> str2 >> str3 >> str4;
  int k;
  for (k = 0; k < str1.length() && k < str2.length(); ++k) { // 找星期
    if (str1[k] == str2[k] && str1[k] >= 'A' && str1[k] <= 'G') {
      cout << week[str1[k] - 'A'] << " ";
      break;
    }
  }
  for (k++; k < str1.length() && k < str2.length(); ++k) { // 接着找小时
    if (str1[k] == str2[k]) {
      if (str1[k] >= '0' && str1[k] <= '9') {
        cout << 0 << str1[k] - '0' << ":";
        break;
      }
      else if (str1[k] >= 'A' && str1[k] <= 'N') {
        cout << str1[k] - 'A' + 10 << ":";
        break;
      }
    }
  }
  for (k = 0; k < str3.length() && k < str4.length(); ++k) { // 找分钟
    if (str3[k] == str4[k]){
      if (str3[k] >= 'A' && str3[k] <= 'Z' '' str3[k] >= 'a' && str3[k] <= 'z') {
        k > 9 ? cout << k : cout << 0 << k;
        break;
      }
    }
  }
  return 0;
}
```
