---
title: "競技プログラミング C++よく使う(気がする)構文 備忘録"
emoji: "🙆"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["C++", "初心者", "競技プログラミング", "AtCoder", "備忘録", "Idea"]
published: false
---

自分用の備忘録です。
競技プログラミング（AtCoder等）で「あれ何だっけ？」となった時にネット検索を挟まずすぐ解決したいと思い作成しました。APG4bの内容を参考とさせていただきました。

# 最初に書くテンプレ
```cpp
#include <iostream>   
#include <vector>    
#include <string>    
#include <algorithm>
#include <utility> 
#include <map>
#include <stack>
#include <queue>
#include <set>
#include <cmath>
#include <iomanip>

#define rep(i, n) for (int i = 0; i < (int)(n); i++)

using namespace std;

using ll = long long;

using vi = vector<int>;
using vvi = vector<vector<int>>;
using vll = vector<ll>; 
using vvll = vector<vector<ll>>;
using vb = vector<bool>;
using vvb = vector<vector<bool>>;
using vs = vector<string>;

using pii = pair<int, int>;
using pis = pair<int, string>;
using pll = pair<ll, ll>;
using pls = pair<ll, string>;
using mii = map<int, int>;
using mll = map<ll, ll>;
using msi = map<string, int>;

void solve() {
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    
    solve();
    return 0;
}
```
これを大会の最初に貼り付ける
(のちの議論は、すべてこれが張り付けてある前提で行う)

# 入出力
## 高速な実装
```cpp
ios::sync_with_stdio(false);
cin.tie(nullptr);
```
これで、入出力が高速になる(特に入出力の回数が多いとき、効果的)

# 数値計算
## べき乗
`pow(base,exponent)` baseのexponent乗(cmathファイルをインクルードしておく)。double型による誤差に注意。
## 10のn乗
`10en` 10のn乗の数
## ビットの計算
`1 << N`によって、1のビットをN右にずらす。すなわち、2のN乗を表す。

# 論理演算
## ビット演算
```cpp
if (num >> i & 1) {
    // 処理;
}
```
numの(下から数えて)i番目のビットが1ならば、処理を実行する

# 文字列
## 小文字から大文字への変換
```cpp
#include <iostream>
#include <cctype> // ファイルのインクルードに注意
using namespace std;

int main() {
    char lower = 'a';
    // toupperはintを返すので、charでキャスト（型変換）するのが一般的です
    char upper = (char)std::toupper(lower);

    std::cout << upper << std::endl; // 'A' が出力される
    return 0;
}
```
これにより、小文字を大文字にかえる。

## 開始位置から取り出す長さだけの文字数を切り取る
`sub = S.substr(i, j)` subは文字列Sのi文字目からj文字を取り出した文字列
## 文字列から特定の文字Aを取り除ける
`S.erase(remove(S.begin(), S.end(), A), S.end())` により、文字列Sから特定の文字Aが取り除かれる
## 文字列の最初と最後
`S.front()`と`S.back()`によって、文字列の最初の文字と最後の文字にアクセスできる

# 型
## 型の宣言
`using ll = long long int` llで、long long intを宣言できるようにする(ほかの型であるdouble,string,vector,mapなどにも有効) <br>
↑長い型名も短縮できて楽。型名にあだ名をつけている気分。

## 型変換
### 数字→数値
`number = numberS - '0'` 数**字**から数**値**へ
`numberS = to_string(number)` 数値から文字列(数字)へ
`stoi(numberS)` 数字からint型数値へ
`stoll(numberS)` 数字からlong long int型数値へ
`stod(numberS)` 数字からdouble型数値へ

# (一次元)配列
## 配列のソート
`sort(vec.begin() + i,vec.begin() + n + 1)` で、配列vecのi番目からn番目までの要素を小さい順に並び変え
`sort(vec.rbegin() + i,vec.rbegin() + n + 1)` で、配列vecのi番目からn番目までの要素を大きい順に並び変え

## 順列全探索
`do {処理} while (next_permutation(vec.begin(),vec.end()))`配列vecの順列を全探索。**ソート済みの配列に対して使うようにする。事前に配列をソートしておく**
## 要素の追加
`vec.push_back()`で配列vecの後ろに、新しく値を追加することができる

## 最大値の導出
`*max_element(a.begin(),a.end())`で配列aの最大値(minでも同様)
`*max_element(a.begin() + i,a.begin + (j + 1))`で配列aの、i番目からj番目の最大値(minでも同様)

## 要素の削除
```cpp
vector<int> v = {1, 2, 3, 4, 5};

v.erase(v.begin() + i);
```
i 番目（0-indexed）を削除
```cpp
vector<int> v = {1, 2, 3, 2, 4};

v.erase(remove(v.begin(), v.end(), 2), v.end());
```
これによって特定の要素を削除(上のようだと、2が消える)
```cpp
v.erase(
    remove_if(v.begin(), v.end(), [](int x) {
        return x % 2 == 0; // ここに条件式を記述
    }),
    v.end()
);
```
配列vの要素xが偶数だった場合、それを削除(条件式を指定すればどういう消し方もでき、便利)

# lower_bound
```cpp
auto itr = lower_bound(vec.begin(), vec.end(), x);
int i = distance(vec.begin(), itr);
```
でvec[i] >= xを満たす最小の整数iを求めることができる。(0-indexedで)<br>
なお、`int i = itr - vec.begin()`としても可<br>
※**`lower_bound(vec.begin() ,vec.end() ,x)`は、イテレータであることに注意**。数字を記録するだけであり、数字そのものではない。

# 多次元配列
## 多次元配列の宣言
- `vector<vector<要素の型>> 変数名(要素数1, vector<要素の型>(要素数2, 初期値))`で宣言できる
- 初期値は省略可能
- `変数名.size()`で縦の大きさを取得できる
- `変数名[0].size()`で横の大きさを取得できる

# set(値を重複なく管理可能)
## setの宣言
```cpp
set<int> num = {1,2,3,3}; //(1)
set<char> s = {a,b,c,d,c,e}; //(2)
```
このように宣言し、numやsの要素をcoutですべて出力すると、
```txt
1 2 3 // (1)
a b c d e // (2)
```
となる
## setへの要素の追加
```cpp
num.insert(200);
num.insert(3);
```
このような文で、coutを用いて要素を追加すると、
```txt
1 2 3 200
```
のように、存在していない200が追加される。
また、すでにnumに存在している3の数は増えない。
## setの要素の削除
```cpp 
num.erase(1)
```
を書き、coutを用いて出力すると、
```txt
2 3 200
```
と出力され、1が消されている。
## setの最小値
```cpp
min_num = *num.begin(); // num.begin()はイテレータ
cout << num;
```
とかくと、出力は
```txt
2
```
となる。また、setの下からn番目の要素にアクセスするときは、num.begin()に(n-1)を足す。
## x以上の最小値
例えば、前述のnumで4以上の値で最小値を出力するとき、
```cpp
cout << *num.lower_bound(4) << "\n"; // num.lower_bound()自体はイテレータ
```
と書く。出力結果は、
```txt
200
```
となる。

# Pair型
## pair型変数
- `pair<型1,型2> 変数名p = {変数1,変数2}`で宣言
- `p.first` は、変数1を指し、`p.second`は変数2を指す
- `p = make_pair(変数1,変数2)`という宣言の方法もあるが、今はこれでなくても先ほどのやつで大丈夫。

## pair型配列
- `vector<pair<型1,型2>> p = {{変数1-1,変数1-2},{変数2-1,変数2-2},...}`でpair型配列pを宣言
- `p[i].first,p[i].second`などで、pのi-1番目の要素にアクセス
- `p.push_back(make_pair(a,b))`で、新しく変数aと変数bのpairを配列pに追加

# stack
順に要素を入れていき、最後に入れたものだけを操作できるデータ構造。
```cpp
stack<string> name; // stack型の変数nameを宣言

name.push("enaga"); // nameの一番上に"enaga"という要素を追加
name.push("hiyoko"); // nameの一番上に"hiyoko"という要素を追加

A = name.top(); // nameの一番上にアクセス
cout << A << "\n";

name.pop(); // nameの一番上を削除
cout << name.top() << "\n";
```
以上を実行すると、
```txt
hiyoko
enaga
```
と出力される

# map(連想配列)
キーとヴァリューを関連付けて管理する方法
- `map<キーの型1,値の型2> memo`で連想配列memoを宣言
- `memo[キー] = (値)`で要素を追加or更新

# STLの関数
- `min(a,b)` 最小値
- `max(a,b)` 最大値
- `swap(a,b)` 交換
- `sort(vec.begin(), vec.end())` 小さい順に並び替え
- `reverse(vec.begin(),vec.end())` 並びを逆にする

<br>
参考：[APG4b](https://atcoder.jp/contests/APG4b)
