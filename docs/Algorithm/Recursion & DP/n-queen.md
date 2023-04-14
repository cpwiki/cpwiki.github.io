---
title: N-Queen Problem
tags: [recursion, backtracking]
---

### Introduction

The n-qeen problem is a puzzle to place **n** number of queens in an **n x n** chessboard. The only rule is that, no two queen to attack each other. The problem can be solved using backtracking.

### Code

```cpp
#include<iostream>
using namespace std;

int taken[10]; // index->col, value->row
int ct = 0; // Count of the valid board orientations

bool valid(int col, int row){
    for(int i=0;i<col;i++){
        if(taken[i]==row||abs(i-col)==abs(taken[i]-row))return false;
    }
    return true;
}

void nQueen(int idx, int n){
    for(int i=0;i<n;i++){
        if(valid(idx,i)){
            taken[idx]=i;
            if(idx==n-1){
                ct++;
                // A valid orientation found & saved in taken array. Do something...

            }
            else nQueen(idx+1,n);
        }
    }
}

int main(){
    int n = 8;
    nQueen(0, n);
    cout<<"Number of valid board orientations: "<<ct<<endl;
    return 0;
}
```

Happy coding!
