---
title: Bubble Sort
tags: [sorting,C,C++,Python,C#]
---
Bubble Sort is the basic sorting algorithm. In this problem, the input will consists of 2 lines, first line will contain an integer n representing the size of the array to be sorted. The next line will contain n integers representing the contents of the array. The task is to sort the array using bubble sort.
* Time Complexity: **n<sup>2</sup>**
* Memory Complexity: **n**
### Input
```
5
2 3 4 7 1
```

### Output
```
1 2 3 4 7
```

### Implementations
=== "C"
```c
#include<stdio.h>

int main(){
    int n;
    scanf("%d",&n);
    int arr[n];
    for(int i=0;i<n;i++){
        scanf("%d",&arr[i]);
    }
    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if(arr[i]>arr[j]){
                int tmp=arr[i];
                arr[i]=arr[j];
                arr[j]=tmp;
            }
        }
    }
    for(int i=0;i<n;i++){
        printf("%d ",arr[i]);
    }
    printf("\n");
    return 0;
}
```

=== "CPP"
```cpp
#include<iostream>

int main(){
    int n;
    scanf("%d",&n);
    int arr[n];
    for(int i=0;i<n;i++){
        scanf("%d",&arr[i]);
    }
    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if(arr[i]>arr[j]){
                int tmp=arr[i];
                arr[i]=arr[j];
                arr[j]=tmp;
            }
        }
    }
    for(int i=0;i<n;i++){
        printf("%d ",arr[i]);
    }
    printf("\n");
    return 0;
}
```
