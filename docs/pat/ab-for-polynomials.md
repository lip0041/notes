# A+B for Polynomials
题目链接[1002 A+B for Polynomials (25 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805526272000000)

## 题干大意

计算多项式的加法，要求输出项数以及各项的指数、系数

## 思路

不难，我利用了归并的思想去做，外加全部使用`c++`的方式编写，需要注意的几个点

1.  相加系数为0的项不能输出
2.  归并(假)，若A和B都遍历完了也要输出结果，这个我最初忘记了
3.  cout的格式化输出结果，要确保输出的系数保留一位小数

输出n位小数的控制代码：

    #include <iomanip>//需要的头文件
    using namespace std;
    
    cout << setiosflags(ios::fixed) << setprecision(n);
    //后面cout输出的数就保留了n位小数

## AC代码

```cpp linenums='1'
#include <iostream>
#include <vector>
#include <iomanip>
using namespace std;

//根据输入的项数，接受输入
void input(vector<int> &index, vector<double> &value, const int k)
{
  int a;
  double b;
  for(auto i = 0; i < k; ++i)
  {
    cin >> a >> b;
    index.push_back(a);
    value.push_back(b);
  }
}
int main()
{
  int k1, k2;
  vector<int> a_index, b_index;
  vector<double> a_value, b_value;
  cin >> k1;
  input(a_index, a_value, k1);
  cin >> k2;
  input(b_index, b_value, k2);

  vector<int> index;
  vector<double> value;
  //A和B的迭代器，设在for外，后续要用到
  auto it1 = a_index.begin(), it2 = b_index.begin();
  for(; it1 != a_index.end() && it2 != b_index.end();) {
    //选取指数大的存入结果向量index和value中
    if (*it1 > *it2) {
      index.push_back(*it1);
      value.push_back(a_value[it1 - a_index.begin()]);
      ++it1;
    } else if (*it1 < *it2) {
      index.push_back(*it2);
      value.push_back(b_value[it2 - b_index.begin()]);
      ++it2;
    } else {
      // 相等时还要判断和是否为0，若为0则不加入结果向量中
      if(a_value[it1 - a_index.begin()] + b_value[it2 - b_index.begin()]){
        index.push_back(*it1);
        value.push_back(a_value[it1 - a_index.begin()] + b_value[it2 - b_index.begin()]);
      }
      ++it1;
      ++it2;
    }
  }
  // 退出for循环的3种情况，都要考虑到
  // cout输出n位小数方法，先设置fixed在设置精度
  if(it1 != a_index.end())
  {
    cout << index.size() + a_index.end() - it1;
    for(auto it = index.begin(); it != index.end(); ++it)
      cout << " " << *it << " " << setiosflags(ios::fixed) << setprecision(1) << value[it - index.begin()];
    for(; it1 != a_index.end(); ++it1)
      cout << " " << *it1 << " " << setiosflags(ios::fixed) << setprecision(1) << a_value[it1 - a_index.begin()];
  }
  else if(it2 != b_index.end())
  {
    cout << index.size() + b_index.end() - it2;
    for(auto it = index.begin(); it != index.end(); ++it)
      cout << " " << *it << " " << setiosflags(ios::fixed) << setprecision(1) << value[it - index.begin()];
    for(; it2 != b_index.end(); ++it2)
      cout << " " << *it2 << " " << setiosflags(ios::fixed) << setprecision(1) << b_value[it2 - b_index.begin()];
  }
  else {
    cout << index.size();
    for(auto it = index.begin(); it != index.end(); ++it)
      cout << " " << *it << " " << setiosflags(ios::fixed) << setprecision(1) << value[it - index.begin()];
  }
  return 0;
}
```
