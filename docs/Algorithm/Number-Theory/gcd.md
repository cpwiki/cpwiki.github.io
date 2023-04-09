---
title: Euclidean Algorithm(GCD)
tags: [gcd, euclidean]
---

### Introduction

Greatest Common Divisors(GCD) of two integers a,b is the largest integer d which can divide both of the integers a,b.

- If b=0, gcd(a,b) = a.
- gcd(a,b) = gcd(b,a%b).
- Time complexity: O(log(min(a,b))).
- Auxiliary memory complexity: O(1).

### Code

```cpp
#include<iostream>
using namespace std;

int gcd( int a, int b ){
    if(b==0) return a;
    return gcd(b,a%b);
}
```

Happy coding!
