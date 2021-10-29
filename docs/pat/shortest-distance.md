# Shortest Distance
## 题干大意

在一个loop中，找两点的最短距离

## 思路

在输入时，就计算出所有距离的和`sum`，由于本题目点个数最大为$10^5$，查询的组数最大为$10^4$量级，所以按照来一组查一次的方式很容易超时，所以在输入时就**按顺时针方向的针对一个基点的距离`distance`**，以空间换时间，就很nice

## 问题

太久没用c了，一只用c++，都忘记`scanf`中是要写变量地址的😅，真尴尬，**更新用c++写**

## AC代码

```cpp linenums='1'
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main()
{
    int N;
    cin >> N;
    vector<int> D(N), distance;
    //distance[i]表示从下标为0到下标为i的点之间的距离
    distance.push_back(0);
    int sum = 0;
    for(auto i = 0; i != N; ++i){
        cin >> D[i];
        if(i)
            distance.push_back(sum);
        sum += D[i];
    }
    int M, a, b;
    cin >> M;
    while(M--){
        cin >> a >> b;
        if(a > b)
            swap(a, b);
        //序号变为下标
        auto temp = distance[b - 1] - distance[a - 1];
        cout << min(temp, sum - temp) << endl;
    }
    return 0;
}
```

