# Product of Polynomials
题目链接[1009 Product of Polynomials (25 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805509540921344)
## 题干大意

多项式乘法实现，常规

## 思路

一个向量存第一个多项式，后面一个多项式边读边计算即可

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    #include <iomanip>
    using namespace std;

    void calc(vector<double> &res, const vector<int> &index, const vector<double> &value, const int a, const double b)
    {
        for(auto it = index.begin(); it != index.end(); ++it)
            res[a + *it] += b * value[it - index.begin()];
    }

    int main()
    {
        int k, a;
        double b;

        vector<int> index;
        vector<double> value, res(2001);

        cin >> k;
        for(auto i = 0; i < k; ++i)
        {
            cin >> a >> b;
            index.push_back(a);
            value.push_back(b);
        }

        cin >> k;
        for(auto i = 0; i < k; ++i)
        {
            cin >> a >> b;
            calc(res, index, value, a, b);
        }

        int count = 0;
        for(auto &p : res)
            if(p != 0.0)
                ++count;
        cout << count;
        for(auto it = res.end() - 1; it >= res.begin(); --it)
            if(*it != 0.0)
                cout << " " << it - res.begin() << " " << setiosflags(ios::fixed) << setprecision(1) << *it;
        return 0;
    }
```
