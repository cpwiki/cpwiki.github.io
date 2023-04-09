---
title: Cycle Finding
tags: [cycle-finding, graph, ditected, undirected]
---

### Introduction

Cycle can be exist in directed and undirected graph. Cycle in a graph can be detected as following,

- Using DFS.
- If back-edge exists, there is a cycle.
- Back-edge is an edge connecting the node with some of it's ansestor.
- Three values of the color array,
  - 0, the node is not visited yet.
  - 1, the node is in the DFS tree and an ancestor of the current node.
  - 2, visited, not an ancestor.
- Initial value of parent array is -1, which means the node have no parent.
- parent[v] = u, means u is the direct parent of v.
- Time Complexity: **O(m)**, where m is the number of edges.

### Code

```cpp
#include<iostream>
#include<vector>
using namespace std;

vector<vector<int>>adj;
vector<int>parent;
vector<int>color;
int cycle_start;
int cycle_end;

void init(int len){
    adj.assign(len,vector<int>());
    parent.assign(len,-1);
    color.assign(len,0);
    cycle_start = -1;
    cycle_end = -1;
}

bool cycleDfs(int u){
    color[u]=1;
    for(int v:adj[u]){
        if(color[v]==0){
            parent[v]=u;
            if(cycleDfs(v))return true;
        }else{
            //Undirected Graph
            if(v==parent[u])continue;

            //Directed Graph
            //if(color[v]==2)continue;

            //Common
            cycle_end = u;
            cycle_start = v;
            return true;
        }
    }
    color[u]=2;
    return false;
}

vector<int>getCycle(){
    vector<int>cycle;
    if(cycle_start!=-1){
        cycle.push_back(cycle_start);
        for(int v = cycle_end; v!=cycle_start; v = parent[v]){
            cycle.push_back(v);
        }
        cycle.push_back(cycle_start);
        reverse(cycle.begin(),cycle.end());
    }
    return cycle;
}


```

Happy coding!
