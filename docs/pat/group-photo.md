# Group Photo
题目链接[1109 Group Photo (25 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805360043343872)
## 题干大意

给定人数，排数，给这些人按身高排队，后一排人身高不低于前一排，每一排身高，身高相同则按名字排序按照中间最高，然后右边，再左边这样子，看英文描述，很容易懂。

## 思路

先给这些人排序，身高从高到低，名字从小到大，然后按每一排划分组，进行排队。

## 问题

注意最后一排人数，按照N - N / K * (N / K - 1)有问题，因为如5/6会当成0，所以要用求余运算更佳。

# AC代码(待优化)
```cpp
    #include <iostream>
    #include <utility>
    #include <vector>
    #include <string>
    #include <algorithm>
    using namespace std;

    struct Student {
        int height;
        string name;
    };
    bool cmp(Student s1, Student s2)
    {
        if (s1.height == s2.height)
            return s1.name < s2.name;
        return s1.height > s2.height ;
    }

    int main()
    {
        int K, N;
        cin >> K >> N;
        vector<Student> stu(K);
    //    for (int i = 0; i < K; ++i)
    //    {
    //        int height; string name;
    //        cin >> name >> height;
    //        stu.push_back(Student{height, name});
    //    }
        for (auto it = stu.begin(); it != stu.end(); ++it)
            cin >> it->name >> it->height;
        sort(stu.begin(), stu.end(), cmp);

        vector<vector<string>> rows(N);
        for (int i = 1; i < N; ++i)
            rows[i].resize(K / N);
        rows[0].resize(K / N + K % N); // 取余 note！！！

        int num = 0;
        for (int i = 0; i < rows.size(); ++i) {
            int p = num, m = rows[i].size();
            num += m;
            int start = m / 2;
            bool direction = true;
            rows[i][start] = stu[p].name;
            for (int j = 1; (p + j) < num; ++j) {
                if (direction) {
                    start -= j;
                    direction = false;
                }
                else {
                    start += j;
                    direction = true;
                }
                rows[i][start] = stu[p + j].name;
            }
        }

        for (int i = 0; i < rows.size(); ++i) {
            for (int j = 0; j < rows[i].size(); ++j)
            {
                cout << rows[i][j];
                if (j != rows[i].size() - 1)
                    cout << " ";
            }
            if (i != rows.size() - 1)
                cout << endl;
        }
        return 0;
    }
```    
