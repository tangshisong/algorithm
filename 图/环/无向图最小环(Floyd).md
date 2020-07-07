回忆Floyd三重循环：
```cpp
for(int k = 1;k <= n;++k)
for(int i = 1;i <= n;++i)
for(int j = 1;j <= n;++j)
g[i][j] = g[j][i] = min(g[i][j],g[i][k] + g[k][j])
```
Floyd在于更新到第k个点时，经过1~k-1的点的路径ij一定是最短路径，i点和j点是与k点直接相连，且i < k,j < k，则说明此时
dist[i][j] + g[i][k] + g[k][j]一定是环路      
```cpp
#include <iostream>  
#include <algorithm>  
#include <cmath>  
#include <vector>  
#include <string>  
#include <cstring>  
#include<stack>
#define N 100
#define INF 1e9
using namespace std;

static int g[N][N]; 
static int dist[N][N];
static int path[N][N];//路径 
int ans = INF;
vector<int> ans_path;
 
void floyd(int n)
{
	//1-n
	for(int k = 1;k <= n;++k)
	{
		//枚举直接与k相连的两条边且i和j小于k 
		for(int i = 1;i < k;++i)
		for(int j = i+1;j < k;++j)
		{
			int temp = dist[i][j] + g[i][k] + g[k][j];
			if(temp < ans)
			{
				ans = temp;
				ans_path.clear();
				
				//从j开始一直向i找(目前的环是i->k->j->...->i)
				int t = j;
				while(t != i)
				{
					ans_path.push_back(t);
					t = path[i][t];
				}
				ans_path.push_back(i);
				ans_path.push_back(k);
			}
		}
		
		
		for(int i = 1;i <= n;++i)
		for(int j = 1;j <= n;++j)
		if(dist[i][j] > dist[i][k] + dist[k][j])
		{
			dist[i][j] = dist[i][k] + dist[k][j];
			path[i][j] = path[k][j];
		}
	}
}


int main()
{
	int n = 6;
    for(int i=1; i<=n; ++i)
      for(int j=1; j<=n; ++j)
      dist[i][j]=g[i][j]=INF, path[i][j]=i;
      
	for(int i = 0;i < 7;++i)
	{
		int u,v,w;
		cin>>u>>v>>w;
		g[u][v] = g[v][u] = dist[v][u] = dist[u][v]	= w;
	}
	floyd(6);
	cout<<ans<<endl;
	for(int i = 0;i < ans_path.size();++i)
	cout<<ans_path[i]<<" ";
}
```
