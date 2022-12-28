---
title: Count Subarray Having XOR Value of K
tags: [Array,XOR,Cumulative Sum]
---
### Problem Statement
Given an array of integers A[] and a number K. The task is to count the number of subarrays the following conditions are true,

- A[] is an array of size n.
- \[A<sub>i</sub>...A<sub>j</sub>\] is a subarray of A[] where, (0 <= i,j < n).
- (A<sub>i</sub>^A<sub>i+1</sub>^...^A<sub>j-1</sub>^A<sub>j</sub>) = K, where ^ represents the XOR operation.

### Input
```
n = 3, A[] = {4, 2, 2, 6, 4}, K = 6

```

### Output
```
Ans: 4
```

### Basics
- (a XOR 0) = a, where a is a variable.
- (a XOR a) = 0, XOR of same value is 0.
- (a XOR b XOR a) = b.
- if (a XOR b) = k, than (a XOR k) = b.

### Solution
We know that the total number of subarrays of an array of size n is, (n<sup>2</sup> + n) / 2. So, if we want to calculate XOR values of each subarray individually, the complexity of the calculation will be atleast O(n<sup>2</sup>). In this case we can reduce the complexity to O(n) with the help of cumulative sum concept. Although we will use XOR instad of sum actually. Let's see how and why will it work.<br>
First of all we are creating an array Q[] of size n. Where Q[i] will contain the XOR value of, [A<sub>0</sub>...A<sub>i</sub>], where (0 <= i < n). The follwing steps are followed to achive that,

- Q[0] = A[0].
- Q[i] = Q[i-1] ^ A[i], where (1 <= i < n).

So, here we can see that,

- Q[p] = (A<sub>0</sub>^A<sub>1</sub>^...^A<sub>p</sub>).
- Q[q] = (A<sub>0</sub>^A<sub>1</sub>^...^A<sub>q</sub>).
- Q[p]^Q[q] = (A<sub>p+1</sub>^...^A<sub>q</sub>), where (p < q) and the value is 0, when (p = q).

With the help of the array Q[], we can easily calculate the XOR of any subarray of A[] with O(1) time complexity.<br>
Now, let [A<sub>p+1</sub>...A<sub>q</sub>] is a subarray where the XOR value is K. So, from the above discussion, we can say that,

- Q[p]^Q[q] = K.
- Q[p]^K = Q[q], [From the basics section].
- Q[p]^k = val, [Let, Q[q] = val].

If we find the XOR of each value Q[p] in Q[] with K. We will get another value val. We have to calculate the total number of occueance of val in the array Q[] and add the number of occuerance to the ans. We can use counters to keep the occurence of each values in Q to avoid the complexity of counting each time.<br>
Also, it's very important to remember that, we are literally counting twice each value(just think how?). To avoid counting twice, we can count only the values in the indexes less than the current index while iterating from 0 to n-1.

### Code
```cpp
#include<iostream>
using namespace std;

int solve (int *A, int n, int K) {
    int Q[n+5];
    int mx = 0;
    for (int i = 0; i<n; i++) {
        if(i == 0) Q[i] = A[i];
        else Q[i] = Q[i-1] ^ A[i];
        mx = (A[i] > mx) ? A[i] : mx;
    }
    mx *= 2;
    int cnt[mx+5];
    for (int i = 0; i < mx + 5; i++) cnt[i] = 0;
    cnt[0] = 1;
    int ans = 0;
    for(int i = 0; i < n; i++) {
        int val = Q[i] ^ K;
        if (val < mx + 5) {
            ans += cnt[val];
        }
        cnt[Q[i]]++;
    }
    return ans;
}

int main() {
    int n = 5;
    int A[] = {4, 2, 2, 6, 4};
    int K = 6;
    int ans = solve (A, n, K);
    cout<<"Ans: "<<ans<<endl;
}
```
Happy Coding!