## BFS求无权图的最短路（搜索）
从源点向外扩散，时间复杂度：O(V^2)   
```cpp
void Graph::shortpath(int point)
{
	int* path = new int[size];
	int* dist = new int[size];
	for(int k = 0;k < size;k++)
	path[k] = dist[k] = -1;
	
	queue<int> q;
	q.push(point);
	dist[point] = 0;
	
	while(!q.empty())
	{
		int i = q.front();
		q.pop();
		
		for(int j = 0;j < size;j++)
		if(A[i][j] && dist[j] == -1)
		{
			q.push(j);
			dist[j] = dist[i] + 1;
			path[j] = i;
		}
	}
	delete [] path;
	delete [] dist;
}
```
