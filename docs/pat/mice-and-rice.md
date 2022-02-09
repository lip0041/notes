# Mice and Rice

题目链接：[1056 Mice and Rice (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805419468242944)

## 题干大意

晋级式比赛，给出每个选手（老鼠）最终的排名。

## 思路

注意⚠️：题目中给的顺序是参赛顺序的选手下标，而不是选手的参赛顺序，，，

> 参考《算法笔记》做的时候脑子很混乱，不清晰

关键在于找到，组数与最终排名的关系，如题目中给的11个老鼠，第一轮有4组，则在第一轮中淘汰下来的老鼠的排名就是5（4+1），第二轮有4个老鼠参赛，组数是2，则淘汰下来的额排名就是3（2+1），第三轮有2两个老鼠参赛，则淘汰下来的就是排名为2。

## AC代码

```cpp linenums="1"
#include <queue>
#include <iostream>
#include <utility>
using namespace std;

int main() {
  int p, g;
  cin >> p >> g;
  pair<int, int> mice[p];
  for (int i = 0; i < p; ++i)
    cin >> mice[i].first;
  queue<int> q;
  for (int i = 0; i < p; ++i) {
    int x; cin >> x;
    q.push(x);
  }
  int temp = p, group; // 当前参加的老鼠数和组数
  while (q.size() != 1) {
    if (temp % g == 0)
      group = temp / g;
    else
      group = temp / g + 1;
    for (int i = 0; i < group; ++i) {
      int max = q.front();
      for (int j = 0; j < g; ++j) {
        if (i * g + j >= temp)
          break;
        int front = q.front();
        if (mice[front].first > mice[max].first)
          max = front;
        mice[front].second = group + 1;
        q.pop();
      }
      q.push(max);
    }
    temp = group;
  }
  mice[q.front()].second = 1;
  for (int i = 0; i < p; ++i) {
    cout << mice[i].second;
    if (i < p - 1)
      cout << " ";
  }

  return 0;
}
```
