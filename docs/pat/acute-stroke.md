# Acute Stroke

题目链接：[1091 Acute Stroke (30 point(s)](https://pintia.cn/problem-sets/994805342720868352/problems/994805375457411072)

## 题干大意

理解题意很重要，这个题刚开始我没有读懂，感觉表述的不清楚，知道当我理解了`L`表示的是`layer`的时候，才终于理解题目给的是一个底确定的长方体区域，而不是整个三维空间（如果是，一直不知道怎么确定每个切片在xoy平面的联系）

## 思路

理解了题意之后，就知道这个题可以采用`BFS`遍历每个连通域，并将每个连通域中1的个数大于等于`T`的个数记下来，最后输出即可

## AC代码

```cpp linenums="1"
#include <iostream>
#include <queue>

using namespace std;
const int MaxM = 1287, MaxN = 129, MaxL = 61;
int pixel[MaxM][MaxN][MaxL];
bool status[MaxM][MaxN][MaxL]{false};
int M, N, L, T; // 注意是L层，每层是M*N，门槛是T

class Point {
  public:
  int x, y, z;
  Point(int a, int b, int c) : x(a), y(b), z(c) {}
  ~Point() = default;
  Point operator+ (Point add) const {
    return Point{x + add.x, y + add.y, z + add.z};
  }
  bool check() const {
    if (x >= M '' x < 0 '' y >= N '' y < 0 '' z >= L '' z < 0)
      return false; // 越界返回false
    if (pixel[x][y][z] == 0 '' status[x][y][z])
      return false; // 当前非肿块点，或已经被访问过，返回false
    return true;
  }
};
const Point adj[6] = { // 一个点的六个相邻点的移动方向 //NOLINT
  Point{0, 0, 1},
  Point{0, 0, -1},
  Point{1, 0, 0},
  Point{-1, 0, 0},
  Point{0, 1, 0},
  Point{0, -1, 0}
};

int BFS(int x, int y, int z) {
  int cur = 0; // 此次bfs中的符合的点的个数
  queue<Point> q;
  Point point{x, y, z};
  q.push(point);
  status[x][y][z] = true;
  while (!q.empty()) {
    Point top = q.front();
    ++cur;
    q.pop();
    for (auto i : adj) {
      point = top + i;
      if (point.check()) { // 经检测，新位置符合要求
        q.push(point); // 入队
        status[point.x][point.y][point.z] = true; // 并设置已经检测过
      }
    }
  }
  if (cur >= T)
    return cur;
  else
    return 0;
}

int main() {
  cin >> M >> N >> L >> T;
  for (int z = 0; z < L; ++z) {
    for (int x = 0; x < M; ++x) {
      for (int y = 0; y < N; ++y)
        cin >> pixel[x][y][z];
    }
  }
  int ans = 0;
  for (int z = 0; z < L; ++z) {
    for (int x = 0; x < M; ++x) {
      for (int y = 0; y < N; ++y)
        // 当前位置为1，且没被访问过，则从当前点开始BFS
        if (pixel[x][y][z] == 1 && !status[x][y][z])
          ans += BFS(x, y, z);
    }
  }
  cout << ans;
  return 0;
}
```
