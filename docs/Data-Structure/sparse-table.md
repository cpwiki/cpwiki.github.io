---
title: Sparse Table
tags: [sparse-table,range-query]
---
### Introduction
Sparse table is a data structure to answer range queries. Sparse table has the following characterstics,

- Immutable DS, that means no update queries.
- Precalculation time complexity: O(nlogn).
- Auxiliary memory complexity: O(nlogn).
- Per query time complexity for idempotent functions: O(1), for associative functions: O(logn).

### Intuition
The following theory will be helpful understanding sparse table.

- Any non-nagetive number can be uniquely represented as a sum of decreasing power of two. E.g. 13 = (1101)<sub>2</sub> = 8 + 4 + 1.
- Any interval can be uniquely represented as a union of intervels with lengths that are decreasing powers of two. E.g. $[2, 14] = [2, 9] \cup [10, 13] \cup [14, 14]$. Here the interval $[2,14]$ has the length of 13 and the intervals $[2,9], [10,13], [14,14]$ have the length of 8, 4 and 1 accordingly.
- Any interval can be represented as the union of log(length of the interval) number of intervals with lengths that are decreasing powers of two.
- The main idea of sparse table is to precompute all results for range queries with power of two length. Then for each query, the range is splitted into ranges with power of two lengths, get the precomputed results and combine to get the final result.

### Code
```cpp
#include<iostream>
using namespace std;
typedef long long ll;

const ll MXN=5e5;
const ll K=20;
ll n=1e5,k;
ll lg[MXN+5];
ll arr[MXN+5];
ll st[K+5][MXN+5];

void setLog(){
    lg[0]=lg[1]=0;
    for(ll i=2;i<=MXN;i++)lg[i]=lg[i/2]+1;
}

ll func(ll a, ll b){
    //Main operation here
    //ll val=(a<b)?a:b; //Example of an idempotent function
    ll val=a+b; //Example of an associative function
    return val;
}

void build(){
    setLog();
    k=lg[n];
    k++;
    for(ll i=0;i<n;i++)st[0][i]=arr[i];
    for(ll i=1;i<=k;i++){
        for(ll j=0;j+(1<<i)<=n;j++){
            st[i][j]=func(st[i-1][j],st[i-1][j+(1<<(i-1))]);
        }
    }
}

ll query_idemp_func(ll l, ll r){
    ll i=lg[r-l+1];
    ll ans=func(st[i][l],st[i][r-(1<<i)+1]);
    return ans;
}

ll query_assoc_func(ll l, ll r){
    ll ans=0; //base value, value depends on the function
    for(ll i=k;i>=0;i--){
        if((1<<i)<=r-l+1){
            ans=func(ans,st[i][l]);
            l+=(1<<i);
        }
    }
    return ans;
}
```

### Exmaple
A list of numbers and queries or ranges are given. For each query, the result is the minumum value among the numbers between the ranges inclusive. All of them are zero indexed. As input, the following are given:

- First line, a number n, the length of the list of numbers.
- Second line, list of n numbers.
- Third line, a number q, the number of queries.
- The next q lines will two numbers l and r, representing the range [l,r] inclusive.

### Input
```
3
1 4 1
2
1 1
1 2
```

### Output
```
4
1
```

### Code
```cpp
#include<iostream>
using namespace std;
typedef long long ll;

const ll MXN=5e5;
const ll K=20;
ll n=1e5,k;
ll lg[MXN+5];
ll arr[MXN+5];
ll st[K+5][MXN+5];

void setLog(){
    lg[0]=lg[1]=0;
    for(ll i=2;i<=MXN;i++)lg[i]=lg[i/2]+1;
}

ll func(ll a, ll b){
    ll val=(a<b)?a:b;
    return val;
}

void build(){
    setLog();
    k=lg[n];
    k++;
    for(ll i=0;i<n;i++)st[0][i]=arr[i];
    for(ll i=1;i<=k;i++){
        for(ll j=0;j+(1<<i)<=n;j++){
            st[i][j]=func(st[i-1][j],st[i-1][j+(1<<(i-1))]);
        }
    }
}

ll query(ll l, ll r){
    ll i=lg[r-l+1];
    ll ans=func(st[i][l],st[i][r-(1<<i)+1]);
    return ans;
}

int main(){
    cin>>n;
    for(ll i=0;i<n;i++)cin>>arr[i];
    build();
    ll q,l,r;
    cin>>q;
    for(ll i=0;i<q;i++){
        cin>>l>>r;
        ll ans=query(l,r);
        cout<<ans<<endl;
    }
    return 0;
}
```
Happy coding!