# Sign in and Sign out
题目链接[1006 Sign In and Sign Out (25 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805516654460928)
## 题干大意

根据时间，输出最早来和最晚走的人的`id`

## 思路

输入时即用`earliest`和`latest`处理保存当前已经输入的人中的最早和最晚

## AC代码
```cpp linenums="1"
#include <iostream>
using namespace std;

struct employee {
  string id;
  int hour{}, minute{}, second{};

}temp, earliest, latest;

bool great(employee &a, employee &b) {
  if (a.hour != b.hour)
    return a.hour > b.hour;
  else if (a.minute != b.minute)
    return a.minute > b.minute;
  else
    return a.second > b.second;
}

int main() {
  int n;
  cin >> n;
  earliest.hour = 24, earliest.minute = 60, earliest.second = 60;
  latest.hour = latest.minute = latest.second = 0;
  while (n--) {
    char c;
    cin >> temp.id >> temp.hour >> c >> temp.minute >> c >> temp.second;
    if (!great(temp, earliest))
      earliest = temp;
    cin >> temp.hour >> c >> temp.minute >> c >> temp.second;
    if (great(temp, latest))
      swap(temp, latest); // 注意用swap的话，只能交换一次，因为有两个值需要更新
  }
  cout << earliest.id << " " << latest.id;
  return 0;
}
```
