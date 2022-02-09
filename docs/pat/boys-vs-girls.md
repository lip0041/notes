# Boys vs Girls
题目链接[1036 Boys vs Girls (25 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805453203030016)
## 题干大意

仍是在输入中处理数据，找最大，最小，只不过这里将数据分成了两类，男性和女性

## 思路

常规，注意判断是否存在最值修改输出格式

## AC代码

```cpp linenums="1"
#include <iostream>
using namespace std;

struct Student {
  string name;
  string id;
  int score;
}male, female, temp;

int main() {
  male.score = 101, female.score = -1;
  int n; char gender;
  cin >> n;
  while (n--) {
    cin >> temp.name >> gender >> temp.id >> temp.score;
    if (gender == 'M' && temp.score < male.score)
      swap(male, temp);
    else if (gender == 'F' && temp.score > female.score)
      swap(female, temp);
  }
  if (female.score == -1)
    cout << "Absent" << endl;
  else
    cout << female.name << " " << female.id << endl;
  if (male.score == 101)
    cout << "Absent" << endl;
  else
    cout << male.name << " " << male.id << endl;
  if (female.score == -1 '' male.score == 101)
    cout << "NA" << endl;
  else
    cout << female.score - male.score;
  return 0;
}
```
