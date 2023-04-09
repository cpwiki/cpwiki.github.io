---
title: Extended Euclidean Algorithm
tags: [ex-gcd, "ax + by = gcd(a,b)"]
---

### Introduction

Extended Euclidean Algorithm is the extended version of Euclidean algorithm which have the ability to find the GCD of two integers a,b. Additionally it can solve the following equation:

```
a*x + b*y = gcd(a, b)
```

- Time complexity: O(log(min(a,b))).
- Auxiliary memory complexity: O(1).

### Intuition

Extended Euclidean Algorithm is the application of Bezout's Identity. Which is, for a!=0 and b!=0, d=gcd(a,b), there exist integers x and y such as:

```
a*x + b*y = gcd(a, b)
```

- It can find the value of x, y and gcd(a, b).
- If b=0, then x = 1, y = 0 and gcd = a.
- Else,

$$
  \left\{\begin{matrix}
  x_{i} = y_{i+1}\\
  y_{i} = x_{i+1} - \begin{Bmatrix}
  y_{i+1}*\left ( \left \lfloor \frac{a_{i}}{b_{i}} \right \rfloor \right )
  \end{Bmatrix}
  \end{matrix}\right.
$$

- Following table is showing the values of each steps to find the GCD of a=102, b=38 and the values of x,y in the equation, a\*x + b\*y = gcd(a,b)

| <h3><b>i</b></h3> | <h3><b>a</b></h3> | <h3><b>b</b></h3> | <h3><b>(a / b)</b></h3> | <h3><b>(a % b)</b></h3> | <h3><b>x</b></h3> | <h3><b>y</b></h3> |
| :---------------: | :---------------: | :---------------: | :---------------------: | :---------------------: | :---------------: | :---------------: |
|         0         |        102        |        38         |            2            |           26            |     3 (**X**)     |    -8 (**Y**)     |
|         1         |        38         |        26         |            1            |           12            |        -2         |         3         |
|         2         |        26         |        12         |            2            |            2            |         1         |        -2         |
|         3         |        12         |         2         |            6            |            0            |         0         |         1         |
|         4         |    2 (**GCD**)    |         0         |            -            |            -            |         1         |         0         |

### Code

```cpp
#include<iostream>
using namespace std;

int exGcd( int a, int b, int& x0, int& y0 ) {
    if( b == 0 ) {
        x0 = 1;
        y0 = 0;
        return a;
    }
    int x1, y1;
    int d = exGcd( b, a % b, x1, y1 );
    x0 = y1;
    y0 = x1 - y1 * ( a / b );
    return d;
}
```

Happy coding!
