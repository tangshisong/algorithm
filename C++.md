复习c/c++的基本知识
# 目录
* [程序的内存分配](#程序的内存分配)
* [const](#const)
* [static](#static)
* [new/delete和malloc/free](#new/delete和malloc/free)
* [strlen和sizof](#strlen和sizof)
* [输入与输出](#输入与输出)
* [this](#this)

### 程序的内存分配
一个c++程序占用的内存结构：  
* 栈区：由编译器自动分配与释放，存放为运行时函数分配的局部变量、函数参数、返回数据、返回地址等。
* 堆区：由程序员自动分配，如果程序员没有释放，程序结束时可能有OS回收。其分配类似于链表。
* 全局区：存放全局变量、静态变量（全局静态变量和局部静态变量）、常量。程序结束后由系统释放。全局区分为已初始化全局区（data）和未初始化全局区（bss）。
* 常量区：存放常量字符串，程序结束后有系统释放。
* 代码区

### const
基本作用：  
1. 修饰变量：变量不可变  
```cpp
const int x = 1  //x不可变
const A a  //常对象只能调用常成员
```
与#define的区别：  
* 处理阶段不同：#define是预编译指令，在预编译阶段进行替换；const在编译/运行处理，需要分配内存  
* 类型检查不同：#define只是进行简单的替换；const有具体类型，需要进行检查
* 存储方式不同：#define不分配内存；const需要  
* 有的调试工具不能对#define调试，可以对const调试  

2. 修饰指针：（1）指向常量的指针 （2）常量指针  
指针是变量，存放变量的地址；引用是别名，不占用内存空间。指针可以为空，引用必须在声明的时候初始化且不能为空。  
```cpp
char test[] = "test";
char* p1 = test;  //变量指针指向字符数组变量
const char* p2 = test;  //变量指针指向字符数组常量
char* const p3 = test;  //常量指针指向字符数组变量
const char* const p4 = test;  //常量指针指向字符数组常量
```
3. 修饰引用：指向常量的引用  
```cpp
const A a;
const A& q = a;  //指向常对象的引用
```
4. 修饰成员函数：可以用于对重载函数的区分，成员函数不能修改成员变量  

### static
1. 修饰普通变量  
（1）静态局部变量  
在函数体的内部，不会随着函数的结束而被销毁，程序结束才被销毁，存在于常量区，在整个程序周期只能被赋值一次。  
（2）静态全局变量  
定义在函数体外，用于修饰全局变量，表示该变量只在本文件可见。而别的全局变量可以对其他文件可见。  
2. 修饰普通函数  
和静态全局变量作用一样，只能对本文件可见。  
3. 修饰成员变量  
即类变量，属于类本身，该类的所有对象共享。
4. 修饰成员函数  
即类方法，可以访问静态成员函数和静态成员变量，不能访问非静态的。  

### new/delete和malloc/free
* 语言定义不同：new/delete是操作符，malloc/free是库函数  
* 申请位置不同：new是在自由存储区分配，malloc是在堆区分配
* 返回类型不同：new分配成功会返回对象的指针，malloc分配成功会返回void*（需要进行强制类型转换）
* 异常结果不同：new分配失败会抛出异常，malloc分配失败会返回NULL
* 计算内存不同：new是编译器自动计算所需内存大小，malloc需要程序指定字节数（sizeof）
* 执行过程不同：new先调用malloc然后调用构造函数，delete先调用析构函数然后调用free
```cpp
int* p1 = new int;  //动态定义一个变量
int* p2 = new int(1);  //定义一个变量并初始化为1
int* p3 = new int[1];   //定义一个数组大小为1
delete p1;
delete [] p3;
```

### strlen和sizof
* strlen是函数，计算字符串在'\0'之前的字符长度
* sizof是运算符，计算字符串所占的字节数

### ++i和i++
++i直接自增返回，i++需要定义一个临时变量然后再自增再返回，++i的效率更高
```cpp
++i    
  INT   INT::operator++()   
  {   
          *this=*this+1;   
          return   *this;   
  }   
i++   
const INT INT::operator  ++(int)   
  {   
            INT   oldvalue=*this;   
            *this=*this+1;   
            return   oldvalue   
  } 
```

### 输入与输出
最好使用c的输入与输出，效率更高。  
1. C的输入与输出
```cpp
int a;
scanf("%d",&a); //接收正确的输入返回1
long long a;
scanf("%lld", &a);

float a;
scanf("%f",&a);
double a;
scanf("%lf",&a);

char s[10];
scanf("%s",s);//读到非空白字符后，若再次遇到空白字符，结束字符串的输入
```
2. C++的输入与输出
```cpp
int a;
cin>>a;
string s;
cin>>s;

cout<<a<<endl;
```
3. c的文件输入输出
```cpp
#include<cstdio>
FILE *fin,*fout;
fin = fopen("data.in","r");
fout = fopen("data.out","w");
while(fscanf(fin,"%d",&x))
{
fprintf(fout,"%d",x);
}
fclose(fin);
fclose(fout);
}
```

### this
this指针：指向调用该成员函数的对象，是一个隐含于每一个非静态成员函数的指针  
当对一个对象调用成员函数时，编译程序先将对象的地址赋给 this 指针，然后调用成员函数，每次成员函数存取数据成员时，都隐式使用this指针。
当一个成员函数被调用时，自动向它传递一个隐含的参数，该参数是一个指向这个成员函数所在的对象的指针。   
this 并不是一个常规变量，而是个右值，所以不能取得 this 的地址（不能 &this）  

### struct和typedef struct
1. C
```cpp
typedef struct student{int x;}stu;
stu S1;   //stu相当于struct student的别名
struct student{int x;}；
struct student S1;
```
2. C++
```cpp
struct student{int x;};
student S1;//直接用即可，无需写关键字struct
```
struct和class的区别：默认的继承访问权限。struct 是 public 的，class 是 private 的。  



