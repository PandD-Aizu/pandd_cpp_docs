---
layout: default
---

## X Cubic

```cpp
#include <iostream>

int main() {
    int x;
    std::cin >> x;
    int ans = x * x * x;
    std::cout << ans << std::endl;
    return 0;
}
```

基本的な入出力のやり方を問う問題でした。

C言語だと以下のように書きます。

```c
#include <stdio.h>

int main() {
    int x;
    scanf("%d", &x);
    int ans = x * x * x;
    printf("%d\n", ans);
    return 0;
}
```

ちなみに、 C++でも`scanf`と`printf`は使えます。
- `iostream`ヘッダの代わりに、`cstdio`というヘッダを`include`します。

```cpp
#include <cstdio>

int main() {
    int x;
    std::scanf("%d", &x);
    std::printf("%d\n", x * x * x);
    return 0;
}
```

## ラーメン

```cpp
#include <iostream>

int main() {
    double a, b, c;
    std::cin >> a >> b >> c;
    double ans = a + b * c;
    std::cout << ans << std::endl;
    return 0;
}
```

小数を扱うには、浮動小数点型である`double`型等を利用します。

$a$ を足すのを忘れないようにしましょう。

おまけですが、小数点以下の出力桁数を決定するには、`iomanip`を`include`して、`std::setprecision()`というものを使います。

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double a, b, c;
    std::cin >> a >> b >> c;
    double ans = a + b * c;
    std::cout << std::fixed << std::setprecision(10);
    std::cout << ans << std::endl;
    return 0;
}
```

例えばこれで`10`桁表示されます。

## Mod

企画開発部プログラミング勉強会伝統の問題です。

```cpp
#include <iostream>

int main() {
    int a, b;
    std::cin >> a >> b;
    int div = a / b;
    int mul = div * b;
    int ans = a - mul;
    std::cout << ans << std::endl;
    return 0;
}
```cpp

整数同士の割り算は小数点以下が切り捨てされることを利用します。

## 力学に備えて

`C++`の問題というより、数学の問題に近かったですね。

$y\ =\ v_0 t + \frac{1}{2}at^2$ の $a$ に $-9.8$ を代入した上で $y = 0$ として $t$ に関する方程式を解きます。

$t = 0, \frac{2v_0}{9.8}$ が導かれ、今回条件に合うのは $t = \frac{2v_0}{g}$ です。

```cpp
#include <iostream>

int main() {
    double m, v0;
    std::cin >> m >> v0;
    double g = 9.8;
    double ans = 2 * v0 / g;
    std::cout << ans << std::endl;
    return 0;
}
```

## 排他的論理和

Google検索等を活用してもらう狙いで作った問題です。例えば、 「C++ 排他的論理和」 と検索すると以下のようなページがヒットします。
- https://learn.microsoft.com/ja-jp/cpp/cpp/bitwise-exclusive-or-operator-hat?view=msvc-170

このページには、 `^` で排他的論理和が計算できると書いており、実際入力例に対して `^`で演算すると出力例と一致する出力がでてきます。

```cpp
#include <iostream>

int main() {
    int a, b;
    std::cin >> a >> b;
    std::cout << (a^b) << std::endl;
    return 0;
}
```

ちなみに、`xor`としても正しいです。

```cpp
#include <iostream>

int main() {
    int a, b;
    std::cin >> a >> b;
    std::cout << (a xor b) << std::endl;
    return 0;
}
```

## Projection

射影は、計算機上で図形を扱う上で非常に重要な知識です。 PandDでのゲーム制作ではこの概念を直接的に扱う機会は無いかもしれないですが....

$p_1, p_2, p, x$ の位置ベクトルを $\vec{P_1}, \vec{P_2}, \vec{P_3}, \vec{X}$ とします。

今回求めたいのは $\vec{X}$ です。

簡潔のため、全体を平行移動して $\vec{P_1} = \vec{O}$ であることとして考えます。

点 $x$ は点 $p_1, p_2$ を通る直線上に存在することから、 ある実数 $k$ が存在して、 $\vec{x} = k(\vec{P_2} - \vec{P_1}) = k\vec{P_2}$ を満たします。 
- つまり、この $k$ が求まれば $x$ は求まったも同然です。

点 $p_1, p_2$ を通る直線と点 $p, x$ を通る直線が直交することに注目します。直交する -> 内積が $0$ なので、

$\vec{Px}\cdot \vec{P_1 P_2} = 0$ です。今までの仮定や式を代入して、

$(k\vec{P_2} - \vec{P}) \cdot \vec{P_2} = 0$ 、よって $k$ について解くと

$k = \frac{\vec{P}\cdot \vec{P_2}}{\mid\mid \vec{P_2}\mid\mid^{2}}$ です。

後はこれを $\vec{x} = k(\vec{P_2} - \vec{P_1}) = k\vec{P_2}$ に代入すれば $\vec{x}$ が求まりました。最初に平行移動していたので、最後に戻すことを忘れずに

```cpp
#include <bits/stdc++.h>

int main() {
    double x1, y1;
    std::cin >> x1 >> y1;
    double x2, y2;
    std::cin >> x2 >> y2;
    double x, y;
    std::cin >> x >> y;

    // 平行移動する
    x2 -= x1;
    y2 -= y1;
    x -= x1;
    y -= y1;

    // kを求める
    double k = (x * x2 + y * y2) / (x2 * x2 + y2 * y2);

    double ansx = k * x2, ansy = k * y2;

    // 平行移動する
    ansx += x1;
    ansy += y1;

    std::cout << ansx << ' ' << ansy << std::endl;
    return 0;
}
```

## for文

```cpp
#include <iostream>

int main() {
    int N;
    std::cin >> N;
    int ans = 0;
    for (int i = 0 ; i < N ; i++) {
        int A;
        std::cin >> A;
        ans += A;
    }
    std::cout << ans << std::endl;
    return 0;
}
```

## if文

```cpp
#include <iostream>

int main() {
    char c;
    std::cin >> c;
    if (c == 'C') {
        std::cout << "C++" << std::endl;
    }
    else {
        std::cout << c << std::endl;
    }
    return 0;
}
```
