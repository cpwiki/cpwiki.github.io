---
title: Line by Line Input C++
tags: [istringstream,C++,]
---

### Code
```cpp
string line;
getline(cin, line);
istringstream is(line);
int n;
while(is >> n){
    //do something with n
}
```
Happy Coding!