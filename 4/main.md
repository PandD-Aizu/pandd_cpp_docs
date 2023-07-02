---
layout: default
---

# プログラマ勉強会第四回

## 目次

- [関数の復習](#関数の復習)
- [引数](#引数)
- [クラス](#クラス)

## イントロ

今回の勉強会では、実際に皆さんに関数を作ってもらうことによって、まずは関数の基礎を復習します。

次に、関数の引数の渡し方の種類について、
- 値渡し
- 参照渡し
- const参照渡し

の３つを学んでもらいます。簡単に使い分けができるくらいになってもらえると嬉しいです。

最後に、クラスについて学んでもらいます。ゲームプログラミングにおいて、クラスはキャラクター・オブジェクト・ゲームシステムなどの様々な実装で多用するので、ぜひ頑張って理解してください。

今回はクラスについてはイントロダクション程度に触れて、詳しい内容は次回(C++最終回)に渡します。


## 関数の復習

#### 基本のおさらい

まずはC++の腕試しに、次の問題を解いてみてください。関数などは意識しなくても大丈夫です。

$3$ 人の数学のテストの点数を標準入力で与えます。最高点を出力してください。
- 自身のない人は、以下のコード(2つあるので、片方)の穴埋め・バグ取りで解答してください

```cpp
#include <iostream>

int main() {
    int a, b, c;
    std::cin >> a >> b >> c;

    int ans = a;
    if () {
        ans = b;
    }
    if () {
        ans = c;
    }

    cout << ans << endl;

    return 0;
}
```

```cpp
#include <iostream>
#include <>

int main() {
    std::vector<int> Math(3); 
    std::cin >> Math[] >> Math[] >> Math[];

    int ans = Math[];
    if () {
        ans = Math[];
    }
    if () {
        ans = Math[];
    }

    cout << ans << endl;

    return 0;
}
```

解答はプロジェクターで公開します。次に、以下の問題を解いて見てください。

$3$ 人の数学と英語のテストの点数を標準入力で与えます。 それぞれ最高点を出力してください。



この時点で、同じ処理を $2$ 回書いたことになるでしょう。ここで、「３つの整数の最大値を返す」処理を関数化してみましょう。
- すでに関数を書いていた人はそれでOKです。ぐっっど


```cpp
#include <iostream>

int max(int a, int b, int ) {
    int res = a;
    if () {
        res = b;
    }
    if () {
        res = ;
    }

    return res; 
}

int main() {
    int a1, b1, c1;
    std::cin >> a1 >> b1 >> c1;
    
    std::cout << max() << std::endl;

    int a2, b2, c2;
    std::cin >> a2, b2, c2;
    
    cout << max() << endl;

    return 0;
}
```

```cpp
#include <iostream>
#include <>

int max(std::vector<int> A) {
    int res = A[0];
    for (int i = 0 ; i < (int)A.size() ; i++) {
        if (res < A[]) {
            res = A[];
        }
    }

    return res; 
}

int main() {
    std::vector<int> Math(3);
    cin >> Math[0] >> Math[1] >> Math[2];

    std::cout << max() << std::endl;

    std::vector<int> Eng(3);
    cin >> Eng[0] >> Eng[1] >> Eng[2];

    std::cout << max() << std::endl;

    return 0;
}
```

このように、あるひとまとまりの処理・複数回行う処理は積極的に関数化していきましょう。

#### ちょっと練習

1. 二次元平面上の座標を一つ与えます。原点からのユークリッド距離を計算する関数を作成して、計算結果を出力してください。
2. 二次元平面上の座標を一つ与えます。原点からのマンハッタン距離を計算する関数を作成して、計算結果を出力してください。

#### 関数で別の関数を呼び出す。

ちょっと練習の第二問で、標準関数を使わなかった場合、マンハッタン距離を求める関数内で「絶対値を求める処理」が沢山登場すると思います。

ここも関数化してみましょう。

```cpp
#include <iostream>

int abs(int value) {
    if (value >= 0) {
        return value;
    }
    else {
        return -value;
    }
}

int distance(int x, int y) {
    int res = abs(x) + abs(y);
    return res;
}

int main() {
    int x, y;
    std::cin >> x >> y;
    
    int ans = distance(x, y);
    std::cout << ans << std::endl;
    
    return 0;
}
```

今まで言及できていませんでしたが、関数を呼び出すことができるのは`main`関数だけの特権ではありません。どの関数も他の関数を呼び出すことができます。

ただし、呼び出す関数は自身より上に定義(正確には、宣言)されている必要があります。

```cpp
int distance(int x, int y) {
    int res = abs(x) + abs(y);
    return res;
}

int abs(int value) {
    if (value >= 0) {
        return value;
    }
    else {
        return -value;
    }
}
```

上記はエラーです。ただし、この順番に定義を書いてもエラーを回避する方法は存在します
- プロトタイプ宣言ということをします。プログラミング入門でもやると思うので詳しくはそちらに委ねます。

#### ちょっと練習2

10要素のテストの点数を受け取って、その分散を計算するプログラムを作成してください。

#### 再帰関数

おまけ程度に見てください。`main`関数を除く関数は関数内で自身を呼び出すことができます。

```cpp
#include <iostream>

int fuctorial(int N) {
    if (N == 0) {
        return 1;
    }
    else {
        return factorial(N - 1) * N;
    }
}

int main() {
    std::cout << factorial(5) << std::endl;

    return 0;
}
```

## 引数

#### 参照渡し

前回、関数の引数に与えた変更は呼び出し元には影響が無いと説明しました。

```cpp
#include <iostream>

int func(int value) {
    value = 1;
    return value;
}

int main() {
    int value = 3;
    
    std::cout << func(value) << std::endl;
    std::cout << value << std::endl;

    return 0;
}
```

これは、引数に渡した`value`が関数の処理の時点でコピーされて、コピーされた`value`に対して`value = 1`をしているからです。
- このような引数の渡し方を「値渡し」といいます。

値渡しは良くも悪くもコピーをするので、メモリの大きいデータ(例えば、`std::vector`などの複数のデータ)をコピーするとそのコピーの分パフォーマンスが落ちます。
- ちょっとくらいなら大丈夫ですが、関数呼び出しを沢山してコピーを積み重ねると結構処理が重くなります。

そのような時の、コピーをしない引数の渡し方として「参照渡し」があります。

```cpp
#include <iostream>

int func(int& value) {
    value = 1;
    return value;
}

int main() {
    int value = 3;
    
    std::cout << func(value) << std::endl;
    std::cout << value << std::endl;

    return 0;
}
```

引数の型名の後に`&`をつけるとデータをコピーせず直接参照する「参照渡し」になります。

コピーをしませんが、呼び出し元のデータに変更を加えているこちに注意してください。
- もちろん、直接変更を加えることを目的に参照渡しを使うこともあるでしょう

## ちょっと練習

1. ３つの引数 $a, b, c$をとって、$a + b$の計算結果を$c$に代入する`void`型の関数を作成してください。
2. `std::vector<int>`を引数に与えて、各要素を標準入力から与えられた整数を代入する`void`型の関数を作成してください。

#### const参照渡し

コピーをしたくないが、呼び出し元引数のデータに変更を加えたくない時は、`const`参照渡しをします。

```cpp
#include <iostream>
#include <vector>

int func(const std::vector<int>& A) {
    int res = 0;
    for (int& a : A) {
        res += a;
    }
    return res;
}

int main() {
    std::vector<int> A = { 1, 2, 3, 4, 5 };
    std::cout << func(A) << std::endl;
    return 0;
}
```

`const`参照渡しをした引数のデータに対して関数内で変更を加えようとするとコンパイルエラーになります。

#### 使い分け、まとめ

- `int`や`double`、`char`、`bool`などの基本的なデータ型に対しては「値渡し」
- `std::vector`や`std::string`などに対しては「const参照渡し」
- 呼び出し元のデータに変更を加えたい時は「参照渡し」


## クラス

クラスはデータとそのデータに対する処理をまとめて扱うことができるものです。

- 宣言・作成する時にする処理(コンストラクタ)
- 所持しているデータ(メンバ変数)
- 所持しているデータに対して、あるいはデータを利用してなにか処理を行う(メンバ関数)
- 上記のメンバ変数や、メンバ関数のアクセス権限の管理
- そのデータに対して演算子を定義する(operator)
- クラスを破棄する時に行う処理(デストラクタ)

などの特徴があります。今回の勉強会では上4つを紹介します。

#### 例1

いままで扱って来た`std::vector`はクラスの最たる例の一つです。

宣言時に(3, 1)とかやっていたのはコンストラクタです。

`push_back()`などはメンバ関数です。

`[0]`などは`[]`演算子の挙動を定義したものです。

#### 例2

沢山の生徒が国語、英語、数学のテストを受けました。生徒には出席番号と名前があります。
- 後で点数の平均値などを出したい需要があります。
これに対して

```
int tanaka_japanese = 10, tanaka_english = 10, tanaka_math = 5;
int tanaka_id = 3;
std::string tanaka = "tanaka";

double tanaka_ave = (double)(tanaka_japanese + tanaka_english + tanaka_math) / 3.0;

int suzuki_japanese = 5, suzuki_english = 20, suzuki_math = 5;
....

```
などとするのは非常に効率が悪いです。


こういったものをクラスによって表現することができます。


#### クラスの基本的な使い方

```cpp
#include <iostream>

class student {
private:
    int japanese, english, math; 

    int max(int a, int b) {
        if (a <= b) {
            return b;
        }
        else {
            return a;
        }
    }

    int sum() {
        return japanese + english + math;
    }


public:
    student(int japanese, int english, int math)
        : japanese(japanese), english(english), math(math) {}

    double calcAverage() {
        return (double)sum() / 3.0;
    }

    int getMax() {
        int res = max(japanese, english);
        res = max(res, math);
        return res;
    }
};

int main() {
    student tanaka(12, 5, 8);
    std::cout << tanaka.calcAverage() << std::endl;
    std::cout << tanaka.getMax() << std::endl;

    return 0;
}
```

一つ一つ要点をかいつまんでいきます。

```cpp
class student {

};
```

`class`というキーワードを指定して、その後ろにクラスの名前を書きます。実装は`{}`で囲んだ中に書きます。
- `{}`の最後にセミコロンが必要なことに注意です。

```cpp
private:
    int japanese, english, math;
```

`private`は一旦飛ばします。

`class`には変数をもたせることが可能で、いままで同じように宣言することが可能です。
- こういったクラスが持つ変数を「メンバ変数」といいます。

```cpp
int max(int a, int b) {
....
}

int sum() {
}
```

`class`には関数をもたせることが可能です。
- こういったものをメンバ関数といいます。
- 引数に与えることなく、メンバ変数を利用することが可能です。(メンバ変数を利用する場合、値はコピーされていません)

```cpp
student(int japanese, int english, int math)
    : japanese(japanese), english(english), math(math) {}
```

これもメンバ関数に見えますが、この子はちょっと特殊です。
- 返却値型が指定されてない
- 関数の名前がクラスの名前と等しい

このようなものをコンストラクタといいます。クラスが宣言された時に呼び出されるものです。

```cpp
    double calcAverage() {
        return (double)sum() / 3.0;
```
普通の関数と同様に、メンバ関数内でメンバ関数を呼び出すことができます。
- もちろん、呼び出す関数は上で定義するか、プロトタイプ宣言をすませておくこと

```cpp
int main() {
    student tanaka(12, 5, 8);
```

作成したクラスを宣言する際には、普段の`int`や`std::vector`と同様にします。
- ただし、コンストラクタで定義した引数に揃えるように`()`の中身を指定します。

```cpp
    std::cout << tanaka.calcAverage() << std::endl;
    std::cout << tanaka.getMax() << std::endl;
```

名前`.メンバ関数名`とすることで定義したメンバ関数を呼び出せます。


#### publicとprivate
```cpp
private:

```
と書いた部分は、クラスの外からはアクセスすることができません。例えば、上のサンプルコードで`tanaka.max(10, 20)`などとしてみましょう。エラーになります。
```

`public:`においたものは外からアクセスすることができます。`.OOO`を利用することで...

何も指定しなかった場合は`private`扱いになります。

基本的に外から呼び出す必要の無いものは`private:`においておきましょう。


#### ちょっと練習3

1. `student`クラスに整数型の生徒の出席番号を追加してみてください。
2. `student`クラスに`std::string`型の生徒の名前を追加してみてください。
3. 名前、出席番号、テストの点数を順に出力するメンバ関数を作ってみてください。
