---
title: Policy-Based Data Structure(PBDS)
tags: [ordered_set, ordered_map]
---

### Introduction

PBDS provide some additional data structures not available in STL in C++.

- PBDS provide "ordered_set", "ordered_map" etc.
- "ordered_set" and "ordered_map" have the similar functionality of "std::set" and "std::map".
- Both of them have some additional functionalities like indexed access and fast iteration.
- Time Complexity of most functionalities: **O(lon(n))**.

### Ordered Set

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>

using namespace __gnu_pbds;

typedef tree<
int,
null_type,
less<int>,
rb_tree_tag,
tree_order_statistics_node_update>
ordered_set;

//Use less_equal<int> instad of less<int> for ordered-multiset

int main(){
    ordered_set oss;

    //insert value
    oss.insert(b);

    //get the size
    ll len=oss.size();

    //get index of value
    ll pos=oss.order_of_key(val);

    //get value of the index
    ll val=*oss.find_by_order(pos);

    //erase value by position
    oss.erase(oss.find_by_order(pos));

    //find and delete value
    ll pos=oss.order_of_key(a);
	ll val=*oss.find_by_order(pos);
	if(a==val)oss.erase(oss.find_by_order(pos));

    return 0;
}
```

### Ordered Map

```cpp
#include <iostream>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>

using namespace std;
using namespace __gnu_pbds;

template <typename K, typename V>
using ordered_map = tree<K, V, less<K>, rb_tree_tag, tree_order_statistics_node_update>;

int main() {
    ordered_map<int, int> omap;

    // insert key-value pairs
    omap.insert({3, 30});
    omap.insert({1, 10});
    omap.insert({4, 40});
    omap.insert({2, 20});

    // get the size
    cout << "Size of map: " << omap.size() << endl;

    // access value of a key
    cout << "Value of key 2: " << omap[2] << endl;

    // erase a key-value pair by key
    omap.erase(3);

    // find and erase a key-value pair by key
    auto it = omap.find(2);
    if (it != omap.end()) omap.erase(it);

    // check if a key exists
    cout << "Key 4 exists: " << (omap.find(4) != omap.end()) << endl;

    // get the index of a key
    cout << "Index of key 1: " << omap.order_of_key(1) << endl;

    // get the key at a particular index
    cout << "Key at index 2: " << (*omap.find_by_order(2)).first << endl;

    // get the value at a particular index
    cout << "Value at index 2: " << (*omap.find_by_order(2)).second << endl;

    // clear the map
    omap.clear();

    return 0;
}
```

Happy coding!
