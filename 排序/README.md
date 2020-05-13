![](https://github.com/tangshisong/algorithm/blob/master/pic/8.png)
## 插入排序
将一个记录插入到已排好序的有序表中，从而得到一个新的有序表
### 直接插入
```cpp
//直接插入排序
/*算法：每次移除一个元素插入前面已经排序好了的序列*/ 
void insert_sort(int num[],int len)
{
	for(int i = 1;i < len;i++)
	{
		int j;
		int temp = num[i];
		for(j = i-1;j >= 0 && num[j]>temp;j--)
		num[j+1] = num[j];
		num[j+1] = temp;
	}
}
```
### 希尔排序
```cpp
//shell排序
/*算法：改变直接插入的间隔*/ 
void shell_sort(int num[],int len)
{
	for(int gap = len/2;gap > 0;gap/=2)
	for(int i = gap;i < len;i++)
	{
		int j;
		int temp = num[i];
		for(j = i-gap;j>=0 && num[j]>temp;j-=gap)
		num[j+gap] = num[j];
		num[j+gap] = temp;
	}
}
```
## 交换排序

### 冒泡排序
```cpp
//冒泡排序
/*算法：两两比较*/ 
void bubble_sort(int num[],int len)
{
	bool flag = true;
	for(int i = 0;i < len-1&&flag;i++)
	{
	flag = false;
	for(int j = 0;j < len-1-i;j++)
	if(num[j]>num[j+1])
	{
		int temp = num[j];
		num[j] = num[j+1];
		num[j+1] = temp;
		flag = true;
	}
	}	
}
```
### 快速排序
```cpp
//快速排序
/*1找主元:取num[0]/中位数法/随机数法*/ 
/*2分子集*/
/*3递归*/ 
void Swap(int &a,int& b)
{
	int temp = a;
	a = b;
	b = temp;
}

void q_sort(int num[],int left,int right)
{
	//找主元 
	int pivot = num[left];
	int i = left;
	int j = right;
	//递归结束条件 
	if(i > j)  
	return ;
	//元素移动 
	while(i < j)
	{
		while(i<j && num[j]>=pivot) {j--; }//从右往左找到比基准小的元素 
		while(i<j && num[i]<=pivot) {i++; }//从左往右找到比基准大的元素 
		if(i < j) 
		Swap(num[i],num[j]); //交换 
	} 
	//把基准点放入该放入的位置 
	num[left] = num[i];
	num[i] = pivot; 
	//子集划分
	q_sort(num,left,i-1);
	q_sort(num,i+1,right);	
}
void quick_sort(int num[],int len)
{
	q_sort(num,0,len-1);
}
```
## 选择排序

### 简单选择
```cpp
//直接选择排序
/*算法：寻找后面的最小值，交换*/ 
void choose_sort(int num[],int len)
{
	for(int i = 0;i < len-1;i++)
	{
		int j = i ;
		for(int k = i+1;k < len;k++)
		if(num[k] < num[j])
		j = k;
		Swap(num[i],num[j]); 
	}
}
```
### 堆排序
```cpp
//堆排序
/*算法：先建堆，每次取最大堆的第一个元素直到堆空*/ 
//num.1:保持最大堆
void keep_heap(int*num,int size,int i) //从1开始 
{
	int temp = num[i];//当前元素 
	for(int k = 2*i;k <= size;k *= 2) //检查当前元素的子树 
	{
		//比较左右儿子的大小，选择最大的那个结点 
		if(k+1 <= size&&num[k+1] > num[k])
		++k;
		if(num[k] > num[i]) //将儿子结点赋给父结点 
		{
			num[i] = num[k];
			i = k;
		}
		else 
		break;	 
	}
	num[i] = temp;  //找到父节点应该放的位置
}

void heap_sort(int* num,int size)
{
	for(int i = size/2;i > 0;i--)//num.2:建堆
	keep_heap(num,size,i);
	
	for(int i=size ;i > 1;i--)//num.3:排序 
	{
		Swap(num[1],num[i]);
		size--;
		keep_heap(num,size,1);
	} 
}
```
## 归并排序
```cpp
/*归并排序*/  /*外排序的利器*/ 
//递归算法 
/*num为待排数组，temp临时存放数组，left左边起点，right右边起点，rightend右边终点*/ 
void merge(int *num,int *temp,int left,int right,int rightend)//归并
{
	int leftend = right-1;
	int tempbegin = left;//临时存放数组起始位置
	 
	while(left<=leftend&&right<=rightend)//合并两个数组到temp 
	{
		if(num[left]<num[right])
		temp[tempbegin++]=num[left++];
		else
		temp[tempbegin++]=num[right++];
	}
	
	while(left<=leftend)          //若有未完成的则直接放入 
	temp[tempbegin++]=num[left++];
	while(right<=rightend)
	temp[tempbegin++]=num[right++];
	
	for(int i=0;i<=rightend;i++)//将排序完成的数替代原数组 
	num[i]=temp[i];             //迭代算法不需要导入 
}

void msort(int *num,int *temp,int left,int rightend)//分治 
{
	if(left<rightend)//递归出口 
	{
		int center=(left+rightend)/2;//分治 
		msort(num,temp,left,center);
		msort(num,temp,center+1,rightend);
		
		merge(num,temp,left,center+1,rightend);
	}
}
```

## 基数排序
```cpp
#include<iostream>
#define N 10
using namespace std;

int get_max(int* num,int n)
{
	//取得数组的最大值以确定最大base
	int max = num[0];
	for(int i = 1;i < n;++i)
	if(num[i] > max)
	max = num[i];
	return max;
}

void base_sort(int* num,int n,int base)
{
	int temp[n];
	int bucket[10] = {0}; 
	
	//按照base位数字计数 
	for(int i = 0;i < n;++i)
	bucket[(num[i]/base)%10]++;
	
	//计算每个数在整个桶中的绝对位置 
	for(int i = 1;i < 10;++i)
	bucket[i] += bucket[i-1];
	
	//按照每个数的base位放入绝对位置 
	for(int i = n-1;i >= 0;--i)
	{
		temp[bucket[(num[i]/base)%10]-1] = num[i];
		bucket[(num[i]/base)%10]--;
	}
	
	//重新赋值给num 
	for(int i = 0;i < n;++i)
	num[i] = temp[i];
}

void radix_sort(int* num,int n)
{
	int max = get_max(num,n);
	for(int base = 1;max/base > 0;base *= 10)
	base_sort(num,n,base);
}

int main()
{
	int num[10] = {999,822,711,699,115,14,30,211,121,110};
	radix_sort(num,10);
	for(int i = 0;i < 10;++i)
	cout<<num[i]<<" ";
}
```


