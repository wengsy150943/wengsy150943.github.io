---
title: "cf1313c-Skyscrapers-单调栈"
excerpt_separator: "`<!--more-->`"
categories:
  - Test Solve
tags:
  -
header:
  image: /assets/images/header.jpg
---

C. Skyscrapers

The outskirts of the capital are being actively built up in Berland. The company "Kernel Panic" manages the construction of a residential complex of skyscrapers in New Berlskva. All skyscrapers are built along the highway. It is known that the company has already bought n plots along the highway and is preparing to build n skyscrapers, one skyscraper per plot.

Architects must consider several requirements when planning a skyscraper. Firstly, since the land on each plot has different properties, each skyscraper has a limit on the largest number of floors it can have. Secondly, according to the design code of the city, it is unacceptable for a skyscraper to simultaneously have higher skyscrapers both to the left and to the right of it.

Formally, let's number the plots from 1 to n. Then if the skyscraper on the i-th plot has ai floors, it must hold that $a_i$ is at most $m_i (1≤a_i≤m_i)$. Also there mustn't be integers $j$ and $k$ such that $j<i<k$ and $a_j>a_i<a_k$. Plots $j$ and $k$ are not required to be adjacent to $i$.

The company wants the total number of floors in the built skyscrapers to be as large as possible. Help it to choose the number of floors for each skyscraper in an optimal way, i.e. in such a way that all requirements are fulfilled, and among all such construction plans choose any plan with the maximum possible total number of floors.

Input
The first line contains a single integer $n (1≤n≤500000)$ — the number of plots.

The second line contains the integers $m_1,m_2,…,m_n (1≤mi≤109)$ — the limit on the number of floors for every possible number of floors for a skyscraper on each plot.

Output
Print $n$ integers $a_i$ — the number of floors in the plan for each skyscraper, such that all requirements are met, and the total number of floors in all skyscrapers is the maximum possible.

If there are multiple answers possible, print any of them.

Examples
inputCopy

```
5
1 2 3 2 1
```

outputCopy

```
1 2 3 2 1
```

inputCopy

```
3
10 6 8
```

outputCopy

```
10 6 6
```

Note
In the first example, you can build all skyscrapers with the highest possible height.

In the second test example, you cannot give the maximum height to all skyscrapers as this violates the design code restriction. The answer [10,6,6] is optimal. Note that the answer of [6,6,8] also satisfies all restrictions, but is not optimal.

对于一个数组，给定其中每个数的上限，要求构造一个单峰的数组，并使其和最大。
枚举峰顶，然后贪心地取两边就好了。可以用单调栈$O(1)$计算每个数左边和右边的贪心结果，总复杂度是$O(n)$的。

```cpp
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int maxn=5e5+10;
ll sky[maxn],ans[maxn],l[maxn],r[maxn];
int main(){
	int n;
	cin>>n;
	for(int i=1;i<=n;++i){
		scanf("%d",&sky[i]);
	}
	stack<int>ht,pos;//单调栈分别计算一个数左右的情况
	for(int i=1;i<=n;++i){
		while(!ht.empty()&&ht.top()>sky[i])
			ht.pop(),pos.pop();
		int temp(0);
		if(!pos.empty()) temp=pos.top();
		l[i]=l[temp]+(i-temp)*sky[i];
		ht.push(sky[i]);
		pos.push(i);
	}
	while(!ht.empty())
		ht.pop(),pos.pop();
	for(int i=n;i>0;--i){
		while(!ht.empty()&&ht.top()>sky[i])
			ht.pop(),pos.pop();
		int temp(n+1);
		if(!pos.empty()) temp=pos.top();
		r[i]=r[temp]+(temp-i)*sky[i];
		ht.push(sky[i]);
		pos.push(i);
	}



	//贪心构造解
	int l=p-1,r=p+1;
	ll lv,rv;
	ans[p]=sky[p];
	lv=rv=sky[p];
	while(l>0){
		lv=min(lv,sky[l]);
		ans[l]=lv;
		l--;
	}
	while(r<=n){
		rv=min(rv,sky[r]);
		ans[r]=rv;
		r++;
	}
	for(int i=1;i<=n;++i){
		if(i>1) cout<<" ";
		cout<<ans[i];
	}
	cout<<endl;
}
```
