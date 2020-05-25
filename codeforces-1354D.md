[题目](https://codeforces.ml/contest/1354/problem/D)

解析：
```c++
First solution: 
write some data structure that would simulate the operations as they are given, 
for example, a segment tree or a Fenwick tree. 
Probably will require optimization since the limits are strict.

Second solution: 
notice that we have to find only one number belonging to the multiset. 
For example, let's find the minimum element. We can do it with binary search as follows: 
let's write a function that, for a given element x, 
tells the number of elements not greater than x in the resulting multiset. 
To implement it, use the fact that all elements ≤x are indistinguishable, 
and all elements >x are indistinguishable too, so the multiset can be maintained with just two counters.

Okay, how does this function help? 
The minimum in the resulting multiset is the minimum x such that this function returns non-zero for it, 
and since the function is monotonous, we can find the answer with binary search.
```

```c++
#include<bits/stdc++.h>

using namespace std;

int n, q;
vector<int> a, k;

int count_le(int x)//计算比x小的元素个数
{
	int cnt = 0;
	for(auto y : a)
		if(y <= x)
			cnt++;
	for(auto y : k)
	{
		if(y > 0 && y <= x)
			cnt++;
		if(y < 0 && abs(y) <= cnt)
			cnt--;
	}
	return cnt;
}
//我们返回的是vector a中最后剩余的最小值
int main()
{
	scanf("%d %d", &n, &q);
	a.resize(n);
	k.resize(q);
	for(int i = 0; i < n; i++)
		scanf("%d", &a[i]);
	for(int i = 0; i < q; i++)
		scanf("%d", &k[i]);
	if(count_le(int(1e9)) == 0)
	{
		puts("0");
		return 0;
	}
	int lf = 0;
	int rg = int(1e6) + 1;
	while(rg - lf > 1)
	{
  //为什么>1而不是>=1
  //因为lf端必然是count_le()==0的，换句话说，没有比lf还小的数存在
  //因为下面if判断中，比mid小的不存在，就让lf=mid，此时比lf小的必然不存在
  //一开始的lf=0，也是这么个意思，类似二分找upper_bound一样让rg=n而不是n-1
		int mid = (lf + rg) / 2;
		if(count_le(mid) > 0)
			rg = mid;
		else
			lf = mid;
	}
	printf("%d\n", rg);
	return 0;
}
```
