---
title: Longest Palindromic Subsequence
tags: [dynamic-programming, two-pointer]
---

### Problem

A string of lowercase english letters will be given. The task is to find the length of the longest palindromic subsequence of the string.

### Solution

The solution steps are simple as following:

- f(l,r) is a function which returns the length of the longest palindromic subsequence of the substring (s[l]...s[r]).
- Initiate l as the first index(0) and r as the last index(s.size()-1) of s.
- f(l,r) will return the following:
  	- l=r, return 1.
  	- l>r, return 0.
  	- s[l]=s[r], return 2+f(l+1,r-1).
  	- else, return max(f(l+1,r), f(l,r-1)).
- f(l,r) will be saved in dp[l][r] to avoid calculation again.

### Code

```cpp
#include<iostream>
using namespace std;

int dp[1010][1010];

int ctDP(int l, int r, string& s){
	if(l==r)return 1;
	if(l>r)return 0;
	if(dp[l][r]!=-1)return dp[l][r];
	if(s[l]==s[r]) dp[l][r] = 2 + ctDP(l+1,r-1,s);
	else dp[l][r] = max(ctDP(l+1,r,s),ctDP(l,r-1,s));
	return dp[l][r];
}

int main(){
    for(int i=0;i<1010;i++){
		for(int j=0;j<1010;j++)dp[i][j]=-1;
	}
	string s = "bbbab";
	int l=0, r=s.size()-1;
	int ans = ctDP(l,r,s);
	cout<<ans<<endl;
    return 0;
}
```

Happy coding!
