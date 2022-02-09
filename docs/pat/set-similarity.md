# Set Similarity

题目链接：[1063 Set Similarity (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805409175420928)

## 题干大意

计算两个集合的相似度，即相同数字的个数占两个集合的总集合的比例

## 思路

明显要求去重，而且后面要计算两个集合的相同数字的个数，也暗含要排序（不然复杂度太高），所以选用`set`进行存储，其他就很常规。

再次回顾一下，`cout`控制输出的格式语句

    #include <iomanip> // 头文件
    using namespace std;
    
    cout << setiosflags(ios::fixed) << setprecision(n); // n为要求的精度

## AC代码

```cpp linenums="1"
#include <iostream>
#include <vector>
#include <iomanip>
#include <set>
using namespace std;

int count(set<int> a, set<int> b) {
  auto it1 = a.begin(), it2 = b.begin();
  int cnt = 0;
  while (it1 != a.end() && it2 != b.end()) {
    if (*it1 == *it2) {
      ++cnt;
      ++it1; ++it2;
    }
    else if (*it1 < *it2)
      ++it1;
    else
      ++it2;
  }
  return cnt;
}

int main() {
  int N;
  cin >> N;
  vector<set<int>> set(N + 1);
  for (int i = 1; i <= N; ++i) {
    int M; cin >> M;
    while (M--) {
      int num; cin >> num;
      set[i].insert(num);
    }
  }
  int K; cin >> K;
  cout << setiosflags(ios::fixed) << setprecision(1);
  while (K--) {
    int a, b;
    cin >> a >> b;
    int cnt = count(set[a], set[b]);
    cout << cnt / double(set[a].size() + set[b].size() - cnt) * 100 << "%\n";
  }
  return 0;
}
```
