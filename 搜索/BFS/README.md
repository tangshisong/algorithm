## 使用
* 二叉树的BFS
* 图的BFS
* 棋盘的BFS
什么时候使用：    
* 图的遍历
* 简单图的最短路径
## 模板
```cpp
void BFS()
{
	//第一步：创建队列，把起始结点都放到队列里面去（第一层）
	queue<node> q;
	q.push(root);
	
	//第二步：while队列不空，处理队列的结点，并且拓展新结点
	while(!q.empty())
	{
		//for 上一层结点拓展下一层结点 
		int size = q.size();
		for(int i = 0;i < size;++i)
		{
			u = q.front();
			q.pop();
			if(u满足某种条件)
			{
				....
			}
			与u相邻的下一层结点入队 
		}
	}
}
```
