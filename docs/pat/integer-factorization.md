# Integer Factorization
题目链接：[1103 Integer Factorization (30 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805364711604224)

## 题干大意

将给定的数拆成，指定个数的P次方的和，输出这些数中总和最大的那一组

## 思路

> 学习了《算法笔记》，提前将用到的这写指定的数初始化，后面直接就一个一个试就好了

主要是`DFS`的问题，借助全局变量会很方便

## AC代码
```cpp linenums="1"
#include <iostream>
#include <cmath>
#include <vector>

using namespace std;

int N, K, P, maxFacSum = -1; // 最大底数和
vector<int> fac, ans, temp; // fac存放不大于N的i^p的数, ans为结果，temp为中间量

void init() {
  int t = 0;
  double i = 0;
  while (t <=N ) {
    fac.emplace_back(t);
    t = int(pow(++i, P));
  }
}
/**
     * @param index 当前尝试的元素下标
     * @param cur_k 当前选中的元素个数
     * @param sum 当前选中的数的和
     * @param fac_sum 当前选中的底数和
     */
void DFS(int index, int cur_k, int sum, int fac_sum) {
  if (sum == N && cur_k == K) { // 找到量一个符合的序列
    if (fac_sum > maxFacSum) { // 选择底数和更大的
      ans = temp;
      maxFacSum = fac_sum;
    }
    return;
  }
  if (sum > N || cur_k > K)
    return;
  // 运行以下代码前提：sum当前和未超出N且当前选择的个数cur_k也未超出K
  if (index >= 1) { // fac[0] = 0, 不在选择范围内
    temp.emplace_back(index);
    // 选择当前index
    DFS(index, cur_k + 1, sum + fac[index], fac_sum + index);
    temp.pop_back();
    // 不选当前index
    DFS(index - 1, cur_k, sum, fac_sum);
  }
}

int main() {
  cin >> N >> K >> P;
  init();
  DFS(fac.size() - 1, 0, 0, 0);
  if (maxFacSum == -1)
    cout << "Impossible\n";
  else {
    cout << N << " = " << ans[0] << "^" << P;
    for (auto it = ans.begin() + 1; it != ans.end(); ++it)
      cout << " + " << *it << "^" << P;
  }
  return 0;
}
```
