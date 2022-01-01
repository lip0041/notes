# Waiting in Line
题目链接[1014 Waiting in Line (30 分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805498207911936)
## 题干大意

排序调度

## 思路

按时间一步步模拟顾客被服务的过程

## 问题

只使用`vector`过了测试点4、5没过，不知道怎么解决，后续尝试使用`queue`解决。

## `vector`代码
```cpp linenums="1"
#include <iostream>
#include <vector>
using namespace std;

class customer {
  public:
  int time; // 需要服务的时间
  int done; // 服务结束时间
  int serve; // 服务开始时间
};

bool empty(vector<vector<int>> &windows) {
  bool flag = true;
  for (auto & window : windows) {
    if (!window.empty()) {
      flag = false;
      break;
    }
  }
  return flag;
}

bool quick(vector<vector<int>> &windows, vector<customer> &customers) {
  bool flag = true;
  for (auto & window : windows) {
    if (window.empty())
      continue;
    auto ip = window.begin();
    if (customers[*ip].done == 0) {
      flag = false;
      break;
    }
  }
  return flag;
}

int find_min(vector<vector<int>> &windows, vector<customer> &customers) {
  int min = 99999; // 初值问题
  for (auto & window : windows) {
    if (!window.empty() && min > customers[*window.begin()].time)
      min = customers[*window.begin()].time;
  }
  return min;
}

void serve(vector<vector<int>> &windows, vector<customer> &customers, int M) {
  int now = 0;
  int id = 0;
  for (int i = 0; i < M; ++i) {
    for (auto it = windows.begin(); it != windows.end() && id < customers.size(); ++it) {
      if (i == 0)
        customers[id].serve = 0;
      it->push_back(id++);
    }
  }
  while (now <= 540 && !empty(windows)) {
    int min = find_min(windows, customers);
    now += min;
    for (auto & window : windows) {
      if (!window.empty()) {
        auto ip = window.begin();
        if (customers[*ip].done == 0)
          customers[*ip].time -= min;
        if (customers[*ip].time == 0) {
          if (customers[*ip].done == 0)
            customers[*ip].done = now;
          window.erase(ip);
          if (!window.empty()) // 若不空，则下一个就是服务对象
            customers[*window.begin()].serve = now;
        }
      }
    }
    // 如果还有顾客等待则检查空余地方插入顾客
    if (id < customers.size()) {
      for (int i = 1; i <= M; ++i) {
        for (auto & window : windows) {
          while (window.size() < i && id < customers.size()) { // 队列是否有位置
            if (window.empty()) { // 队列为空, 则肯定会被服务
              if (customers[id].time + now >= 540) {
                customers[id].done = customers[id].time + now;
              }
              customers[*window.begin()].serve = now;
            } else {
              if (customers[id].time + now + customers[window.front()].time >= 540) {
                customers[id].done = customers[id].time + now + customers[window.front()].time;
              }
            }
            window.push_back(id++);
          }
        }
      }

    }
    if (quick(windows, customers))
      break;
  }
}

int main() {
  int N, M, K, Q;
  cin >> N >> M >> K >> Q;
  vector<vector<int>> windows(N);
  vector<customer> customers(K);
  for (auto & customer : customers) {
    cin >> customer.time;
    customer.done = 0;
    customer.serve = 541;
  }
  vector<int> queries(Q);
  for (int & query : queries) {
    cin >> query;
  }
  serve(windows, customers, M);
  auto it = customers.begin();
  for (auto i = 0; i < Q; ++i) {
    if((it + queries[i] - 1)->done > 540) {
      if ((it + queries[i] - 1)->serve < 540) {
        int hour = (it + queries[i] -1)->done / 60 + 8;
        int minute = (it + queries[i] - 1)->done % 60;
        if (hour > 17) {
          cout << "Sorry" << endl;
          continue;
        }
        hour >= 10 ? (cout << hour << ":") : (cout << 0 << hour << ":");
        minute >= 10 ? (cout << minute << endl) : (cout << 0 << minute << endl);
      }
      else
        cout << "Sorry" << endl;
    }
    else {
      int hour = (it + queries[i] -1)->done / 60 + 8;
      int minute = (it + queries[i] - 1)->done % 60;
      hour >= 10 ? (cout << hour << ":") : (cout << 0 << hour << ":");
      minute >= 10 ? (cout << minute << endl) : (cout << 0 << minute << endl);
    }
  }
  return 0;
}
```
