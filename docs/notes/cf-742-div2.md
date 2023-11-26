>  是兄弟就一起来上分 ！

<!--more-->

 [`梁佬题解`](https://killtimer0.github.io/) 

###  B

 1. 问题 : 有数组a , 对数组所有的元素进行 `Mex` 和 `Xor` 运算 ，结果分别为 a 和 b , 求 数组 a 的元素最少为多少。
 2. 核心 :
    + 令 ` x = 0 ^ 1 ^ 2 …… ^ a-1 `， 则当` x = b `时 `ans = a`
    + 当 `x != b && x ^ b != a` 时， 我们可以添加 `x^b` , 有 `x ^ b ^ x  = b `, `ans = a + 1`;
    + 当 `x != b && x ^ b == a `时， 我们不能添加 `x^b`, 我们添加 `x ^ b ^ 1` 和 1 ， 有 `x ^ x ^ b ^ 1 ^ 1 = b, ans = a + 2 `;


```c++
#include <iostream>
#include <algorithm>
#include <cstring>
#include <vector>

using namespace std;
const int N = 3e5 + 10;
int w[N];

void Init(){
	for(int i = 1; i < N; ++ i){
		w[i] = w[i-1]^i;
	}
}

int main(){
	int t;
	Init();
	scanf("%d",&t);
	while(t--){
		int a, b;
		scanf("%d%d",&a,&b);
		int cnt = a;
	  	int d = w[a-1]^b;
	  	if(w[a-1]==b){
	  		printf("%d\n", cnt);
	  	}else if(d==a){
	  		printf("%d\n", cnt+2);
	  	}else{
	  		printf("%d\n", cnt+1);
	  	}
	}
	return 0;
}
```




###  C

 1. 问题 : 规定一种加法进位时进到 `下下一位`，给定一个 n , 问有多少对正整数为这种运算的结果 
 2. 核心 :

    + 因为奇数位进位只能进到奇数位，偶数位进位也只能进到偶数位 ，则把数按奇偶位拆成两个数 a, b ，则得到a, b的加法为普通的加法 。

    + 之和为a, b的数对分别为 `a+1, b + 1`, 则最终答案为 `(a+1)*(b+1)-2`， 减去其中一个数为0的两种情况 。





```c++
#include <iostream>

#include <string>

using namespace std;
typedef long long ll;

int main(){
	int t;
	cin >> t;
	while(t--){
		string s;
		cin >> s;
		int a = 0, b = 0;
		for(int i = 0; i < s.size(); ++ i){
			if(i&1){
				a = a*10 + s[i]-'0';
			}
			else{
				b = b*10 + s[i]-'0';
			}
		}
		printf("%lld\n", (a+1)*(b+1)-2);
	}
	return 0;
}
```






###  D

 1. 问题 : 存在 n 个和为 s 的正整数，当把这些数`看为`十一进制表示的数时，得到他们的和，要求当和最大时输出这n个数。
 2. 核心 :

    + 我们发现如果十一进制加法进位会有损失，且高位进位损失比低位进位损失要大，所以我们尽可能不进位或让低位进位 。

    + 我们可以每一次都尽可能地取最大的 $ 10^k$ , 即尽量都有更长的位数 。




```c++
#include <iostream>

using namespace std;

void solve(int s, int n){
	if(n==1){
		printf("%d\n", s);
		return;
	}
	int p = 1;
	while(p*10<s) p *= 10;   // 
	while(s-p<n-1) p /= 10;  // 核心为这两个循环，作用是挖出符合条件的最大的10^k
	printf("%d ", p);
	solve(s-p, n-1);
}

int main(){
	int t;
	scanf("%d", &t);
	while(t--){
		int s, n;
		cin >> s >> n;
		if(s<n){
			printf("0\n");
			continue;
		}
		solve(s, n);
	}
	return 0;
}
```

###  E 

1. 问题描述，给定一个长度为n的序列 a ，有以下两种操作：
   + ` 1 x y  `  表示将 $a_x$ 修改为 `y`
   + `2 l r`  表示询问区间 `[ l , r ]` 上的连续非递减序列个数，其中单个数也算一个非递减序列 
2. 解决 : 典型线段树题型  

**分析** 

我们考虑 : 

​	要维护节点的答案(连续非递减序列个数)，左右节点需要存储什么信息，有以下几种情况：

- 当`tr[2*u].rv > tr[2*u+1].lv`时，`tr[u].ans = tr[2*u] .ans + tr[2*u+1].ans `
- 当`tr[2*u].rv <= tr[2*u+1].lv`时，`tr[u].ans = tr[2*u].ans + tr[2*u+1].ans + tr[2*u].suffix * tr[2*u+1].prefix `  , 其中 prefix 和 suffix 分别存储序列的`前缀和后缀最大连续非递减序列个数` 




!!!note "提示"
    那为什么要写两个Push_up()呢？ 第一个Push_up()为了更新树中原本的区间，
    而第二个为了便于合并并更新查询时的区间，在数中原本不存在这样一个完整的区间。



**完整代码**


```c++
#include <bits/stdc++.h>

using namespace std;
const int N = 2e5 + 10;
typedef long long ll;
int a[N];

struct node{
	int l, r;
	int lv, rv;
	ll suf, pre, ans;
}tr[4*N];

typedef struct node Node; 

// 更新为关键d 
void Push_up(int u){
    tr[u].lv = tr[2*u].lv, tr[u].rv = tr[2*u+1].rv;
    tr[u].pre = ((tr[2*u].pre==(tr[2*u].r-tr[2*u].l+1))&&(tr[2*u].rv<=tr[2*u+1].lv))?tr[2*u].pre+tr[2*u+1].pre:tr[2*u].pre;
	tr[u].suf = ((tr[2*u+1].suf==(tr[2*u+1].r-tr[2*u+1].l+1))&&(tr[2*u+1].lv>=tr[2*u].rv))?tr[2*u+1].suf+tr[2*u].suf:tr[2*u+1].suf;
	tr[u].ans = tr[2*u].ans + tr[2*u+1].ans;
	if(tr[2*u].rv <= tr[2*u+1].lv){
		tr[u].ans += tr[2*u].suf * tr[2*u+1].pre;
	}
}

void Push_up(Node &u, Node &L, Node &R){
	u.l = L.l, u.r = R.r, u.lv = L.lv, u.rv = R.rv;  
	u.pre = ((L.pre==(L.r-L.l+1))&&(L.rv<=R.lv))?L.pre+R.pre:L.pre;
	u.suf = ((R.suf==(R.r-R.l+1))&&(R.lv>=L.rv))?R.suf+L.suf:R.suf;
	u.ans = L.ans + R.ans;
	if(L.rv <= R.lv){
		u.ans += L.suf * R.pre;
	}
}

void Build(int u, int l, int r){
	if(l==r) tr[u] = {l, l, a[l], a[l], 1, 1, 1};
	else{
    	tr[u].l = l, tr[u].r = r, tr[u].lv = a[l], tr[u].rv = a[r];  // 此处易忘 ！
		int mid = (l+r)/2;
		Build(2*u, l, mid), Build(2*u+1, mid+1, r);
		Push_up(u);
	}
}

Node Query(int u, int l, int r){
	if(tr[u].l==l && tr[u].r==r){ 
	    //cout << "-- 找到子区间" << l << '~' << r << endl;  // Debug 的好地方 
	    return tr[u];
	}else{
		int mid = (tr[u].l+tr[u].r)/2;
		if(r<=mid) return Query(2*u, l, min(r, mid));
		if(l>mid) return Query(2*u+1, max(mid+1, l), r);
		else{
			Node res, left, right;
			left = Query(2*u, l, mid);
			right = Query(2*u+1, mid+1, r);
			Push_up(res, left, right);
			return res;
		}
	}
}

void Modify(int u, int th, int x){
	if(tr[u].l==th&&tr[u].r==th){
		tr[u].lv = tr[u].rv = x;
	}else{
		int mid = (tr[u].l+tr[u].r)/2;
		if(th<=mid) Modify(2*u, th, x);
		else Modify(2*u+1,th, x);
		Push_up(u);
	}
}

int main(){
	int n, m;
	scanf("%d%d", &n, &m);
	for(int i = 1; i <= n; ++ i) scanf("%d", &a[i]);
	Build(1, 1, n);
	while(m--){
		int k, p, q;
		scanf("%d%d%d", &k, &p, &q);
		if(k==1){
			Modify(1, p, q);
		}else{
			printf("%lld\n", Query(1,p,q).ans);
		}
	}
	return 0;
}
```




[**线段树单点修改**](https://wyh-de-house.top/2021/10/01/Segment-tree-1/#more) 