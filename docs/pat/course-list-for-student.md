# Course List for Student

题目链接：[1039 Course List for Student (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805447855292416)

## 题干大意

给定课程对应的选课学生，然后给你学生名字查询该学生选的课程信息。

## 思路

使用`map`，由于`unordered_map`效率更高，使用之建立学生名字与存储的下标的对应关系。

在`codeup`中提交的话会超时，解决办法是将去掉`map`、去掉`cin`改为`scanf`、去掉`cout`改为`printf`以及将`string`改为`char`数组。

## AC代码
```cpp linenums="1"
#include <iostream>
#include <unordered_map>
#include <algorithm>
#include <vector>
using namespace std;

int main() {
  int N, K;
  cin >> N >> K;
  vector<vector<int>> stu;
  unordered_map<string, int> map;
  int k = 0;
  for (int i = 0; i < K; ++i) {
    int id, num;
    cin >> id >> num;
    for (int j = 0; j < num; ++j) {
      string name;
      cin >> name;
      if (map.find(name) == map.end()) {
        map[name] = k++;
        stu.emplace_back();
      }
      stu[map[name]].emplace_back(id);
    }
  }
  for (int i = 0; i < N; ++i) {
    string name;
    cin >> name;
    cout << name << " " << ((map.find(name) == map.end()) ? 0 : stu[map[name]].size());
    if (map.find(name) == map.end()) {
      if (i != N - 1)
        cout << endl;
      continue;
    }
    sort(stu[map[name]].begin(), stu[map[name]].end());
    for (auto &entry : stu[map[name]])
      cout << " " << entry;
    if (i != N - 1)
      cout << endl;
  }
  return 0;
}
```

