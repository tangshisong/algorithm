## 从亿级数据中寻找最大的K个数（TopK）
### 方案一：最小堆
建立容量为K的最小堆，先放入K个数据初始化堆（O（K）），对于剩余的N-K个数据，每次来和堆顶比较，如果比堆顶小就丢弃，比堆顶大就占用堆顶，
重新调整堆，调整完所有数据（（N-K）logK）。故当N远远大于K时，`时间复杂度为O（NlogK）`。所`占用的空间为K个单元`，即此方法不需要足够大的内存。  

### 方案二：快速排序
时间复杂度：O（n）但是快排要求所有数据加载到内存中，故对于特别特别巨大的数据可以考虑分块后再分别使用快排之后综合所有块的topk再使用快排
```cpp
#include<iostream>
#include<vector>
using namespace std;
void swap(int& x,int& y)
{
	x = x + y;
	y = x - y;
	x = x - y;
}
int q_select(int* num,int left,int right) //划分
{
	int pivot = num[left];
	int i = left;
	int j = right;
	if(i > j)
	return i;
	
	while(i < j)
	{
		while(i < j && num[j] <= pivot) --j;
		while(i < j && num[i] >= pivot) ++i;
		if(i < j)
		swap(num[i],num[j]);
	}
	num[left] = num[i];
	num[i] = pivot;
	return i;
}

void topk(int* num,int n,int k)
{
	int i = 0,j = n-1;
	int idx = q_select(num,i,j);
	while(idx != k-1)
	{
		if(idx < k-1) //看右序列
		{
			i = idx + 1;
			idx = q_select(num,i,j);
		}
		else  //看左序列
		{
			j = idx - 1;
			idx = q_select(num,i,j);
		}
	}
	
	for(int i = 0;i < k;++i) //前k个数为答案
	cout<<num[i]<<" ";
	cout<<endl;
}

int main()
{
	int num[] = {1,0,88,0,1,8888,4,5,1,3,345,5,23,999999,2,55,3,21,32,34,23,-11};
	topk(num,22,13);
}
```
