# Shuffling Machine
## 题干大意

对54张牌进行给定次数且给定序列的洗牌模拟。

## 思路

设一个`res`数组用来记录最终第i张牌在初始序列(S1~S13,...,D13,J1,J2)中的序号。对每个牌根据给定的`shuffleseq`进行给定`cnt`次套娃查找。最终结果根据初始序列的序号进行映射，不麻烦.

## 问题

不审题... `no extra space at the end of the line`这几行字被我吃了，太久没做题了。

## AC代码

```cpp linenums='1'
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int cnt;//循环次数
    //洗牌序列、最终结果res--res[i]中记录的是第i个牌在初始序列的顺序
    vector<int> shuffleSeq, res(55);
    shuffleSeq.push_back(-1);
    const char card[5] = {'S', 'H', 'C', 'D', 'J'};
    if(cin >> cnt, cnt){
        for(int n; cin >> n; shuffleSeq.push_back(n));
        int curP, truP = 1;
        for(int i = 1; i!= 55; ++i){
            curP = i;
            //循环cnt次
            for(int j = 0; j != cnt; ++j){
                truP = shuffleSeq[curP];
                curP = truP;
            }
            //第i个牌最终位置为truP
            res[truP] = i;
        }
    }
    //循环次数为0
    else
        for(auto it = res.begin() + 1; it != res.end(); ++it)
            *it = it - res.begin();
    for(auto it = res.begin() + 1; it != res.end(); ++it){
        //格式修正，如初始为第25个牌是(25-1)/13 = 1,H组的第(25-1)%13+1 = 12个，即H12
        cout << card[(*it - 1) / 13] << ((*it - 1) % 13 + 1);
        //最后末尾不输出空格
        if(it - res.begin() != 54)
            cout << ' ';
    }
    return 0;
}
```

