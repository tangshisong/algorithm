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
N\*N的棋盘上放置N个皇后，要求每个皇后不能在同一行、列、对角线，输出解的个数和字典序解   
首先思考终止条件：我们采用逐行放置，如果能走到第N+1行就需要停止了，说明搜索完成找到一个解  
考虑扩展方式：我们在每一行按列扩展  
合法的扩展方式：要求所有皇后不能在同一行（按行扩展就解决了这个问题）、同一列（需要一个数组记录哪些列访问过）、
同一左对角线（有如下性质：处于同一左对角线的元素行列和相等）、同一右对角线（处于同一右对角线的元素行列差的绝对值相等）  
无需要修改操作，需要不断回溯求解故需要还原标记  
```cpp
#include<iostream>
#include<vector>
#define N 8
using namespace std;

int col[2*N+5] = {0};
int ld[2*N+5] = {0};
int rd[2*N+5] = {0};
int ans = 0;
void DFS(int s,vector<int>& vec)
{
	//终止状态
	if(s == N)
	{
		++ans;
		for(int i = 0;i < N;++i)
		cout<<vec[i]+1<<" ";
		cout<<endl;
		return ;
	}
	
	//扩展方式：按列扩展 
	for(int i = 0;i < N;++i)
	{
		if(!col[i]&&!ld[i+s]&&!rd[s-i+N])//检查扩展方式合法性 
		{
			col[i] = ld[i+s] = rd[s-i+N] = 1; //标记
			vec.push_back(i);
			DFS(s+1,vec);   
			col[i] = ld[i+s] = rd[s-i+N] = 0; //搜索结束后还原标记（回溯）
			vec.pop_back(); 
		}
	}
}
int main()
{
	vector<int> vec;
	DFS(0,vec);
	cout<<ans;
}
```
## 黑白皇后问题
在N皇后的基础上加了一个皇后：要求黑皇后不能在同一行、列、对角线，白皇后不能在同一行、列、对角线，输出解的个数和字典序解  
解法：两次DFS，先对黑皇后DFS再对白皇后DFS  
终止条件：两个皇后都处理完并且黑白皇后都到达第N+1行  
特殊条件：对黑皇后DFS完后就对白皇后DFS  
扩展方式：按列扩展  
扩展方式的合法性：（1）题目给定棋盘，1代表该位置可放，0代表不可放（2）判断列、左右对角线可否放置：用0代表黑白皇后都可放置，
1代表黑皇后不能放置，2代表白皇后不能放置，3代表黑白皇后都不能放置  
```cpp
#include<iostream>
#include<stack>
#include<queue>
#include<vector>
#define N 4
using namespace std;

int map[N][N]; //根据题目给定的棋盘来做 
int col[2*N+5] = {0};
int ld[2*N+5] = {0};
int rd[2*N+5] = {0};
int ans = 0;

void DFS(int s,int p,vector<int>& vec)
{
	//终止条件：两个皇后都放置完成 
	if(s == N&&p == 2)
	{
		++ans;
		for(int i = 0;i < N;++i)
		cout<<vec[i]+1<<" ";
		cout<<endl;
		for(int i = N;i < 2*N;++i)
		cout<<vec[i]+1<<" ";
		cout<<endl;
		return;
	}
	//特殊条件：黑皇后放置完成开始放白皇后 
	if(s == N)
	{
		DFS(0,2,vec);
	}
	//按列扩展
	for(int i = 0;i < N;++i)
	{
		if(map[s][i] && col[i] != 3 && col[i] != p &&
		ld[i+s] != 3 && ld[i+s] != p &&
		rd[i-s+N] != 3 && rd[i-s+N] != p)
		{
			map[s][i] = 0;
			col[i] += p;
			ld[i+s] += p;
			rd[i-s+N] += p;
			vec.push_back(i);
			DFS(s+1,p,vec);
			map[s][i] = 1;
			col[i] -= p;
			ld[i+s] -= p;
			rd[i-s+N] -= p;
			vec.pop_back();		
		}
	} 
}

int main()
{
	vector<int> vec; 
	for(int i = 0;i < N;++i)
	for(int j = 0;j < N;++j)
	map[i][j] = 1;
	DFS(0,1,vec);
	cout<<ans;
}
```

## 9\*9数独游戏
终止条件：我们采取按行列搜索，那么当到达第N+1行，搜索结束  
特殊状态：当列到达N+1时，需要换行：DFS(x+1,0);当前行列的元素已经存在需要跳过：DFS(x,y+1)  
扩展方式：按1-9的数字扩展（按内容扩展）    
扩展方式的合法性：同一行、列、3\*3矩阵不能存在相同数字，所以此时我们需要三个数组记录1-9数字的占用情况
```cpp
#include<iostream>
#include<vector>
#define N 9
using namespace std;
bool k = false;
int ans = 0;
int map[N][N];//s输入 
int row[N+1][N+1],col[N+1][N+1],mat[N+1][N+1];//第i行/列/矩阵的每个数字的占用情况 
void DFS(int x,int y)
{
	if(k) //游戏有很多种解法我们只需要得到其中一种即可（字典序第一个） 
	return;
	if(x == N)
	{
		k = true;
		for(int i = 0;i < N;++i)
		{
			for(int j = 0;j < N;++j)
			cout<<map[i][j]<<" ";
			cout<<endl;
		}
		return ;
	}
	if(y == N)
	{
		DFS(x+1,0);
		return ;
	}
	if(map[x][y] != 0)//未被占用
	{
		DFS(x,y+1);
		return ;
	}
	
	for(int i = 1;i <= N;++i)//按内容扩展
	{
		if(!row[x][i]&&!col[y][i]&&!mat[x/3*3+y/3][i])
		{
			map[x][y] = i;
			row[x][i] = 1;
			col[y][i] = 1;
			mat[x/3*3+y/3][i] = 1;
			DFS(x,y+1);
			map[x][y] = 0;
			row[x][i] = 0;
			col[y][i] = 0;
			mat[x/3*3+y/3][i] = 0;
		}
	} 
} 

int main()
{
	for(int i = 0;i <= N;++i)
	for(int j = 0;j <= N;++j)
	row[i][j] = col[i][j] = mat[i][j] = 0;
	
	for(int i = 0;i < N;++i)
	for(int j = 0;j < N;++j)
	{
		scanf("%d",&map[i][j]);
		if(map[i][j])
		{
			row[i][map[i][j]] = 1;
			col[j][map[i][j]] = 1;
			mat[i/3*3+j/3][map[i][j]] = 1;
		}
	}
	DFS(0,0);
}
0 2 6 0 0 0 0 0 0
0 0 0 5 0 2 0 0 4
0 0 0 1 0 0 0 0 7
0 3 0 0 2 0 1 8 0
0 0 0 3 0 9 0 0 0
0 5 4 0 1 0 0 7 0
5 0 0 0 0 1 0 0 0
6 0 0 9 0 7 0 0 0
0 0 0 0 0 0 7 5 0
```

