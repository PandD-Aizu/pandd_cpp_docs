---
layout: default
---

# プログラマ勉強会 第五回

## 目次

- [イントロダクション](#イントロダクション)
- [クラスについて復習](#クラスについて復習)
- [std::complex](#std::complex)
- [座標上の点クラスを作成する](#座標上の点クラスを作成する)

## イントロダクション

今回は、前回軽く触った`class`について、実際に`class`を作成しながら作り方を理解してもらいます。初歩的な内容しか触れない予定なので、もっと知りたいという方は公式リファレンスなどをご参照ください。

## クラスについて復習

初回から、第四回勉強会の前半まで私達は基本的なデータを利用して計算を行う方法について学んできました。
- 整数や小数、文字、真理値などの基本的なデータ(プリミティブ)

しかし、現実世界ではそれらのデータを複数組み合わせたものが沢山登場します。
- 前回でいうと、「生徒」というデータを扱うために「3教科のテストの点数」「出席番号」「名前」という複数のデータをまとめて管理する必要がありました。

また、そのデータ特有の処理も存在します。
- 「生徒」の例だと「テストの点数の平均値を割り出す」などがありました。

このようなデータ、データ操作を実現するのにクラスが有効でした。

## std::complex

#### 複素数を扱う標準機能

復習の一貫として、`C++`の標準機能にある複素数を扱うクラスを見てみましょう。複素数は２つの実数を利用して表現することができる数です。(実数と実数の組み合わせですね)

サンプルコード

```cpp
#include <iostream>
#include <complex>

int main() {
    std::complex<double> A(1.0, 2.0);
    std::cout << A.real() << std::endl;
    std::cout << A.imag() << std::endl;

    std::complex<double> B(2.0, 3.0);
    A += B;
    std::cout << A.real() << std::endl;
    std::cout << B.imag() << std::endl;

    return 0;
}
```

上のサンプルコードと[リファレンスの日本語訳](https://cpprefjp.github.io/reference/complex/complex.html)を交互に見ながら進めていきます。

まず、`complex`ヘッダをインクルードします。`std::vector`や`std::string`の時と同じですね。
- `C++`の標準機能を利用するには何かしらのヘッダをインクルードしなければいけないことが多いです。
- リファレンスのヘッダのページを参照して、インクルードファイルを見つけてください。

#### コンストラクタ

リファレンスのメンバ関数の`(constructor)`と書かれている所をクリックしてみましょう。`std::complex`のコンストラクタの簡単な説明がでてきます。

コンストラクタとは、そのクラスが作られるときに行う処理です。
- `std::vector`などでは、`std::vector<int> A(3, 2)`などとしていましたね。これは $(2, 2, 2)$ を作る処理をしていました。

サンプルコードでは、コンストラクタの`(1)`を試しています。実部に$3.0$ 、虚部に $2.0$ を代入した複素数`A`を作っています。
- つまり $A = 3.0 + 2.0i$ です。

#### メンバ関数

メンバ関数は、クラスに紐付いた処理です。今回だと`real()`と`imag()`があります。`std::vector`の時と同様に`.OOOO(引数)`とすることで呼び出すことができます。
- コンストラクタもメンバ関数です。

- 同じメンバ関数名でも、引数の数・型の種類・順番が異なると処理が異なることがあります。自分でクラスを作る時も、引数の数・型の種類・順番によって行う処理を変えることができます。

今回の`real`、`imag`では「引数を取らない場合」と「`T`型のデータを一つとる場合」があります。
- `T`型とは、<>の中で指定した型のことだと思ってもらえれば十分です。

引数をとらない場合は現在の実部、虚部を値として返すようになっています。

引数を取る場合は、実部、虚部に与えられた値を設定するようになっています。

#### operator

今回の勉強会では詳しく扱いません。演習問題のおまけ枠などに置いておきます
- 端的に言うと、そのクラスに対する演算子を定義することができます。
- `std::complex`だと、四則演算、比較演算子、`std::cin, std::cout`の`<<`、`>>`の演算子に対する挙動が定義されているようです。

#### ちょっと練習

1. $c = 1.5 + -3.0i$ を`std::complex`型で表現してみましょう。
2. `C++`のハッシュマップを試してみましょう[リファレンス](https://cpprefjp.github.io/reference/unordered_map/unordered_map.html)


## 座標上の点クラスを作成する

#### 座標上の点

先程まで見ていた複素数に似ていて、なおかつ複素数より(おそらく)フレンドリーな二次元座標上の点を表現するクラスを作成してみましょう。
- $x$ 座標、 $y$ 座標を管理します
- 原点からの距離を返す関数を作ります


#### class定義

```cpp
#include <iostream>

class Point {
};

int main() {
    return 0;
}
```

何も中身が実装されていない`Point`クラスを作成しました。

`class`キーワード、スペース、クラスの名前、波括弧とします。
- 本当に何も実装しない時は波括弧はいらないですが、そのようなことは大抵無いので...

最後にセミコロンが必要なことだけ把握してください。

#### 試しにクラスを呼び出してみる

```cpp
int main() {
    Point p;
    return 0;
}
```

`int`や`std::vector`の時と同じように宣言することができます。当然ですが、`Point`に何も実装していないので今作った`p`は特になにかできることはありません。

#### メンバ変数

$x$ 座標と $y$ 座標を保管する変数を用意します。

```cpp
class Point {
    double x, y;
};
```

このようなクラスの中に定義された変数を「メンバ変数」といいます。

`main`関数の方で宣言していた`p`でこの`x, y`にアクセスしてみましょう。
- メンバ関数と同じように.OOOでアクセスできます。

```cpp
int main() {
    Point p;
    std::cout << p.x << ' ' << p.y << std::endl;
    return 0;
}
```

残念ながら、これはコンパイルエラーとなります。
- error: `double Point::x` is private within this context

メンバ変数、関数はデフォルトでは呼び出し側から隠されています。(アクセス制限されている。なんて言ったりします)

呼び出し側からアクセスするには、そのメンバ変数やメンバ関数を公開する必要があります。

```cpp
class Point {
public:
    double x, y;
};
```

この`public:`をアクセス指定子といいます。

`public:`と書かれた所から下(他のアクセス指定子が出てくるまで)に定義された変数、関数は外部から呼びだし可能になります。

#### コンストラクタ

コンストラクタを定義して、作成時に $x$ 座標 $y$ 座標を設定できるようにしましょう。

```cpp
class Point {
public:
    double x, y;
    Point(double initX, double initY) : x(initX), y(initY) {}
};
```

コンストラクタは関数のように書きますが、いくつか異なる点があります。
- 返却値型を書きません。(なにか値を`return`することができません)
- 名前をクラスの名前と一緒にします
- `:` と`{}`の間でメンバ変数の初期化をすることができます
   - 例えば、`x(initX)`でメンバ変数`x`を引数の`initX`で初期化することができます。

このコンストラクタを使って`p`を初期化しましょう。

```cpp
#include <iostream>

class Point {
public:
    double x, y;
    Point(double initX, double initY) : x(initX), y(initY) {}
};

int main() {
    Point p(1.0, 2.0);
    std::cout << p.x << ' ' << p.y << std::endl;
    return 0;
}
```

このプログラムを実行すると、無事`1.0 2.0`と出力されると思います。

#### 距離を返す関数

原点からその点までの距離を返す関数を作成してみましょう。
- 今回はユークリッド距離で作成しますが、他の距離で作っても良いです。

```cpp
#include <iostream>
#include <cmath>

class Point {
public:
    double x, y;
    Point(double initX, double initY) : x(initX), y(initY) {}

    double distance() {
        return sqrt(x * x + y * y); 
    }
};

int main() {
    Point p(1.0, 2.0);
    std::cout << p.x << ' ' << p.y << std::endl;
    std::cout << "distance is " << p.distance() << std::endl;
    return 0;
}
```

(平方根を取るには`cmath`ヘッダをインクルードして`sqrt`関数を使用します)

普段の関数の定義と同じように作成します。メンバ変数は引数に指定しません。

#### std::complexと似た実装にする

現在はメンバ変数の`x`、`y`のアクセス権限がpublicであるため、呼び出し側から直接この値をいじることができます。

```cpp
int main() {
    Point p(1.0, 2.0);
    std::cout << p.x << ' ' << p.y << std::endl;

    p.x = 10.0;
    std::cout << p.x << std::endl;

    return 0;
}
```

ここでいきなりですが、`x, y`のアクセスを制限します。

```cpp
class Point {
private:
    double x, y;

public:
    Point(double initX, double initY) : x(initX), y(initY) {}

    double distance() {
        return sqrt(x * x + y * y); 
    }
};
```

`private:`はクラスの内部でしかアクセスできないようにします(例外はありますが、触れません)
- デフォルト(何もアクセス指定子を書いていない時)と同じアクセス権限です。しかし、`private:`と書いた方がわかりやすいでしょう。

この状態で`x`座標を返すメンバ関数を作ってみます。

```cpp
class Point {
private:
    double x, y;

public:
    Point(double initX, double initY) : x(initX), y(initY) {}

    double distance() {
        return sqrt(x * x + y * y); 
    }

    double X() {
        return x;
    }
};

int main() {
    Point p(1.0, 2.0);
    std::cout << p.X() << std::endl;
    // std::cout << p.x << std::endl; エラー！！

    return 0;
}

```

`std::complex`と同じメンバ関数名で、 $x$ 座標に新しい値を設定できるようにしてみます。

```cpp
class Point {
private:
    double x, y;

public:
    Point(double initX, double initY) : x(initX), y(initY) {}

    double distance() {
        return sqrt(x * x + y * y); 
    }

    double X() {
        return x;
    }

    void X(double newX) {
        x = newX;
        return;
    }
};

int main() {
    Point p(1.0, 2.0);
    std::cout << p.X() << std::endl;
    p.X(5.0);
    std::cout << p.X() << std::endl;

    return 0;
}
```

$x$ 座標に関しては値の取得、設定ができるようになりました。

#### ちょっと練習

1. $y$ 座標も同様に値の取得、設定ができるようにしましょう。
2. `Point`型を引数にとって、引数の $x$ 座標、 $y$ 座標を自身に代入するメンバ関数を作ってみましょう
3. $z$ 座標を追加して、 $3$ 次元座標にしてみましょう。
