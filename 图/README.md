## 基本概念
1. 分类    
有向图、无向图、简单图（无重边、无自环）、多重图、完全图（无向图有n(n-1)/2条边、有向图有n(n-1)条边)  
2. 连通分量  
连通：两个顶点之间有路径可达  
连通图：无向图的任意两个顶点连通  
连通分量：无向图的极大连通子图  
强连通图：有向图的任意两个点都连通  
强连通分量：有向图的极大连通子图  
3. 度  
无向图的度 = 2\*边数 有向图的入度 = 有向图的出度 = 边数  
4. 存储  
（1）邻接矩阵（适用于稠密图）  
空间复杂度：O（V^2）  
A[i][j] = 1/0（有边为1，无边为0）  
无向图：无向图的邻接矩阵是对称矩阵，第i个点的度为第i行/列的非零元素的个数，O（1）时间确定点i和j是否有边相连  
有向图：非对称矩阵，第i个点的出度为第i行的非零元素的个数，第i个点的入度为第i列的非零元素的个数  
（2）邻接表（适用于稀疏图）  
无向图：O（V+2E） 有向图：O（V+E）  
计算两个点是否有边以及一个点的出度需要遍历邻接链表  
计算一个点的入度需要遍历整个邻接表  

## 深度优先遍历DFS
访问v之后，寻找v未被访问的邻居访问，递归进行，类似二叉树的先序遍历   
空间复杂度：O（V）递归调用栈  
邻接矩阵的时间复杂度：O（V^2) 邻接表的时间复杂度：O（V+E）  
```cpp
#include<iostream>
#include<stack>
#include<queue>
#include<vector>
#define N 5
using namespace std;

int A[N][N] = {0};
int visit[N] = {0};
void DFS_re(int start)
{
	cout<<start;
	visit[start] = 1;
	
	for(int i = 0;i < N;++i)
	if(!visit[i]&&A[start][i])
	DFS_re(i);
}
void DFS(int start)
{
	stack<int> s;
	s.push(start);
	
	while(!s.empty())
	{
		int i = s.top();
		s.pop();

		if(!visit[i])
		{
			cout<<i;
			visit[i] = 1;			
			for(int j = 0;j < N;++j)
			if(!visit[j]&&A[i][j])
			s.push(j);			
		}

	}
}
```
## 广度优先遍历BFS
访问v之后，访问v所有未被访问的邻居，之后从邻居继续该操作，类似二叉树的层次遍历  
```cpp
//把DFS的栈改为队列即可
void BFS(int start)
{
	queue<int> q;
	q.push(start);
	
	while(!q.empty())
	{
		int i = q.front();
		q.pop();

		if(!visit[i])
		{
			cout<<i;
			visit[i] = 1;			
			for(int j = 0;j < N;++j)
			if(!visit[j]&&A[i][j])
			q.push(j);			
		}

	}
}
```


