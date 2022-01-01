# Speech Patterns

题目链接：[1071 Speech Patterns (25 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805398257647616)

## 题干大意

统计出现次数最多的单词

## 思路

统计单词数，也就是要分割单词，这里注意单词有大小写字母和数字组成，以及对非有效字符的判断

## AC代码
```cpp linenums="1"
#include <iostream>
#include <map>
using namespace std;

int main() {
  map<string, int> count;
  string str;
  getline(cin, str);
  int i = 0;
  while (i < str.length()) {
    string word;
    while (i < str.length() && isalnum(str[i])) {
      if (str[i] >= 'A' && str[i] <= 'Z') // 改为小写
        str[i] += 32;
      word += str[i++];
    }
    if (!word.empty()) { // 统计出是个单词
      if (count.find(word) == count.end())
        count[word] = 1;
      else
        ++count[word];
    }
    while (i < str.length() && !isalnum(str[i]))
      ++i; // 跳过非单词字符
  }
  string ans;
  int max = 0;
  for (auto &it : count) {
    if (it.second > max) {
      max = it.second;
      ans = it.first;
    }
  }
  cout << ans << " " << max;
  return 0;
}
```
