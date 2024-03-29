---
layout: default
---

# 演習問題

## 問題1 Dot Product (OO)

長さ $N$ の数列 $A$ $B$ を与えます。 $\displaystyle \sum_{i = 1}^{N} A_i \cdot B_i$ を求めてください

入力形式
```
N
A_1 A_2 ... A_N
B_1 B_2 ... B_N
```

入出力 $1$

```
3
1 2 3
4 5 6
```

```
32
```

入出力 $2$

```
7
1 3 2 4 2 4 1                                                                                                                                                                                              
3 4 5 3 1 3 9
```

```
60
```

入出力 $3$

```
5
0 2 0 2 0
2 0 2 0 2
```

```
0
```
## 問題2 Palindrome (OO)

英小文字からなる文字列 $S$ を与えます。回文か判定してください。

入出力 $1$

```
abdba
```

```
Yes
```

入出力 $2$

```
abda
```

```
No
```

入出力 $3$

```
nolemonnomelon
```

```
Yes
```

入出力 $4$

```
z
```

```
Yes
```

## 問題3 Matrix (OOO)

$N\times M$ 行列 $A$ と $M\times K$ 行列 $B$ を与えます。

行列積 $AB$ を出力してください。

入力形式
```
N M K
A_11 A_12 ... A_1M
A_21 A_22 ... A_2M
...
A_N1 A_N2 ... A_NM
B_11 B_12 ... B_1K
B_21 B_22 ... B_2K
...
B_M1 B_M2 ... B_MK
```


入出力 $1$

```
2 2 2
1 1
1 0
5 2
3 1
```

```
8 3
5 2
```

入出力 $2$

```
1 2 3
1 2
3 4 5
6 7 8
```

```
15 18 21
```


入出力 $3$

```
3 4 1
1 2 0 1
0 3 0 1
4 1 1 0
1
2
3
0
```

```
5
6
9
```
