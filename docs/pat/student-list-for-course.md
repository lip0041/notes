# Student List for Course

题目链接：[1047 Student List for Course (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805433955368960)

## 题干大意

跟`A1039`反过来了，给你学生信息，输出每个课程选的学生信息。

## 思路

刚开始，直接将学生名字存入`course`向量，但最后一个总超时，后来是用`unordered_map`存储学生下标与名字的映射，以为是`emplace_back` `string`的时候耗时，但最后一个还是超时，最后经过搜寻，才知道是`cout`导致的问题，所以这个题用不着`unordered_map`。

另外不得不吐槽一下，题目中本来就说末尾没有额外的空行，下面代码也没有对最后一行输出有判断就能`AC`，就很无语，，，

## `cout`超时问题分析

上述思路中，已经表述，初步写的代码中，过不了第三个测试点，一直超时，下面是我的处理分析过程：

经过搜寻资料，得知：`cout`比`printf`多个缓冲区，只有当缓冲区写满的时候才会真正输出，而当使用`std::endl`输出换行时，末尾会再运行一个`flush`强行清除缓冲区，这样就没能发挥`cout`中缓冲区的优化，所以显得运行时间要长。但当使用`"\n"`输出换行时，就跟`printf`差不多了（就本题而言）。

另外，`printf`与`cout`不要混用，因为在多线程环境下，他们的执行顺序不一定会是执行完一个再执行另一个，而一个不使用缓冲区的突然跳到使用缓冲区的输出方式，或者反过来，会造成非期望的结果。

所以，最终结论是，这道题，`cout`使用`\n`输出换行一样也能过！！！

## AC代码
```cpp linenums="1"
#include <iostream>
#include <vector>
#include <algorithm>
// #include <cstdio>
using namespace std;

int main() {
  int N, K;
  istream::sync_with_stdio(false); // 关闭同步，时间上会快个约200多ms
  cin >> N >> K;
  vector<vector<string>> course(K + 1);
  for (int i = 0; i < N; ++i) {
    string name;
    int num, id;
    cin >> name >> num;
    for (int j = 0; j < num; ++j) {
      cin >> id;
      course[id].emplace_back(name);
    }
  }
  for (int i = 1; i <= K; ++i) {
    // printf("%d %d\n", i, course[i].size());
    cout << i << " " << course[i].size() << "\n";
    // 同样使用 lambda 表达式，真的很简洁
    sort(course[i].begin(), course[i].end(), [](string a, string b){ return a < b; }); 
    for (auto &it : course[i]) {
      // printf("%s\n", it.c_str()); // c_str() 转换成c语言风格时字符串
      cout << it << "\n";
    }
  }
  return 0;
}
```
