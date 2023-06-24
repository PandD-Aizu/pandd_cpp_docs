---
layout: default
---

# 企画開発部 プログラミング勉強会第三回


## 目次

- [配列](#配列)
- [std::vector](#std::vector)
- [std::string](#std::string)
- [関数](#関数)
- [スコープ](#スコープ)

## イントロ

今回はまず、複数のデータをまとめて扱うことができる「配列」を紹介します。

`C`や`C++`では配列の一般的な仕様として、`int A[4]`みたいに変数名の後ろに`[]`をつけて中に要素数を指定するものがあります。
- prog0で確実に習うと思うのでそちらに任せます

今回の勉強会ではそれを**扱わず**`C++`の標準ライブラリのひとつ`std::vector`(可変長配列)で同等の処理の方法を学んでいただきます。
- こうする理由は、`Siv3D`で配列として提供されている`s3d::Array`が`std::vector`と使い方が似ているためです。

また、文字列を扱う「`std::string`」も紹介します。`std::vector`とほぼ使い方が同じです。

次に今回の目玉、「関数」を扱います。

関数では、重複する処理等を`main`関数から分割して扱うことができます。
- ロジックを上手く分割して、関数に分けて記述することはプログラミングの醍醐味の一つであり、楽しく感じる人も多いでしょう

関数は大事な概念なので、 $2$ 回に分けて勉強会を行います。今回はその前半として、スコープを扱います。

スコープとは、簡単に言えば「変数の生きていられる範囲」です

`if`、文や`for`文、関数が存在するプログラムを書いたり読んだりするためにはスコープの理解が必須です。

今回も盛りだくさんですが、気張っていきましょう！


## 配列

唐突に質問ですが、「Excel」をご存知ですか？「Excel」は表計算ソフトの一つですね。

Excelを開くと表がずらーっとでてきて、そこに数やテキストを入れることができます。
- 行番号と列番号 $(i, j)$ に対してデータを一つ割り当てるわけですね。

`C`や`C++`でも似たようなことができたら嬉しいですよね。

例えば、あなたが学校の先生で、生徒のテストの点数を管理することを考えます。
- 平均点、中央値を出したり
- 各生徒毎に偏差値を割り出したりしたいです

そのような時に第一回、第二回勉強会で習った概念のみでプログラムを書こうとするとこうなります。

```cpp
#include <iostream>

int main() {
    int p1 = 50, p2 = 80, p3 = 78, p4 = 32, p5 = 100, p6 = 68, p7 = 26;
    double ave = (p1 + p2 + p3 + p4 + p5 + p6 + p7) / 7;
    ...
}
```

正直平均点だけでもかなり厳しいですね。中央値を求めようとすると、 $7$ 要素を昇順に並び替える必要があるので、それはそれはもうすごい`if`文祭りになっていしまいます。

しかも実際は、生徒は $30$ 人くらいいます。絶望....

しかし、`C`、`C++`を含む多くのプログラミング言語では、このような複数のデータを扱う方法の一つに「配列」を提供しています。

`C++`ではメジャーなものに $4$ 種類の配列があります。

- 生配列(いわゆる「普通の配列」)
- `std::array` (固定長配列)
- `std::vector` (可変長配列)
- `std::unique_ptr<T[]>` (自分が馴染み無いので説明は避けます)

今回は $3$ 番目の`std::vector`を重点的に説明します。

## std::vector

```cpp
#include <iostream>
#include <vector> // std::vectorを利用するにはこのヘッダをインクルードする必要がある

int main() {
    std::vector<int> A = { 1, 4, 5, 6, 2 };
    std::cout << A[0] << std::endl; // 1番目の要素「1」が出力される
    std::cout << A[2] << std::endl; // 3番目の要素「5」が出力される
    std::cout << A.size() << std::endl; // Aの要素数「5」が出力される
    std::cout << A.back() << std::endl; // Aの最後の要素「2」が出力される
    A[1] += 3; // Aの2番目の要素に3を足す
    std::cout << A[1] << std::endl; // 7が出力される
    return 0;
}
```

例えば、上のサンプルコードの例だと $(1, 4, 5, 6, 2)$ という整数の列を`std::vector`で扱っています。
- 各要素を出力したり、要素数を出力したり、要素に値を加算したりしていますね。

`std::vector`を扱うには色々ポイントがあります。ひとつひとつ見ていきましょう
- すべてを覚える必要はありません。必要に応じて調べながら使ってみてください
- リファレンスの日本語訳は[こちら](https://cpprefjp.github.io/reference/vector/vector.html)です

```cpp
#include <vector>
```

標準入出力を行うのに`#include <iostream>`をしたのと同様に、`vector`というヘッダをインクルードする必要があります。

```cpp
std::vector<int> A = { 1, 4, 5, 6, 2 };
```
`std::vector<扱いたい型> 変数名 = { 列の要素をカンマ区切り }`とすることで`std::vector`を宣言、初期化することができます。

他にも様々な初期化(第4回の内容になりますが、正しく言うとコンストラクタ)があります。
- 扱いたい型を`int`にした場合で例示しておきます。

| 書き方 | 内容 |
| :---: | :---: |
| A | 空列で初期化する |
| A(5) | 長さ $5$ の各要素が $0$ の列 |
| A(3, 1) | 長さ $3$ の各要素が $1$ の列 |
| A = { 1, 2, 3, 4, 5 } | 列(1, 2, 3, 4, 5) |
| A(B) | (Bという`std::vector<int>`がある状態で)Bのコピー |
| A = B | (Bという`std::vector<int>`がある状態で)Bのコピー |

```cpp
A[0]
```

各要素にアクセスするには、`変数名[番号]`とします。
- この番号を添字と言ったりします
- 添字は、 $0$ からスタートすることに注意してください

ここで、列の範囲外の添字を指定したりするとプログラムがどのような動作をするかわかりません
- 実行時エラーを吐いたり、吐かなかったりします。

```cpp
A.size()
```

変数名`.size()`とすることで、列の要素数を取得することができます。

この`.OOO()`をメンバ関数と呼びます。詳しくは次回やります。`std::vector`のメンバ関数をいくつか紹介しておきます。

| 呼び出し方 | できること | ()の中に入れるもの | 注釈 |
| :---: | :---: | :---: | :---: |
| .size() | 要素数を取得する | 何も入れない | 要素数を扱う型はint型では無く`std::size_t`型 |
| .front() | 一番最初の要素を取得する | 何も入れない | A[0]と同じ |
| .back() | 一番最後の要素を取得する | 何も入れない | A[A.size() - 1]と同じ |
| .push_back(value) | `value`を末尾に挿入する | 挿入したい要素 | .push_front()は存在しない |
| .at(i) | (i + 1)番目の要素を取得する | 取得したい要素の番号 | 範囲外アクセスをすると例外を出す(大雑把に言うと、エラーにしてくれる) |
| .clear() | 全要素を削除する | 何も入れない | 呼び出し後、空になる |
| .begin() | 最初のイテレータを返す | 何も入れない | イテレータの話は今回は時間が無くて扱えない... |

ちょっと練習

1. 要素数が $10$ でどの要素も $2$ である`std::vector<int>`を作ってみましょう
2. 1で作った`std::vector`に`push_back()`を使って、末尾に $3$ を挿入してみましょう。
3. 2までやった上で、`back()`を使って末尾の要素を出力してみましょう。
4. `clear()`で列を空列にしましょう
5. `size()`を出力して、要素数が $0$ になっていることを確認しましょう

#### 列とfor文は相性が良い

```
#include <iostream>
#include <vector>

int main() {
    vector<int> A = { 1, 2, 3, 4, 5 };
    for (int i = 0 ; i < (int)A.size() ; i++) {
        std::cout << A[i] << ' ';
    }
    std::cout << std::endl;
    return 0;
}
```

このように、列を前から、あるいは後ろから舐めるのには`for`ループが有効です。

一般に $n$ 回同じ処理をしたい時は`for (int i = 0 ; i < n ; i++) {}`としますが、このカウンタ変数が`std::vector`の添字アクセスに適しています。

```cpp
#include <iostream>
#include <vector>

int main() {
    int N;
    std::cin >> N;
    std::vector<int> A(N);
    for (int i = 0 ; i < N ; i++) {
        std::cin >> A[i];
    }
    return 0;
}
```

学校の授業や(興味のある人は)競技プログラミングでは良く「長さ $N$ の数列を入力で受け取る」という処理を課されることが多いです。
- 演習問題でもちらほらでるかも

こういう時は`for`文を使って上記の様に書くことができます。

#### range-based for

`C`には無くて`C++`にあるちょっと特殊な`for`文です。余力があったら覚えてください。

```cpp
#include <iostream>
#include <vector>

int main() {
    int N;
    std::cin >> N;
    std::vector<int> A(N);
    for (int& a : A) {
        std::cin >> a;
    }
    return 0;
}
```

`std::vector`等では`for (型 変数名 : 列名)`とすることで列の要素を前から順番に変数に入れることができます。
- `&`がついているのは次回説明します。今はおまじないだと思って良いです。入力の時は必要です。

他にも、すべての要素に $3$ を加算するみたいなプログラムだと

```cpp
for (int i = 0 ; i < (int)A.size() ; i++) {
    A[i] += 3;
}
```
が
```cpp
for (int& a : A) {
    a += 3;
}
```
と書けます。書く量が少なくて便利ですね。

#### std::vectorにstd::vectorを入れる。

`std::vector`の各要素に`std::vector`を持つことができます。

```cpp
#include <iostream>
using namespace std;

int main() {
    std::vector<std::vector<int>> A = { { 1, 2, 3 }, { 4, 5 }, { 6, 7, 8, 9 }, { 10 } };
    std::cout << A[0][1] << std::endl;
    std::cout << A[2][0] << std::endl;
    std::cout << A.size() << std::endl;
    std::cout << A[1].size() << std::endl;
    return 0;
}
```

クイズ！

1. A[3][0]の値は？
2. A[0].size()の値は？
3. A.front().back()の値は？
4. A[2][2]の値は？


`std::vector`の各要素に`std::vector<std::vector<...>>`を入れることもできます。どんどんややこしくなる....


## std::string

文字列を扱うことを考えます。第一回勉強会ぶりですね。

単一の文字を扱う型は`char`でした。つまり、`char`の列を考えることによって文字列を管理できそうです。

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<char> S = { 'P', 'a', 'n', 'd', 'D' };
    return 0;
}
```

しかし、文字列についてはもっとスマートなものがあります。それが`std::string`です。

```cpp
#include <iostream>
#include <string>

int main() {
    std::string S = "PandD";

    std::cout << S << std::endl;

    S += "Game dev Club!!";

    std::cout << S << std::endl;

    return 0;
}
```

`std::vector<char>`でできることはたいてい`std::string`でできます。更に
- 文字列リテラル(ダブルクォーテーションで囲った文字の並び)での初期化
- `+`での文字列の連結
- `std::cin`でターミナルから文字の並びを入力で受け取る

等ができます。べんり〜〜〜〜

#### ちょっと練習

1. 標準入力から文字列を受け取って、そのまま出力するプログラム(オウム返し)を作成してみましょう
2. `std::vector`や`std::string`で好きに遊んでみてください


## 関数

#### 先に例示

話題を大きくかえて、関数というものの話に移ります。

以下の問題を考えましょう。

「L以上R以下の素数を列挙してください」

これは前回の勉強会でちらっとやりましたね。前回は`while`文で書いたので今回は`for`文で書きます。

```cpp
#include <iostream>

int main() {
    int L, R;
    std::cin >> L >> R;
    for (int i = L ; i <= R ; i++) {
        int value = i;
        bool ok = true;
        for (int j = 2 ; j < value ; j++) {
            if (value % j == 0) {
                ok = false;
            }
        }
        if (ok) {
            std::cout << value << std::endl;
        } 
    }
    return 0;
}
```

LからR以下まで値を回すのを外側のループが、素数判定をループの内側で行っています。

こちらのコード、少し読みづらく感じませんか？というのも、プログラムが実際にどう動くのかを観察すると、ループが２つ入りこんでいて挙動を追うのが大変です。

ここで、関数を利用し、素数判定のパートをmain関数の外に追い出してしまいます。


```cpp
#include <iostream>

// @brief: valueが素数かを判定する関数
// @param value: 素数判定したい値
// @response: valueが素数ならtrue
bool isPrime(int value) {
    int value = i;
    bool ok = true;
    for (int j = 2 ; j < value ; j++) {
        if (value % j == 0) {
            ok = false;
        }
    }
    return ok;
}

int main() {
    int L, R;
    std::cin >> L >> R;
    for (int i = L ; i <= R ; i++) {
        if (isPrime(i)) {
            std::cout << i << std::endl;
        } 
    }
    return 0;
}
```
これは上のコードと同じ挙動をするプログラムです。

とりあえず今はmain関数がすっきりしたな程度のニュアンスを感じてもらえたら大丈夫です。


#### 関数とは

まず関数ってな〜〜〜〜にって話からしていきます。

関数は「0個以上の与えられた値を利用して特定の処理を行い何かしら値を返す(返さなくても良い)」というものです。

この意味ではmain関数も関数ですね。

数学の関数に思いを馳せてみましょう。たとえば $f(x) = x + 2$ というのは $x$ を受取って、 $x$ に $2$ を足したものを返していますね。
- これからの都合のため、 $x\in \mathbb{Z}$ とします。

これを `C++` の関数で書くと以下のようになります。

```cpp
int f(int x) {
    return x + 2;
}

int main() {
    std::cout << f(3) << std::endl; // 5が出力される
    return 0;
}
```

数学の $f(x)$ と比較しながら順番に説明します。

まず、 $f(x)$ の $x$ にあたる部分が `f(int x)` の `(int x)`の部分です。
- これを**引数**といいます。
- 引数は必ず(型 引数名) とします

次に `x + 2`を返しているのが

```cpp
return x + 2;
```

ここです。 

まず、 `int f(int x) {` の`int`の部分が返すデータの型 (値返却型) です。

返す値は `return `の後に続けて書きます。

関数で行う処理は `{}`の中に書きます。`main`関数での`return 0`と同様に、`return`文を読み込んだらその時点でその関数は値を返して実行を終了します。(呼び出し元に戻ります)

ここでいう呼び出し元は

```cpp
<< f(3) <<
```

ここです。この`f(3)`ですね。
- ここでは、 $x = 3$ として関数を呼び出しているので $3 + 2 = 5$ が帰ってきて、 $5$ が出力されます。

先程の素数判定のプログラムの`isPrime`関数を見てみましょう


```cpp
#include <iostream>

// @brief: valueが素数かを判定する関数
// @param value: 素数判定したい値
// @response: valueが素数ならtrue
bool isPrime(int value) {
    int value = i;
    bool ok = true;
    for (int j = 2 ; j < value ; j++) {
        if (value % j == 0) {
            ok = false;
        }
    }
    return ok;
}

int main() {
    int L, R;
    std::cin >> L >> R;
    for (int i = L ; i <= R ; i++) {
        if (isPrime(i)) {
            std::cout << i << std::endl;
        } 
    }
    return 0;
}
```

まず、引数が`int value`なので、整数を一つ受け取る関数であることがわかります。

次に `bool`が値返却型に設定されているので、真理値を結果として返す関数であることがわかります。

実際素数なら`true`そうでないなら`false`を返す関数となっています。


#### 関数名と関数を使うメリット

関数を使うメリットの一つに「コードを読みやすくする」というものがあります。

素数判定のプログラムについても、`main`関数の中身が読みやすいのでは無いでしょうか？
- `std::cout`される条件が「 $i$ が素数である時」と直感的にわかりやすいと思います。

このような恩恵が受けられるのも、関数名にその関数がする処理を端的に説明したようなものをつけているからです。関数名にはちょっと気を使ってみましょう！

#### 複数の引数を持つ関数

```cpp
#include <iostream>

int sum(int a, int b) {
    return a + b;
}

int main() {
    int a, b;
    std::cin >> a >> b;
    std::cout << sum(a, b) << std::endl;
    return 0;
}
```

数学の関数にも $2$ 変数関数などをはじめ多変数関数があるのと同様に、こちらの関数にも複数の引数をつけることができます。
- コンマ区切りで指定します。

#### 返り値を持たない関数

```cpp
#include <iostream>
#include <string>

void output(std::string S) {
    std::cout << S << std::endl;
}

int main() {
    output("PandD");
    output("Univ of Aizu");
    return 0;
}
```

特に値を返さない関数については値返却型に`void`を指定します。
- 第一回勉強会以来の登場です

`void`が値返却型に設定されているプログラムで`return`文を使いたい時は

```cpp
void isOdd(int a) {
    if (a % 2 == 0) {
        return;
    }
    std::cout << a << " is odd!!!" << std::endl;
}
```
のように`return`の後ろにセミコロンだけをつけるようにします。


## スコープ

#### 変数は生きている場所に限りがある。

```cpp
#include <iostream>

int sum(int a, int b) {
    return a + b;
}

int main() {
    int a, b;
    std::cin >> a >> b;
    std::cout << sum(a, b) << std::endl;
    return 0;
}
```

このプログラムでこのような疑問を抱いたかもしれません。

```cpp
int main() {
    int a, b;
    std::cin >> a >> b;
```
ここの`a, b`と
```cpp
int sum(int a, int b) {
    return a + b;
}
```
ここの`a, b`で変数名が被っているが、大丈夫なのかと。

実際
```cpp
int main() {
    int a = 10;
    int a = 20;
    return 0;
}
```

みたいにすると、コンパイルエラーが発生します。

しかし、今回の場合実際プログラムは正常に動作していてなんら問題は無いです。なぜなら、この`a, b`は違う存在だからです。

変数には生きていられる場所に限りがあります。それがスコープです。


```cpp
#include <iostream>

int main() {
    {
        int a = 10;
        std::cout << a << std::endl;
        // ここでaが死ぬ
    }
    {
        int a = 20;
        std::cout << a << std::endl;
        // ここでaが死ぬ
    }
    int a = 30;
    std::cout << a << std::endl;
    return 0;
}
```

基本的には変数で宣言された場所から、自身を含む{}の末尾までが変数は生きて、{}の外側に出ると死にます。

`a = 10`の`a`と`a = 20`の`a`と`a = 30`の`a`は名前が同じだけの全くの別物です。

前回の勉強会で、

```cpp
#include <iostream>

int main() {
    for (int i = 0 ; i < 5 ; i++) {
        // 省略
    }
    std::cout << i << std::endl;
    return 0;
}
```
がエラーになるという話をしました。これもスコープが関係していて、

```cpp
for (int i = 0 ; i < 5 ; i++) {
    // 省略
} // iはここの中でしか生きられない
```

この`for`ブロックの中でしか生きられないからです。これを解決するには

```cpp
#include <iostream>

int main() {
    int i;
    for (i = 0 ; i < 5 ; i++) {
        // 省略
    }
    std::cout << i << std::endl;
    return 0;
}
```

としてあげれば良いです。(後で説明しますが)これはあまり行儀の良くないプログラムです...


#### 関数のスコープ

```cpp
#include <iostream>

int sum(int a, int b) {
    return a + b;
}

int main() {
    int a, b;
    std::cin >> a >> b;
    std::cout << sum(a, b) << std::endl;
    return 0;
}
```

先程もいいましたが、関数の呼び出し元の`a, b`と呼び出し先の関数内の`a b`も名前が同じだけの別物です。

しかし、この子は別物といってもクローンみたいなイメージで、値自体は同じですね。

```cpp
sum(1, 3)
```
としたら、関数内では`a`に`1`が、`b`に`3`が入っています。しかし、やはり別物なので

```cpp
#include <iostream>

int notSumButOne(int a, int b) {
    a = 0;
    b = 1;
    return a + b; 
}

int main() {
    int a = 3, b = 5;
    std::cout << notSumButOne(a, b) << std::endl;
    std::cout << a << std::endl;
    std::cout << b << std::endl;
    return 0;
}
```

ということをしても`main`関数内の`a, b`には`1`や`0`が代入されることはありません。なぜなら別者だから....
- 実はやる方法はあって、次回説明します
- 更に実はこのやる方法は今回の勉強回資料で登場しています(?!)

#### ちょっと練習

1. ３つの整数を受け取って、その総乗を返す関数を作ってみましょう
2. 一つの整数を受け取って、その整数が2の倍数であるかを判定する関数を作ってみましょう
3. `std::vector<int>`を受け取って、その総和を返す関数を作ってみましょう
