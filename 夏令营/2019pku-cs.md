# pku夏令营上机考试150分钟八道题
### AB都是简单的打印题，要注意输出格式！从C题难度起飞......C题是BFS，D题应该是DP
[A.数的字典序](http://bailian.openjudge.cn/xly2019/A/)
```cpp
#include<iostream>
#include<stdio.h>
#include<string.h>
#include<algorithm>
using namespace std;
int main()
{
	int n;
	while(scanf("%d",&n)&&n)
	{
		int x = n,y,c=0;
		while(x)
		{
			y = x%10;
			x /= 10;
			c++;
		}
		
		if(y == 9 || (n>0&&n<9))
		printf("%d\n",n);
		else
		{
			x = 1;
			for(int i = 0;i < c-1;i++)
			x *= 10;
			printf("%d\n",x-1);
		}
	}
}
```
[B.打印日历](http://bailian.openjudge.cn/xly2019/B/)
```cpp
#include<stdio.h>
#include<iostream>
using namespace std;
bool run(int x) //判断是否闰年 
{
	return (x%4 == 0&&x%100 !=0)|| x %400==0;
}
int A[13] = {0,31,28,31,30,31,30,31,31,30,31,30,31};

int main()
{
	int year,month,sum=0;
	scanf("%d %d",&year,&month);
	for(int i = 1900;i < year;i++)
	if(run(i))
	sum += 2;
	else
	sum += 1;
	
	for(int i = 1;i < month;i++)
	if(run(year)&&i==2)
	sum += 29;
	else
	sum += A[i];
	
	int M = A[month];
	if(run(year)&&month==2)
	M = 29;
	
	int day = sum % 7;
	int t = 0;
	 
	printf("Sun Mon Tue Wed Thu Fri Sat\n");
	for(int i = 0;i <= day;i++)
	printf("    "),t++;
	for(int i= 1;i <= M;i++)
	{
		if(i < 10)
		printf("  %d ",i);
		else
		printf(" %d ",i);
		t++;
		if(t == 7)
		t=0,printf("\n");
	}
	
}
```
[C.跳房子](http://bailian.openjudge.cn/xly2019/C/)

[D.上楼梯](http://bailian.openjudge.cn/xly2019/D/)
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<string>
#define ll long long
using namespace std;
ll dp[51];
int main()
{
	int n,k;
	while(scanf("%d %d",&n,&k))
	{
		memset(dp,0,sizeof(dp));
		dp[0] =  1;
		for(int i = 1;i <= n;i++)
		for(int j = 1;j <= min(k,i);j++)
		{
			string s = to_string(j);
			if(s.find("4") == string::npos)
			dp[i] += dp[i-j];
		}
		printf("%d\n",dp[n]);
	}
} 
```
