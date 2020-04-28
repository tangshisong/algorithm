## 模板
```cpp
void DFS(para) //参数用来表示状态
{
	if(终点状态)
	{
		...//根据题意添加
		return; 
	}
	if(不合法状态)
	return;
	if(特殊状态) //剪枝 
	return; 
	
	for(扩展方式)
	{
		if(扩展方式所达到的状态合法)
		{
			修改; //根据题目要求添加 
			标记;
			DFS();
			(还原标记);//回溯才采用此步骤 
		}
	}
}
```
## N皇后问题
N\*N的棋盘上放置N个皇后，要求每个皇后不能在同一行、列、对角线 
首先思考终止条件：我们采用逐行放置，如果能走到第N+1行就需要停止了，说明搜索完成找到一个解  
考虑扩展方式：我们在每一行按列扩展  
合法的扩展方式：要求所有皇后不能在同一行（按行扩展就解决了这个问题）、同一列（需要一个数组记录哪些列访问过）、
同一左对角线（有如下性质：处于同一左对角线的元素行列和相等）、同一右对角线（处于同一右对角线的元素行列差的绝对值相等）  
无需要修改操作，需要不断回溯求解故需要还原标记  
```cpp
#include<iostream>
#include<stack>
#include<queue>
#include<vector>
#define N 8 
using namespace std;

int col[2*N+5] = {0};
int ld[2*N+5] = {0};
int rd[2*N+5] = {0};
int ans = 0;
void DFS(int s)
{
	//终止状态
	if(s == N)
	{
		++ans;
		return ;
	}
	
	//扩展方式：按列扩展 
	for(int i = 0;i < N;++i)
	{
		if(!col[i]&&!ld[i+s]&&!rd[s-i+N])//检查扩展方式合法性 
		{
			col[i] = ld[i+s] = rd[s-i+N] = 1; //标记 
			DFS(s+1);   
			col[i] = ld[i+s] = rd[s-i+N] = 0; //搜索结束后还原标记（回溯） 
		}
	}
}
int main()
{
	DFS(0);
	cout<<ans;
}
```
