## Floyd求各个顶点之间的最短路（DP）
时间复杂度：O(V^3)，基于点的DP算法，通过中间点不断去更新通过该点的路径      
使用范围：带权图，允许负边但不允许负环
```cpp
void Graph::floyd()
{
	int A[size][size],path[size][size];
	for(int i = 0;i < size;i++)
	for(int j = 0;j < size;j++)
	{
		A[i][j] = edge[i][j];
		if(i == j || edge[i][j] == INF)
		path[i][j] = -1;
		else
		path[i][j] = i;
	}
	
	for(int k = 0;k < size;k++)
	for(int i = 0;i < size;i++)
	for(int j = 0;j < size;j++)
	if(A[i][k]+A[k][j] < A[i][j])
	{
		A[i][j] = A[i][k]+A[k][j];
		path[i][j] = path[k][j];
	}
}
```
