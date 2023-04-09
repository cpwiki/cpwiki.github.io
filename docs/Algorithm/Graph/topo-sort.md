---
title: Topological Sort
tags: [topological-sort, graph, ditected, acyclic]
---

### Introduction

Topological Sort is ordering the nodes of an acyclic graph such a way that, the full graph can be visited with minimul number of dfs calls all over again.

- Graph should be directed.
- Graph should not contain any cycle.
- Dfs is used.
- Time Complexity: **O(m)**, where m is the number of edges.

### Code

```cpp
#include<iostream>
#include<vector>
using namespace std;

vector<vector<int>>adj;
vector<bool>visited;
vector<int>sorted;

void init(int len){
    adj.assign(len,vector<int>());
    visited.assign(len,false);
    sorted.clear();
}

void sortDfs(int s){
    visited[s]=true;
    for(int v:adj[s]){
        if(!visited[v])sortDfs(v);
    }
    sorted.push_back(s);
}

void topological_sort(int l, int r){
    for(int i=l;i<=r;i++){
        if(!visited[i])sortDfs(i);
    }
    reverse(sorted.begin(),sorted.end());
}
```

Happy coding!
