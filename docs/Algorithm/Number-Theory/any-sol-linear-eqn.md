---
title: Diophantine Equation(Find any Solution)
tags: [diophantine-equation, any-solution, ex-gcd, ax + by = c]
---

### Introduction

ax + by = c is said to be Diophantine Equation of two variables, if the values of x,y are integers.

- It's possible to solve Diophantine Equations with the help of Extended Euclidean Algorithm.
- Time complexity: O(log(min(a,b))).
- Auxiliary memory complexity: O(1).

### Intuition

The following theory will be helpful understanding Diophantine Equations.

- If, d = gcd(a,b) is not a divisor of c, there is "No Solution".
- (a=0, b=0 and c=0), any possible combination of integers can be a solution.
- (a=0, b!=0) or (a!=0, b=0), there is "One Solution".
- (a!=0 and b!=0), there are "Infinately Many Solution".
- If (x<sub>0</sub>,y<sub>0</sub>) is a solution of ax + by = c, all the solutions are:

$$
\left ( x,y \right )=\left (x_{0} + \frac{b}{d}.k, y_{0} - \frac{a}{d}.k \right )
$$

- In Extended Euclidean Algorithm, the equation, ax + by = d is solved where, d = gcd(a,b). The solution can easily be transformed to:

$$
a.x + b.y = d \\
\Rightarrow a\frac{x.c}{d} + b\frac{y.c}{d} = c \\
\Rightarrow a.X + b.Y = c
$$

- Where $X=\frac{x.c}{d}$ and $Y=\frac{y.c}{d}$.

### Code

```cpp
#include<iostream>
using namespace std;
bool anySolution(ll a, ll b, ll c, ll &x0, ll &y0, ll &d)
{
    d = exGcd(abs(a), abs(b), x0, y0);
    if (c % d != 0)
        return false;
    x0 *= (c / d);
    y0 *= (c / d);
    if (a < 0)
        x0 = -x0;
    if (b < 0)
        y0 = -y0;
    return true;
}
```

Happy coding!
