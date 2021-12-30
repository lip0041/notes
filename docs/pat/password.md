# Password
题目链接：[1035 Password (20 point(s))](https://pintia.cn/problem-sets/994805342720868352/problems/994805454989803520)

## 题干大意

按照规则：`1->@, 0->%, l->L, O->o`修改密码

## 思路

设置标志，表示是否有修改，修改后的存储在另一个`vector`中

## AC代码
```cpp
    #include <iostream>
    #include <vector>
    using namespace std;

    struct User {
        string name;
        string passwd;
        User(string s1, string s2) : name(s1), passwd(s2) {}
    };

    bool scan(User& user) {
        bool modified = false;
        for (auto &s : user.passwd) {
            switch (s) {
                case 'l':
                    s = 'L'; modified = true; break;
                case '0':
                    s = '%'; modified = true; break;
                case '1':
                    s = '@'; modified = true; break;
                case 'O':
                    s = 'o'; modified = true; break;
                default:
                    break;
            }
        }
        return modified;
    }

    int main() {
        int n; cin >> n;
        vector<User> users;
        while (n--) {
            string t_name, t_passwd;
            cin >> t_name >> t_passwd;
            users.emplace_back(t_name, t_passwd);
        }
        vector<User> ans;
        for (auto& user : users) {
            if (scan(user)) {
                ans.emplace_back(user);
            }
        }
        if (ans.size() == 0) {
            cout << "There " << (users.size() > 1 ? "are " : "is ") << users.size() << " account"
                << (users.size() > 1 ? "s " : " ") << "and no account is modified";
        }
        else {
            cout << ans.size() << endl;
            for (auto& u : ans) {
                cout << u.name << " " << u.passwd;
                if (&u != &ans.back())
                    cout << endl;
            }
        }
        return 0;
    }
```
