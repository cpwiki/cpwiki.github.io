---
title: Maximum Sum of K Positive Numbers from N Stacks
tags: [dynamic-programming, dimension-reduction]
---

### Problem

There are n number of stacks of positive numbers are given. The task is to take k numbers from the stacks, so that the summation of the taken numbers is maximized.

- From a stack, only the top item can be taken. After removing the top item, the next item get to the top.

### Solution
- Traverse the stacks from left or right.
- Take as much numbers as we want or allowed (posibly zero) from that stack and move forward, don't come back.
- Keep the maximum value at each state.
- Memorize to avoid recalculation.

### Code

```cpp
#include<bits/stdc++.h>
using namespace std;

int dp[1010][2010]; //memorization
int n; // will keep the number of stacks
vector<vector<int>>stacks; // stacks

void init(){
	for(int i=0;i<10101;i++){
		for(int j=0;j<2010;j++)dp[i][j]=-1;
	}
}

int ctDP(int idx, int k){
	if(idx>=n||k<=0)return 0;
	if(dp[idx][k]!=-1)return dp[idx][k];
	int m=stacks[idx].size();
	int sum=0;
	for(int i=0;i<=min(m,k);i++){
		if(i!=0)sum+=stacks[idx][i-1];
		dp[idx][k]=max(dp[idx][k],sum+ctDP(idx+1,k-i));
	}
	return dp[idx][k];
}

int main(){
	//load_input(); //load stacks
	n = stacks.size();
	init();
	int ans=ctDP(0,k);
	cout<<ans<<endl;
	return 0;
}
```

Happy coding!
