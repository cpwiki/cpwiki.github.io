---
title: K-th Permutation of Sequence 1 to n
tags: [divide-and-conquer]
---

### Problem

There is an array of sequence [1,...,n] given. We have to find the permutation of the k-th permutation of the array.

### Solution

We are going to divide this problem into smaller problems. We will try to solve, what is the first number of the k-th permutation of an array. Then the solution of the main problem will be found recursively.

- Array with n items have n! number of pernutations.
- Each value in the array will appare in the fist position for the permutation for (n-1)! times continuously and follow the assending order.
- The first (n-1)! permutations will contain smallest value at the first index, (n-1)! permutations after that will contain second smallest value at the first index and so on.
- Array={1,2,3}, n!=6, (n-1)!=2, k=3(0-indexed), permutations are:
	- {1,2,3}
	- {1,3,2}
	- {2,1,3}
	- {2,3,1} (Target Permutation)
	- {3,1,2}
	- {3,2,1}
- idx=k/(n-1)!=3/2=1. Value in the index-1 in the Array is: 2. So 2 will be places in the first index (index-0) in our target permutation **{2,\_,\_}**.
- k=k%(n-1)!=3%2=1, as we are done with one position, so we can reduce the value of k, so that it will remain in the range of the count of permutations on Array size smaller by one position.
- 2 will be removed as we can't use it again, Array={1,3}.
- n=2, n!=2, (n-1)!=1, k=1, idx=1/1=1, Value in the index-1 in the current Array is: 3. So, 3 will be places in the second index in our target permutation **{2,3,\_}**.
- k=1%1=0, Array={1}, n=1, So the remaining value will be placed in the remaining index of out permutation **{2,3,1}**.

### Code

```cpp
#include<bits/stdc++.h>
using namespace std;

#include<ext/pb_ds/assoc_container.hpp>
#include<ext/pb_ds/tree_policy.hpp>

using namespace __gnu_pbds;

//For set functionality, indexed access and faster delete opperation
typedef tree<
int,
null_type,
less<int>,
rb_tree_tag,
tree_order_statistics_node_update>
ordered_set;

vector<int> kthPermutation(int n, int k){
	//k--;//if k is 1-indexed
	vector<int>permutation;

	ordered_set oss;
    for(int i=1;i<=n;i++)oss.insert(i);

	//Value of n!
	int fact = 1;
	for(int i=2;i<=n;i++){
		fact*=i;
	}
	for(int i=n;i>0;i--){
		fact/=i; // Value of (n-1)!
		int idx = (i==1)? 0 : (k/fact);
		k %= fact;
		int val=*oss.find_by_order(idx);
		permtation.push_back(val);
		oss.erase(oss.find_by_order(idx));
	}
	return permutation; 
}

int main(){
    int n=3;
	int k=3; //0-indexed
	vector<int>permutation = kthPermutation(n,k);
	for(int i=0;i<n;i++){
		cout<<permutation[i]<<" ";
	}
	cout<<endl;
}
```

Happy coding!
