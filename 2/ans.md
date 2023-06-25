---
layout: default
---

## 第一問 Positive Integer

```cpp
#include <iostream>

int main() {
    int a;
    std::cin >> a;
    if (a > 0) {
        std::cout << "Yay!" << std::endl;
    }
    else {
        std::cout << ":(" << std::endl;
    }

    return 0;
}
```

if文の基本的な文法の理解を問う問題でした。

なお、今回は「非負整数」 $a$ を与えるといっています。なので、 $a$ が $0$ の時しか「:(」と出力しません。よって以下のようにも書けます。

```cpp
#include <iostream>

int main() {
    int a;
    std::cin >> a;
    if (a) {
        std::cout << "Yay!" << std::endl;
    }
    else {
        std::cout << ":(" << std::endl;
    }

    return 0;
}
```

`int`を`bool`に変換する時、 $0$ ならfalse、 $0$ でないならtrueと評価されることを利用しています。


## 第二問

```cpp
#include <iostream>

int main() {
    for (int i = 1 ; i <= 25 ; i++) {
        if (i % 3 == 0) {
            std::cout << "Fizz" << std::endl;
        }
        else {
            std::cout << i << std::endl;
        }
    }
    return 0;
}
```

if文の基本的な文法の理解を問う問題でした。

$3$ の倍数の時だけ `Fizz`が出力されていることに気づきましょう。

## 第三問

```
#include <iostream>

int main() {
    long long v;
    std::cin >> v;
    int ans = 0;
    while (v % 2 == 0) {
        ans++;
        v /= 2;
    }
    std::cout << ans << std::endl;
    return 0;
}
```

問題文にある通り、`int`型よりも絶対値が大きい整数を扱うことができる型をネット検索等で探します。
- 今回は`long long`や`std::int64_t`を利用すると正解できます。

$2$ で割り切れる回数はwhile文を使うと簡単に求まります。

一般にループを回す回数が固定の時はfor文、そうでない時はwhile文を使うことが多そうです。
- 勿論状況によってかわりますが...

## 第四問

```cpp
#include <iostream>

int main() {
  int N;
    std::cin >> N;
    for (int y = 0 ; y < N ; y++) {
        for (int x = 0 ; x < N - y ; x++) {
            std::cout << '#';
        }
        std::cout << std::endl;
    }
    return 0;
}
```
二重ループ

## 第五問

```cpp
#include <iostream>

int main() {
    int N;
    std::cin >> N;
    for (int y = 0 ; y < N ; y++) {
        for (int x = 0 ; x < N ; x++) {
            if (x + y + 1 < N) {
                std::cout << ' ';
            }
            else {
                std::cout << '#';
            }
        }
    }

    return 0;
}
```

企画開発部プログラマ勉強会に代々伝わる難問です。むずかしい....


## おまけ1

```cpp
#include <iostream>

int main() {
    int N;
    std::cin >> N;
    bool ok = true;
    int now = 0;
    for (int i = 0 ; i < N ; i++) {
        char c;
        std::cin >> c;
        if (c == '(') {
            now++;
        }
        else {
            if (now == 0) {
                ok = false;
            }
            now--;
        }
    }
    if (now != 0) {
        ok = false;
    }
    if (ok) {
        std::cout << "Yes" << std::endl;
    }
    else {
        std::cout << "No" << std::endl;
    }
    return 0;
}
```

## 予習1

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
    std::vector<int> B(N);
    for (int i = 0 ; i < N ; i++) {
        B[N - i - 1] = A[i];
    }
    for (int i = 0 ; i < N ; i++) {
        std::cout << B[i];
        if (i + 1 < N) {
            std::cout << ' ';
        }
    }
    std::cout << std::endl;
    return 0;
}
```

別解

algorithmヘッダに引数に与えたイテレータの範囲を反転する`std::reverse`という関数があります。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    int N;
    std::cin >> N;
    std::vector<int> A(N);
    for (int& a : A) {
        std::cin >> a;
    }
    std::reverse(A.begin(), A.end());
    for (int i = 0 ; i < N ; i++) {
        std::cout << A[i];
        if (i + 1 < N) {
            std::cout << ' ';
        }
    }
    std::cout << std::endl;
    return 0;
    
}
```
