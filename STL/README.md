# 介绍
STL共有6种组件：容器，容器适配器，迭代器，算法，函数对象和函数适配器。  
# 容器
## 序列容器
每个元素都有固定位置－－取决于插入时机和地点，和元素值无关
### vector
头文件：<vector>，创建一个关于对象T的动态数组类：`vector<T> v`    
特点：随机访问、支持末尾删、末尾增（数组的特性）  
底层实现： vector就是一个动态数组，里面有一个指针指向一片连续的内存空间，当空间不够装下数据时，会自动申请另一片更大的空间（一般是增加当前容量的50%或100%），然后把原来的数据拷贝过去，接着释放原来的那片空间；当释放或者删除里面的数据时，其存储空间不释放，仅仅是清空了里面的数据。**由于原空间被释放，所以以前保留的迭代器失效**。   
1. 增  
v.insert(pos,n,data) 在pos插入n个data，无return  
**v.push_back(data) 在尾部添加**
2. 删
v.erase(pos)  删除pos处的元素，传回下一个元素位置   
v.erase(beg,end)  删除区间[beg,end)   
**v.pop_back() 删除尾部元素**   
3. 改查    
直接使用索引   
4. 其他经常使用的操作  
v.size() 返回元素个数   
v.capacity() 返回容器的容量   
v.empty() 判断容器为空否   
v.back()和v.front() 返回最后一个元素和第一个元素    
v.begin()和v.end()  返回容器的**第一个元素的迭代器和最后一个元素的后面的迭代器**（迭代器可以理解为指针）   
二维数组的定义：**vector<vector<T> > dp(M,vector<T>(N,0))**
### list
头文件：<list>，创建一个关于对象T的双向链表类：`list<T> l`      
特点：支持任意位置删除和插入、不支持随机访问  
底层实现：以结点为单位存放数据，结点的地址在内存中不一定连续，每次插入或删除一个元素，就配置或释放一个元素空间   
### deque
头文件：<deque>，创建一个关于对象T的双端队列类：`deque<T> d`     
和vector类似（随机访问、尾部插入和删除），但是支持在首部快速插入和删除，所以多了两个函数（push_front和pop_front）   
底层实现：deque和vector的最大差异，一在于deque允许于常数时间内对头端进行元素的插入或移除操作，二在于deque没有所谓的capacity观念，因为它是动态地以分段连续空间组合而成，随时可以增加一段新的空间并链接起来。换句话说，像vector那样“因旧空间不足而重新配置一块更大空间，然后复制元素，再释放旧空间”这样的事情在deque中是不会发生的。也因此，**deque没有必要提供所谓的空间预留（reserved）功能**    
## 关联容器
元素位置取决于特定的排序准则，和插入顺序无关
### map
头文件：<map>，创建一个关于对象K和V的红黑树类：`map<K,V> m`  
特点：有序、不允许键重复   
1. 增
通过pair：m.insert(pair<K,V>(key,value));   
通过数组下标：m[key] = value;    
用insert函数插入数据，在数据的插入上涉及到集合的唯一性这个概念，即当map中有这个关键字时，insert操作是插入数据不了的，但是用数组方式就不同了，它可以覆盖以前该关键字对应的值      
实际上，插入操作会返回一个pair对象：pair<map<K,V>::iterator,bool> it，如果插入成功则it.second == true。
2. 删
erase(key)  根据关键字删除   
3. 查  
最好使用count(key)  他会返回对应该键值的元素个数（非1即0）  
size()   键值对个数  
只能使用迭代器遍历 
```cpp
    map<int, string>::iterator iter;   
    for(iter = mapStudent.begin(); iter != mapStudent.end(); iter++)    
       cout<<iter->first<<' '<<iter->second<<endl;  
```
### set
头文件：<set>，创建一个关于值的红黑树类：`set<T> s`  
特点：有序、不允许键重复  

# 容器适配器
包装了现有的STL容器类的模板类，提供了一个不同的、通常更有限制性的功能。
### stack
默认情况下基于deque<T>容器实现向下推栈，即后进先出机制。只能访问最近刚刚进去的对象  
头文件:<stack>，创建：`stack<T> s`   
s.top()  取栈顶  
s.pop()  弹栈  
s.push(data)  压栈   
s.empty()  是否空  
s.size()  大小  
注意stack是不可迭代对象   
### queue
头文件：<queue>，创建：`queue<T> q`
s.front()  取前    
s.back()  取后  
s.pop()  出队   
s.push(data)  入队     
s.empty()  是否空    
s.size()  大小    
### priority_queue 
优先级队列适配器类使用的是矢量容器vector<T>   
