# 競技プログラミング C++ 備忘録

# 入出力
## 高速な実装
```cpp
ios::sync_with_stdio(false);
cin.tie(nullptr);
```
これで、入出力が高速になる(特に入出力の回数が多いとき、効果的)

# 数値計算
## べき乗
```cpp
pow(base,exponent)
```
- baseのexponent乗(cmathファイルをインクルードしておく)。double型による誤差に注意。

# 文字列
## 開始位置から取り出す長さだけの文字数を切り取る
```cpp
sub = S.substr(i, j)
```
- subは文字列Sのi文字目からj文字を取り出した文字列
## 文字列から特定の文字Aを取り除ける
```cpp
S.erase(remove(S.begin(), S.end(), A), S.end())
```
- Sから特定の文字Aが取り除かれる

# 型
## 型の宣言
```cpp
using lli = long long int
```
- lliで、long long intを宣言できるようにする(ほかの型であるdouble,string,vector,mapなどにも有効)
## 型変換
### 数字→数値
```cpp
number = numberS - '0' //(1)
numberS = to_string(number) //(2)
=stoi(numberS) //(3)
=stoll(numberS) //(4)
=stod(numberS) //(5)
```
上から順に、
- (1)数**字**から数**値**へ
- (2)数値から文字列(数字)へ
- (3)数字からint型数値へ
- (4)数字からlong long int型数値へ
- (5)数字からdouble型数値へ

# (一次元)配列
## 配列のソート
```cpp
vector<int> array;
sort(array.begin() + i,array.begin() + n + 1); //(1)昇順ソート
sort(array.rbegin() + i,array.rbegin() + n + 1); //(2)降順ソート
```
- (1)i番目からn番目までの要素を小さい順に並び変え
- (2)i番目からn番目までの要素を大きい順に並び変え
## 順列全探索
```cpp
do {処理} while (next_permutation(配列変数名.begin(),配列変数名.end()))
```
配列の順列を全探索。**ソート済みの配列に対して使うようにする。事前に配列をソートしておく**
## 要素の追加
(配列名).push_back()で配列の後ろに、新しく値を追加することができる

# 多次元配列
## 多次元配列の宣言
- `vector<vector<要素の型>> 変数名(要素数1, vector<要素の型>(要素数2, 初期値))`で宣言できる
- 初期値は省略可能
- `(変数名).size()`で縦の大きさを取得できる
- `(変数名)[0].size()`で横の大きさを取得できる

- `*max_element(a + 1,a + (要素数))`で配列の最大値を求められる(minでも同様)
- `変数名 = lower_bound(配列名 + 1,配列名 + 要素数 + 1,x) - 配列名`で配列名[i] >= xを満たす最小の整数iを変数に記録

# Pair型
## pair型変数
- `pair<型1,型2> (変数名p) = {変数1,変数2}`で宣言
- `p.first` は、変数1を指し、`p.second`は変数2を指す
- `p = make_pair(変数1,変数2)`という宣言の方法もあるが、今はこれでなくても先ほどのやつで大丈夫。

<br>

## pair型配列
- `vector<pair<型1,型2>> (配列名p) = {{変数1-1,変数1-2},{変数2-1,変数2-2},...}`でpair型配列を宣言
- `p[i].first,p[i].second`などで、pのi-1番目の要素にアクセス
- `p.push_back(make_pair(変数a,変数b))`で、新しく変数aと変数bのpairを配列pに追加

# map(連想配列)
キーとヴァリューを関連付けて管理する方法
- `map<キーの型1,値の型2> (連想配列名memo)`で連想配列memoを宣言
- `memo[キー] = (値)`で要素を追加or更新

# STLの関数
- `min(a,b)` 最小値
- `max(a,b)` 最大値
- `swap(a,b)` 交換
- `sort(vec.begin(), vec.end())` 小さい順に並び替え
- `reverse(vec.begin(),vec.end())` 並びを逆にする
