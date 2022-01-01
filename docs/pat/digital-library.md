# Digital Library
题目链接：[1022 Digital Library (30 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805480801550336)

## 题干大意

给书的信息，按照给定的部分信息查出来书的`id`，这里有个问题就是，一本书可能与多个作者、出版社等对应。

## 思路

使用`map<string, set<int>>`这种类型，也就是将一个`string`如作者，跟多个书的`id`对应。

这里又学到了通过`cout`控制输出的位数：

    #include <iomanip>
    cout << setw(n) << setfill(c); // 通过设置n个位，不足的用c填充

以及`cin.peek()`判断是否读到了行末，这个函数返回当前输出流中指针指向的字符，指针不后移动，而`cin.get()`读入当前的字符并指针向后移动一个

    if (cin.peek() == '\n') { // 判断是行末
        cin.get(); // 读取出换行符
        break; // 进一步操作，比如退出现在的循环（如果在循环内的话）
    }

## AC代码
```cpp linenums="1"
#include <iostream>
#include <map>
#include <iomanip>
#include <set>
using namespace std;

void print(map<string, set<int>> &mapSet, string &query) {
  if (mapSet.find(query) == mapSet.end())
    cout << "Not Found\n";
  else {
    for (auto &set : mapSet[query])
      cout << setw(7) << setfill('0') << set << "\n"; // 控制输出位数，以0填充
  }
}

int main() {
  ios::sync_with_stdio(false);
  map<string, set<int>> mapTitle, mapAuthor, mapKey, mapPublisher, mapYear;
  int n, m, id;
  string title, author, key, publisher, year;
  cin >> n;
  while (n--) {
    cin >> id; cin.get();
    getline(cin, title); mapTitle[title].insert(id);
    getline(cin, author); mapAuthor[author].insert(id);
    while (cin >> key) {
      mapKey[key].insert(id);
      if (cin.peek() == '\n') { // 又学到一招，cin.peek()获取当前位置的字符，可以检测是否读到了行末
        cin.get();
        break;
      }
    }
    getline(cin, publisher); mapPublisher[publisher].insert(id);
    getline(cin, year); mapYear[year].insert(id);
  }
  cin >> m;
  int type; string query;
  while (m--) {
    cin >> type; cin.get(); cin.get();
    getline(cin, query);
    cout << type << ": " << query << endl;
    switch (type) {
      case 1:
        print(mapTitle, query); break;
      case 2:
        print(mapAuthor, query); break;
      case 3:
        print(mapKey, query); break;
      case 4:
        print(mapPublisher, query); break;
      case 5:
        print(mapYear, query); break;
      default: break;
    }
  }
  return 0;
}
```
