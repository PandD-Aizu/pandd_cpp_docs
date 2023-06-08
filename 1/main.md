# プログラマ勉強会第一回資料

## 目次

- [はじめに](#anchor1)
- [はじめてのC++](#anchor2)
- [変数と型](#anchor3)
- [コメントをふる](#anchor4)
- [演習問題第一回](#anchor5)


<a id="anchor1"></a>
## はじめに

#### 大事なお願い

この資料やスライドを勉強会参加者以外に見せないでください
- 不備や誤りがあった場合の対応を楽にするためです

<br />

#### この勉強会の目標

- Siv3Dを扱うための基本的なC++の文法を習得する
- Siv3Dで動くものを作成する
- 検索力・考察力を養う

<br />

#### Siv3Dを扱うための基本的なC++の文法を習得する

具体的にこの勉強会では以下を扱います。勉強会を終えた時点で、この中の6 ~ 10割ほど何となくニュアンスを理解できるようになってくれれば幸いです。

(*がついたものは、勉強会では端折る可能性が高いですが、資料には追記しておく予定です)

- 基本的な出力方法
	- 四則演算・剰余
- `std::vector`
	- `operator []`
	- `push_back()`*
	- `pop_back()`*
	- `iterator`*
- 条件分岐(if文、switch-case文)
	- 論理演算子
	- 比較演算子
	- 短絡評価*
- 繰り返し
	- `for`
	- `while`
	- `continue`
	- `break`
	- `range based for`*
- 関数
	- 値渡しと参照渡し
	- 返り値、値返却型
	- スコープの概念
    - ラムダ式 *
    - 関数オブジェクト *
    - `std::function` *
- `class`
	- `private`と`public`
	- コンストラクタ
	- デストラクタ*
	- メンバ
	- 継承
- `namespace`*
- `enum, enum class`*
- `STL`*
	- `std::set`
	- `std::map`
	- `std::sort`
	- `std::max_element`
	- `std::accumulate`

<br />

#### Siv3Dで動くものを作成する

説明無しに「Siv3D」という単語を何回か出してしまいました。

[Siv3D](https://siv3d.github.io/ja-jp/)とは、主に2Dゲーム・ビジュアライザ等に有用なC++フレームワークです。もっと簡単にいうと、「企画開発部がゲームを作る時に使うやつ」です

新入生歓迎会等でOBや部員が作成したゲームをプレイしたかもしれません。これらはSiv3Dを利用して作られています。[^1]

今回の勉強会の後半でもSiv3Dプログラミングを体験してもらいます。ここで[Cookie Clicker](https://orteil.dashnet.org/cookieclicker/) の再現を目指します。

<br />

#### 検索力・考察力を養う

勉強会では毎回演習問題に取り組んでもらいますが、たまに特殊な問題が混じっています。
- 勉強会で説明していない用語や機能が登場する
- 他の問題や、prog0の課題の問題と比べて難しい

前者に関しては、まずはネット検索で色々調べてみてください。`OOO C++`とかで調べれば多分ヒントがあります。多分。

後者は頑張ってください。

演習問題等について、わからないことがあったら遠慮せずに先輩等に質問しましょう。

#### 環境について

C++のコードを実行する環境として、今回は以下の３つのうちどれかを採用すれば大丈夫です。
1. web上のC++実行環境(例えば、[Wandbox](https://wandbox.org/#))
2. 学内環境(g++が入っているはず)
3. 自力で環境構築する
	- MacかLinuxなら多分直ぐに終わります。(私はMacは知らないので微妙なんですけど...)
	- Windowsはちょっと面倒。WSLを入れてLinuxのプログラムを実行できるようにするのが一番楽かも

自力で環境構築する際も遠慮なく先輩を頼って大丈夫です(zawaは機械音痴なので頼るとちょっと怖いかも?)

<br />

#### コードの実行の練習

ここにサンプルコードを置いておきます。
- ファイル名は"sample.cpp"等にしてください。拡張子を必ず「.cpp」にしてください。
```cpp
#include <iostream>

int main() {
    std::cout << "3つの整数を空白区切りで入力してください" << std::endl;
    int a, b, c;
    std::cin >> a >> b >> c;
    std::cout << "和は " << a + b + c << " です" << std::endl;
}
```
Wandboxを利用している人は、画面右に「標準入力」というタブがあると思います。それをクリックして開いて整数を３つ入力してください。実行を押すと入力内容を受け取ってプログラムを実行します。

学内環境・ローカル環境を利用している人はターミナル上で(`ls`等で`sample.cpp`があることを確認して)
```bash
g++ sample.cpp
```
とコマンドを実行してください。

これはコンパイルと言って、人間が書いたC++のプログラムを機械が読めるように翻訳しています。翻訳したものを実行ファイルといいます。

その後に`ls`すると、実行ファイル`a.out`があることが確認できると思います。

```bash
./a.out
```
でプログラムを実行できます。3つの整数を入力してみてください。

<br />

<a id="anchor2"></a>
## はじめてのC++

#### C++とは

2Q 「プログラミング入門(prog0)」で習う「C」言語の派生言語です。
- 「C」の文法をある程度踏襲しています
- 良くも悪くも「C」と比較して沢山の文法があります。
- 演習問題の解答は「C++」での解答とは別に「C」の解答も用意しておくつもりです。「C」の授業と「C++」の授業で頭が混乱したら両方のコードを読んで違いを噛み砕いてください。

<br />

#### 最初のプログラム

さっそくC++プログラマーの第一歩を踏み出しましょう。以下のコードを写経し、実行してみましょう。

```cpp
int main() {
	return 0;
}
```
`return 0`前の空白はタブキーを押すことで再現することができます(この空白をインデントといいます)。反対に、Shiftを押しながらタブキーを押すことでこの空白が引っ込みます。

これは何もしないプログラムです。もっと正しく言うと、即終了するプログラムです。

一つ一つ紐解いてみましょう

```cpp
int main() {
}
```
これは、**main関数**といいます。

`int main(){}`はどのcppファイルにも必ず一つ必要です。0個でも2個以上でもダメです。CPUはこの`main() {}`の`{ }`に囲まれた中身の命令を原則**上から順**に評価して実行します。

`return 0`でプログラムを終了します。0以外の数を入れても問題無いはずですが(多分)、0でreturnするとOSが「プログラムが正常に終了した」と認識します[^2]。0以外は異常終了を意味するので、無意味に0以外にするのはやめましょう。

一個の命令の終わりには必ず「;」が必要です。忘れるとコンパイルエラーになります。

<br />

#### 文字の並びを出力しよう

次にターミナルに「Hello World」と出力しましょう。

```cpp
#include <iostream>

int main() {
	std::cout << "Hello World" << std::endl;
	return 0;
}
```

もしあなたがAOJのアカウントを持っているのなら、[こちら](https://onlinejudge.u-aizu.ac.jp/courses/lesson/2/ITP1/1/ITP1_1_A) に提出することで間違ってないことを確認できます。アカウントを持っていなくても目視で確認できれば大丈夫です。

```cpp
#include <iostream>
```
`#include`で`C++`に用意されている様々な機能を利用できるようにすることができます。`iostream`は入出力に関する機能を集めたものです。

```cpp
std::cout << 
```
`std::cout`によって`<<`の後ろに続く数や文字の並びを出力することができます。

```cpp
"Hello World"
```

ダブルクォーテーションマークで囲んだ単語や文章は文字の並びと認識されます。[^3]   
今回は「Hello World」が出力されることになります

```cpp
std::endl;
```
これによって改行できます。[^4]

最後に「;」が必要なことに気を付けてください。

<br />

#### ちょっと練習

次の文を出力するプログラムを書きましょう

1. 「Pine and Daikon」
2. 「C++完全に理解した」
3. 「古池や
		蛙飛び込む
		水の音」

3に関しては、改行も入れるのがミソです。頑張ってください。

正解は勉強会終了後に追記します。今は先輩等にチェックしてもらってください。

<br />

#### 数を出力しよう

`std::cout`は数も出力することができます。

```cpp
#include <iostream>

int main() {
    std::cout << 2 << std::endl; // 2を出力する
    std::cout << 1.5 << std::endl; // 1.5を出力する
    std::cout << 0 << std::endl; // 0を出力する
    return 0;
}
```

文字の並びを出力する時とは異なり、ダブルクォーテーションマークで挟む必要が無いです。

さらっとでていますが、

```cpp
std::cout << 2 << std::endl; // 2を出力する
```

// の後に続く文章は、プログラムは無視します。(コメントといいます。)

他人や未来の自分にプログラムの意図を伝えることができる大事な機能なので、ぜひ積極的にご活用ください。

<br />

#### 簡単な計算をしてみよう

多くのプログラミング言語にとって、四則演算と剰余算[^5]は基本です。それはC++も例外ではありません。

```cpp
#include <iostream>

int main() {
    std::cout << 2 + 3 << std::endl; // 2 + 3 を出力する
    std::cout << 5 - 1 << std::endl; // 5 - 4 を出力する
    std::cout << 100 * 900 << std::endl; // 100 x 900を出力する
    std::cout << 7 / 2 << std::endl; // 7 ÷ 2 を出力する
    std::cout << 10 % 3 << std::endl; // 10を3で割った余りを出力する
    return 0;
}
```

`+`や`-`は良いとして、掛け算は`x`ではなく`*`、割り算は`/`で計算することができます。剰余算は`%`です。

上のコードを実行すると、 $\frac{7}{2}$ が $3$ と出力されていることが見て取れます。整数同士の除算は切り捨てられます。

```cpp
#include <iostream>

int main() {
    std::cout << 2 + 3 * 4 << std::endl; // 14
    std::cout << (2 + 3) * 4 << std::endl; // 20

    std::cout << 3 * 4 + 2 * 5 << std::endl; // 22
    std::cout << 3 * (4 + 2) * 5 << std::endl; // 90
    return 0;
}
```

演算の優先順位は普段の計算と同様です。括弧もあります。

四則演算のプログラムの練習はあとでやります。

<br />

#### 数を入力する

今までで数や文字の並びを出力しました。今度は数を入力してみましょう

予想がついた人もいるかもしれません。出力時は`cout`、つまり「out」なので入力は「in」で`cin`です。未説明の内容を含むコードですが、一旦気にせず写経して実行してみてください。

```cpp
#include <iostream>

int main() {
	int value;
	std::cin >> value;
	std::cout << value << "が入力されました。" << std::endl;
	return 0;
}
```

`cout`では`<<`でしたが、`cin`では`>>`ですね。
- 無理に覚える必要は無いです。演習問題や自習を積み重ねると自然と手が覚えますし、忘れた度に都度コンパイルエラーに引っかかる or 調べるで済む話です

<br />

<a id="anchor3"></a>
## 変数と型

#### 変数と型の説明

C、C++を含む多くの言語には**変数**というものがあります。変数とは、データを格納して覚えておいてくれる箱のような物です。変数(箱)が存在する限り、その箱の中身を取り出したり別のデータを入れたりすることが可能です。

先程のコードの
```cpp
int value;
```
は`value`という名前の変数を用意していました。このように変数を用意することを**宣言**するといいます。ここに
```cpp
std::cin >> value;
```
とすることで、標準入力で得たデータを`value`に入れていました。そして、
```cpp
std::cout << value << ...
```
で`value`の中身を標準出力していました。この変数の名前は何でも良く(何個かだめなルールはありますが)

```cpp
int mikan;
std::cin >> mikan;
```
とか、
```cpp
int super_long_long_long_long_long_name_value;
std::cin >> super_long_long_long_long_long_name_value;
```
とかやっても良いです。基本は状況に即して適切で簡潔な名前をつけることになるでしょう。

さて、変数には色々種類があります。変数の種類によってそのデータの記憶の仕方や、様々な標準機能の動作の仕方が異なります。

以下のコードを実行して、標準入力に`1.5 1.5`と入力してみてください。
```cpp
#include <iostream>

int main() {
	double value1;
	std::cin >> value1;
	int value2;
	std::cin >> value2;
	std::cout << "value1 is " << value1 << std::endl;
	std::cout << "value2 is " << value2 << std::endl;
	return 0;
}
```
1.5を入力したはずなのに、value2が1になっていますね。このように結果が変わってしまう原因は`int`と `double`の違いにあります。

`int`はintegerからとられていて、「整数」を意味します。

`double`は「浮動小数点数」といって、コンピュータで実数を扱うためのものです[^6][^7]。

このような、データの種類を**型**といいます。

基本的な型の種類
| 型名 | 扱えるデータ | 注釈 |
| :---: | :---: | :---: |
| int | 整数 | |
| long | 整数 | intより絶対値が大きい数も扱える(勿論限界はある) |
| double | 浮動小数点数 | |
| long double | 浮動小数点数 | doubleより精度が高い |
| char | 単一の文字 | |
| bool | 真理値 | |
| void | 無 | void型の変数を宣言できない |

型によって、先程やった四則演算の結果も変わります。例えば

```cpp
#include <iostream>
int main() {
  int a = 1, b = 2;
  double c = 1, d = 2;
  std::cout << (a / b) << std::endl;
  std::cout << (c / d) << std::endl;
  return 0;
}
```
を実行してみてください。`int`型どうしの割り算は小数点以下切り捨てが発生しますが、`double`型どうしは小数点以下も考慮されていることがわかると思います。

<br />

#### 変数の初期化・代入

上のコードではさらっと
```cpp
int a = 1, b = 2;
```
とかいています。変数の後に、 `=`と値を続けることで、変数にその値を入れることができます。これを**代入**といいます[^8]。

また、変数の宣言と同時に代入することを**初期化**といいます。

はじめて値が代入される前、変数には何が入っているか定かではありません。必ず変数を使う時はその変数に何かしらの値を代入したか、或いは初期化を行ったか確認しましょう。
- 標準入力`std::cin >> `等をするみたいな事情がない場合は初期化によって変数に不定値が入っている状況を解消すべきでしょう。

<br />

#### ちょっと練習2
1. ２つの整数を`int`型で標準入力で受け取って、色んな四則演算をしてみましょう
2. 2つの`int`型の変数を宣言して、何かしらの値で初期化、その変数で色んな四則演算をしてみましょう。
3. `3 / 0`みたいな0割り算をためしてみましょう。どうなるかな?`3.0 / 0.0`なら..?

<br />

#### 四則演算と代入の組み合わせ

文法だけの解説にとどめます。
```cpp
#include <iostream>

int main() {
  int a = 1;
  a += 2;
  std::cout << a << std::endl;
  return 0;
}
```
これは`3`を出力します。
`+=`、`-=`、`*=`、`/=`、`%=`等は左辺の変数の値にに右辺の値を足し算/引き算/・・・/したものを左辺の変数の値に出力します。

上のサンプルコードは以下と同値です。
```cpp
#include <iostream>

int main() {
  int a = 1;
  a = a + 2;
  std::cout << a << std::endl;
  return 0;
}
```
ここで、`=`は代入を意味する演算子であり、数学でいう「等しい」を意味するものでは無いことに注意してください。最初は混乱すると思いますが、なれると

<a id="anchor4"></a>
## コメントをふる

#### コメント

どのような目的であれ、プログラムを書いているとメモを残したいとなる状況が多々あります。そのような時に有用なのがコメントです。

```cpp
/*
標準入力から一つの整数を受け取って、10を足したものを出力するプログラム
*/
#include <iostream>

int main() {
  int input_value; // input_valueという名前の変数を宣言
  std::cin >> input_value; // 標準入力でinput_valueに値を読み込む
  int output_value = input_value + 10;
  std::cout << output_value << std::endl;
  return 0;
}
```
`/**/`で囲まれた部分は全てコメントとなり、プログラムと無関係な文章を残すことができます。
`//`の後ろは、その行に限りコメントとなり、プログラムと無関係な文章を残すことができます。

#### コメントを残す意義

以下に続くのは私が1年4Q「アルゴリズムとデータ構造」のとある課題で提出したコードです(C言語)
- 1年の4学期にはこんな長いコードを書かされる課題が出るんですね。辛い...

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node *NodePointer;
struct Node {
    int key;
    int priority;
    NodePointer left;
    NodePointer right;
};

NodePointer root;

NodePointer create_node(void);
NodePointer add_node(int, int);
NodePointer right_rotate(NodePointer);
NodePointer left_rotate(NodePointer);
NodePointer preorder_walk(NodePointer);
NodePointer inorder_walk(NodePointer);
NodePointer insert(NodePointer, int, int);
NodePointer find(int);
NodePointer delete(NodePointer, int);

int main() {
    int num_query;
    scanf("%d", &num_query);

    for (int i = 0 ; i < num_query ; i++) {
        char query[7];
        scanf("%s", query);
        
        if (query[0] == 'i') {
            int key, priority;
            scanf("%d%d", &key, &priority);
            root = insert(root, key, priority);
        }

        else if (query[0] == 'f') {
            int key;
            scanf("%d", &key);
                NodePointer x = find(key);
            if (x != NULL)
                printf("yes\n");
            else
                printf("no\n");
        }

        else if (query[0] == 'd') {
            int key;
            scanf("%d", &key);
            root = delete(root, key);
        }

        else if (query[0] == 'p') {
            inorder_walk(root);
            printf("\n");
            preorder_walk(root);
            printf("\n");
        }
    }

}

NodePointer create_node() {
    NodePointer x = (NodePointer)malloc(sizeof(struct Node));
    return x;
}


NodePointer find(int key) {
    NodePointer x = root;
    while(x != NULL) {
        if (x->key == key)
            return x;
        else if (x->key > key)
            x = x->left;
        else
            x = x->right;
    }

    return x;
}

NodePointer delete(NodePointer t, int key) {
    if (t == NULL)
        return NULL;
    
    if (key < t->key)
        t->left = delete(t->left, key);
    else if (key > t->key)
        t->right = delete(t->right, key);
    else {
        if (t->left == NULL && t->right == NULL)
            return NULL;
        else if (t->left == NULL)
            t = left_rotate(t);
        else if (t->right == NULL)
            t = right_rotate(t);
        else {
            if (t->left->priority > t->right->priority)
                t = right_rotate(t);
            else
                t = left_rotate(t);
        }

        return delete(t, key);
    }
    
    return t;
}
```

こんなの読める訳が無いんですよね。自分も読めないです。
- そもそもこのコードがどのようなプログラムなのかわからない
- 各処理が何をしているのか説明がまったくない

というのが問題です。文法とかの話では無いです。

単純な話、冒頭に
```c
/*
アルゴリズムとデータ構造の課題のコード
Treapを実装
s1290001 愛澤透哉
*/
#include <stdio.h>
#include <stdlib.h>
```
みたいなことが書いてあれば、「ああこれはTreapというデータ構造を実装したものなんだな」とわかって、目的がわかると「じゃあ`NodePointer`ってTreapの頂点なのかな」とか「insertってTreapに新しい頂点を挿入しているかな」みたいにコードに対する考察が進みます。

さらにコードの中身にも
```c
        // クエリの文字列の最初の文字で、クエリの種類を特定する
        if (query[0] == 'i') {
            int key, priority;
            scanf("%d%d", &key, &priority);
            root = insert(root, key, priority);
        }
```
みたいなことが書いてあれば、`if (query[0] == 'i')`という意図の不明な条件分岐にも、目的がわかります。
- `if`文は次回勉強会で取り扱います。条件分岐ができるようになります。

- 処理が書いてあるモチベーション・目的
- 難解な処理に対しては、噛み砕いた説明
- 関数(第3回で扱います)の引数や返り値の用途の説明

等があると親切でしょう。チーム開発のメンバーや未来の自分のためにも、コメントはある程度ふるようにしましょう。

<br />

<a id="anchor5"></a>
## 演習問題

別の資料にのせています。

<br />

[^1]: 一つ例外があって、MIP(4人でコントローラーで遊ぶやつ)は違うやつを利用しています。企画開発部がSiv3Dを採用する前に制作されたゲームです。

[^2]: 実はmain関数のreturnは省略しても動きますが、書く方がお行儀が良いです。

[^3]: 正確には文字列リテラルといいます

[^4]: 改行以外にも色々やってますが、勉強会の趣旨から大きく外れるので省略

[^5]: aをbで割った余りのことです

[^6]:実数は $\sqrt{3}$ 等、無限小数になることがあります。コンピュータでは無限小数を扱えないので有限桁の小数で近似値として扱います。

[^7]: 浮動小数点数のことを「小数」と言うと多方面から叱られるので、用語の使い分けは意識しましょう。本当に申し訳ない話なのですが、私は用語の使い分けがかなりルーズになってしまっているのでこの資料でも間違いとかが潜伏しているかもしれません.....

[^8]: さらにさらっと書いちゃっていますが、同じ型ならカンマ区切りで変数の宣言を横並びに書けます。
