## dijkstra求单源最短路（贪心）
时间复杂度：O(V^2)，算法是基于点划分的，与边无关。   
思想：将点根据是否访问划分为两组，然后选出dist最小的点且未被访问过，作为新的松弛点   
不允许存在负边。   
```cpp
void Graph::dijkstra(int point)
{
	int* dist = new int[size];
	int* path = new int[size];
	int* collect = new int[size];
	for(int k = 0;k < size;k++)
	{
		dist[k] = INF;
		path[k] = -1;
		collect[k] = 0;
	}
	dist[point] = 0;
	collect[point] = 1;
	int i = point;
	
	for(int k = 0;k < size-1;k++)
	{
		for(int j = 0;j < size;j++)
    //三角不等式
		if(G[i][j]&&!collect[j]&&dist[i] + edge[i][j] < dist[j])//松弛
		{
			dist[j] = dist[i] + edge[i][j];
			path[j] = i;
		}
		
		//确定下一个要访问的点（选择dist最小的那个点） 
		int min = INF;
		for(int s = 0;s < size;s++)
		if(!collect[s]&&dist[s] < min)
		{
			min = dist[s];
			i = s;
		}
		collect[i] = 1;
	}
	
	for(int i = 0;i < size;i++)
	cout<<dist[i]<<"  ";
	delete [] dist;
	delete [] path;
	delete [] collect; 
}
```
