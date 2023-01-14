---
title: Sorting Algorithms
tags: [sorting,C,C++,Python,C#]
---
# Sorting Algorithms

1. Bubble Sort
2. Insertion Sort
3. Merge Sort
4. Tim Sort
5. Counting Sort

### Bubble Sort

* Time Complexity: **O(n<sup>2</sup>)**
* Auxiliary Space: **O(1)**

```cpp
void bubble_sort( int *arr, int l, int r ) {
    for ( int i = l; i <= r; i++ ) {
        for ( int j = i + 1; j <= r; j++ ) {
            if ( arr[i] > arr[j] ) {
                int tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
            }
        }
    }
}
```

### Insertion Sort

* Time Complexity: **O(n<sup>2</sup>)**
* Auxiliary Space: **O(1)**

```cpp
void insertion_sort( int *arr, int l, int r ) {
    for ( int i = l; i <= r ; i++ ) {
        int key = arr[i];
        int j = i-1;
        while( j >= l && arr[j] > key ) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### Merge Sort

* Time Complexity: **O(nlogn)**
* Auxiliary Space: **O(n)**

```cpp
void merge ( int *arr, int l, int mid, int r ) {
    int len_left = mid - l + 1;
    int len_right = r - mid;
    auto left = new int[len_left];
    auto right = new int[len_right];
    for ( int i = 0; i < len_left; i++ ) left[i] = arr[l + i];
    for ( int i = 0; i <len_right; i++ ) right[i] = arr[mid + i + 1];
    int idx_left = 0, idx_right = 0, idx_arr = l;
    while ( idx_left < len_left && idx_right < len_right ) {
        if ( left[idx_left] <= right[idx_right] ) {
            arr[idx_arr] = left[idx_left];
            idx_left++;
        }
        else{
            arr[idx_arr] = right[idx_right];
            idx_right++;
        }
        idx_arr++;
    }
    while ( idx_left < len_left ) {
        arr[idx_arr] = left[idx_left];
        idx_left++;
        idx_arr++;
    }
    while ( idx_right < len_right ) {
        arr[idx_arr] = right[idx_right];
        idx_right++;
        idx_arr++;
    }
    delete[] left;
    delete[] right;
}

void merge_sort( int *arr, int l, int r ) {
    if ( l < r ){
        int mid = l + (r - l) / 2;
        merge_sort(arr, l, mid);
        merge_sort(arr, mid+1, r);
        merge(arr, l, mid, r);
    }
}
```

### Tim Sort

* Time Complexity: **O(nlogn)**
* Auxiliary Space: **O(n)**

```cpp
int min ( int a, int b ) {
    return a < b ? a : b;
}

void tim_sort ( int *arr, int l, int r ) {
    int run = 32;
    int len = r - l + 1;
    for ( int i = l; i <= r; i += run ){
        insertion_sort( arr, i, min ( i + run - 1, r ) );
    }
    for ( int siz = run; siz < len; siz = 2 * siz ){
        for ( int left = l; left <= r; left += 2 * siz ) {
            int mid = left + siz - 1;
            int right = min ( left + 2 * siz - 1, r );
            if ( mid < right ){
                merge ( arr, left, mid, right );
            }
        }
    }
}
```

### Counting Sort

* Time Complexity: **O(n+k)**
* Auxiliary Space: **O(n+k)**

Where, k is the difference of maximum and minimum of all values in the array

```cpp
void max ( int a, int b ) {
    return a > b ? a : b;
}

void counting_sort ( int *arr, int l, int r ) {
    int min_val = arr[l];
    int max_val = arr[l];
    int len = r - l + 1;
    for ( int i=l; i <= r; i++ ) {
        min_val = min ( min_val, arr[i] );
        max_val = max ( max_val, arr[i] );
    }
    int dif = max_val - min_val + 1;
    int cnt[dif + 1];
    for ( int i = 0; i <= dif; i++ ) cnt[i] = 0;
    for ( int i = l; i<= r; i++ ) {
        int idx = arr[i] - min_val;
        cnt[idx]++;
    }
    for ( int i = 1; i<= dif; i++ ) {
        cnt[i] += cnt[i-1];
    }
    for( int i = 0; i <= dif; i++ ) {
        while( cnt[i] ){
            arr[cnt[i] - 1] = i + min_val;
            cnt[i]--;
        }
    }
}
```
Happy Coding!