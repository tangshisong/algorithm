## DFS
DFS就是暴力搜索，通过剪枝来优化解空间。其优化解法常常是dp。  
dfs主要是对应多个选择（选与不选的问题），从不同的分支往下搜索。  
## 通用模板
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

## 网格模板
```cpp
int map[N][N],vis[N][N];
int dir[4][2] = {0,1,0,-1,1,0,-1,0};  //方向向量
int check(int x,int y)
{
	if(!vis[x][y]&&...)
	return 1;
	return 0;
}


void dfs(int x,int y)
{
	if(出现某个解)
	{
		处理
		return; 
	}
	
	for(int i = 0;i < 4;++i)
	if(check(x+dir[i][0],y+dir[i][1]))
	{
		vis[x+dir[i][0]][y+dir[i][i]] = 1;
		dfs(x+dir[i][0],y+dir[i][1]);
	}
 } 
```
## 什么时候有for
for循环也是一种选择的体现，比如说一个顶点有很多条分支，这时就可以使用for依次遍历各个分支，然后把这个分支所在的节点作为参数传递到dfs中，进行下一次的深搜。通常图问题（抽象化的）都会采用for  


