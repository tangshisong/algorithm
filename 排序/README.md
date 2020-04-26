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

### 堆排序

## 归并排序

## 基数排序
