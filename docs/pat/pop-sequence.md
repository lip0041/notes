# Pop Sequence
题目链接：[1051 Pop Sequence (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805427332562944)

## 题干大意

检测给定的栈输出序列是否是正确的栈输出序列

## 思路

根据输入序列，模拟栈混洗，最终辅助栈空则是正确的

## AC代码

```cpp linenums="1"
#include <stack>
#include <iostream>
#include <vector>
using namespace std;

int main() {
  int M, N, K;
  cin >> M >> N >> K;
  while (K--) {
    vector<int> pop;
    for (int i = 0; i < N; ++i) {
      int x; cin >> x;
      pop.emplace_back(x);
    }
    stack<int> s;
    bool status = true; // 判断在模拟过程中是否辅助栈的大小超过了M
    int j = 0;
    for (int i = 0; i < N;) {
      if (s.empty()) { // 栈空时，直接入
        s.push(++i);
        continue;
      }
      if(s.top() != pop[j]) { // 当此时栈顶元素不等于要输出的元素时，入栈
        if (s.size() == M) { // 如果超过了设定大小M，直接退出，输出NO
          status = false;
          break;
        }
        s.push(++i);
      }
      else { // 此时相等，循环出栈（满足，栈顶=pop[j]
        while (!s.empty() && s.top() == pop[j]) {
          s.pop();
          ++j;
        }
      }
    }
    while (!s.empty() && s.top() == pop[j]) { // 由于最后一个值为N的元素入栈后，在for循环中没有检查，所以在此检查
      s.pop();
      ++j;
    }
    if (s.empty() && status) // 如果没有超过M且最终栈空，则输出yes
      cout << "YES";
    else
      cout << "NO";
    if (K)
      cout << "\n";
  }
  return 0;
}
```
