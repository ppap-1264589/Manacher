# [Trang chủ](https://ppap-1264589.github.io/interesting-solution)

## Bài Toán
[Longest Palindrome](https://cses.fi/problemset/task/1111)

# Hướng dẫn

Thực sự là cp-algorithms là một trang đã nói khá rõ về chủ đề này -> [Manacher's Algorithm](https://cp-algorithms.com/string/manacher.html)

Dưới đây là một cách cài đặt khả thi cho bài toán trên:

```c++
#include <bits/stdc++.h>
#define Task "A"
#define up(i,a,b) for (int i = a; i <= b; i++)
#define bit(x,i) ((x >> i) & 1)
using namespace std;

const int maxn = 1e6 + 10;
string s;
int d1[maxn];
int d2[maxn];
int pos = -1;
int maxx = -1;
int n;

void Manachers_Odd(){
    for (int l = 1, r = 0, i = 1; i <= n; i++){
        int k = (i > r) ? 1 : min(d1[l+r-i], r - i + 1);
        while (i-k >= 1 && i+k <= n && s[i-k] == s[i+k]) k++;

        d1[i] = k--;
        if (maxx < d1[i]*2-1){
            maxx = d1[i]*2-1;
            pos = i - d1[i] + 1;
        }
        if (i + k > r){
            r = i + k;
            l = i - k;
        }
    }
}

void Manachers_Even(){
    for (int l = 1, r = 0, i = 2; i <= n; i++){
        int k = (i > r) ? 0 : min(d2[l+r-i], r - i + 1);
        while (i-k-1 >= 1 && i+k <= n && s[i-k-1] == s[i+k]) k++;

        d2[i] = k--;
        if (maxx < d2[i]*2){
            maxx = d2[i]*2;
            pos = i - d2[i];
        }
        if (i + k > r){
            r = i + k;
            l = i - k;
        }
    }
}

signed main(){
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    if (fopen(Task".inp", "r")){
        freopen (Task".inp", "r", stdin);
        freopen (Task".out", "w", stdout);
    }

    cin >> s;
    n = s.size();

    s = '@' + s;
    Manachers_Odd();
    Manachers_Even();
    cout << s.substr(pos, maxx);
}
```
