---
title: Bubble Sort
tags: [sorting,C,C++,Python,C#]
---
Bubble Sort is the basic sorting algorithm. In this problem, the input will consists of 2 lines, first line will contain an integer n representing the size of the array to be sorted. The next line will contain n integers representing the contents of the array. The task is to sort the array using bubble sort.

* Time Complexity: **O(n<sup>2</sup>)**
* Memory Complexity: **O(n)**
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

    void bubble_sort(int n, int *arr){
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if(arr[i]>arr[j]){
                    int tmp=arr[i];
                    arr[i]=arr[j];
                    arr[j]=tmp;
                }
            }
        }
    }

    int main(){
        int n;
        scanf("%d",&n);
        int arr[n];
        for(int i=0;i<n;i++){
            scanf("%d",&arr[i]);
        }
        bubble_sort(n,arr);
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
    using namespace std;

    void bubble_sort(int n, int *arr){
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if(arr[i]>arr[j]){
                    int tmp=arr[i];
                    arr[i]=arr[j];
                    arr[j]=tmp;
                }
            }
        }
    }

    int main(){
        int n;
        cin>>n;
        int arr[n];
        for(int i=0;i<n;i++){
            cin>>arr[i];
        }
        bubble_sort(n,arr);
        for(int i=0;i<n;i++){
            cout<<arr[i]<<" ";
        }
        cout<<endl;
        return 0;
    }
    ```

=== "C#"
    ```csharp
    using System;

    namespace Sorting{
        class Sorter{
            static void bubble_sort(int[] arr){
                int n = arr.Length;
                for(int i=0;i<n;i++){
                    for(int j=i+1;j<n;j++){
                        if(arr[i]>arr[j]){
                            int tmp=arr[i];
                            arr[i]=arr[j];
                            arr[j]=tmp;
                        }
                    }
                }
            }

            public static void Main(string[] args){
                int n = Convert.ToInt32(Console.ReadLine());
                int[] arr = Array.ConvertAll(Console.ReadLine().Trim().Split(' '),Convert.ToInt32);
                bubble_sort(arr);
                for(int i=0;i<n;i++){
                    Console.Write(arr[i]+" ");
                }
                Console.WriteLine();
            }
        }
    }
    ```

=== "Python"
    ```python
    def bubble_sort(arr):
        n=len(arr)
        for i in range(0,n):
            for j in range(i+1,n):
                if arr[i]>arr[j]:
                    tmp=arr[i]
                    arr[i]=arr[j]
                    arr[j]=tmp

    if __name__ == "__main__":
        n=int(input())
        arr=input().split(' ')
        arr=[int(val) for val in arr]
        bubble_sort(arr)
        for num in arr:
            print(num, end=" ")
        print("\n")
    ```
