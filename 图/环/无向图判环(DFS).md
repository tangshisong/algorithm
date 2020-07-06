假设u->v->w是环的一部分，u是v的前驱，w是v的后继，如果进行dfs后，筛选到v发现后继w已经被访问了且w不是前驱u，说明有环的存在。   

```cpp
#include <iostream>  
#include <algorithm>  
#include <cmath>  
#include <vector>  
#include <string>  
#include <cstring>  
#define N 100
using namespace std;

vector<vector<int>> g(N);
static bool visited[N] = {false};
bool ans = false;

void add(int u,int v)
{
	g[u].push_back(v);
	g[v].push_back(u);
}

//对于无环图，每个点只有唯一前驱 
//u->v->w
void exit_cycle(int u,int v)
{
	visited[v] = true;
	int size = g[v].size();
	for(int i = 0;i < size;++i)
	{
		int w = g[v][i];
		if(!visited[w])
		exit_cycle(v,w);
		else
		{
			if(w != u)//v的后继结点w已经访问且不是v的前驱u说明有环 
			{
				ans = true;
				break;
			}
		}
	}
}

int main()
{
	int n = 5;
	for(int i = 0;i < n;++i)
	{
		int a,b;
		cin>>a>>b;
		add(a,b);
	}
	for(int i = 0;i < 6;++i)
	if(!visited[i])
	exit_cycle(-1,i); //第一个结点没前驱 
	cout<<ans;
}
```
