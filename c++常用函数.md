# c++常用函数

## max( )

```c++
头文件#include <algorithm>
using namespace std;
max（ ， ）
```



## strlen( )

头文件：<cstring>
格式：strlen（字符数组名）
功能：仅计算**字符串s**的（unsigned int型）长度，不包括’\0’在内，**char[i] == ‘\0’是字符串结束的标志**
说明：返回s的长度，不包括结束符NULL

```c++
实例
#include <iostream>
#include <cstring>
int main(void)
{
    char s[] = "Golden Global View";
    std:: cout << s << " has " << strlen(s) << " chars";
    return 0;
}
// Golden Global View has 18 chars
```

```c++
使用strlen时一定要注意是否赋值
char aa[10];cout<<strlen(aa)<<endl; //结果是不定的
char aa[10]={'\0'}; cout<<strlen(aa)<<endl; //结果为0
char aa[10]="jun"; cout<<strlen(aa)<<endl; //结果为3
```



## malloc( )

头文件#include<malloc.h>

malloc内的参数是需要<font color='red'>动态分配的字节数</font>

malloc 函数返回的是 void * 类型，必须通过 (type *) 来强制转换

malloc（）是动态内存分配函数，用来向系统请求分配内存空间。当无法知道内存具体的位置时，想要绑定真正的内存空间，就要用到malloc（）函数。因为malloc只管分配内存空间，并不能对分配的空间进行初始化，所以申请到的内存中的值是随机的，经常会使用memset()进行置0操作后再使用。　　

与其配套的是free（），当申请到的空间不再使用时，要用free（）函数将内存空间释放掉，这样可以提高资源利用率，最重要的是----就是因为它可以申请内存空间，然后根据需要进行释放，才被称为“动态内存分配”!

```c++
type *var_name = (type*)malloc(sizeof(type)*num);
```

```c++
int *p;
p = (int*)malloc(sizeof(int) * 128);
//分配128个整型存储单元，并将这128个连续的整型存储单元的首地址存储到指针变量p中
double *pd = (double*)malloc(sizeof(double) * 12);　　
//分配12个double型存储单元，并将首地址存储到指针变量pd中
free(p);
free(pd);
p = NULL;
pd = NULL;　　
指针用完赋值NULL是一个很好的习惯。
内存泄漏一般是指程序申请了一块内存，使用完后，没有及时将这块内存释放，从而导致程序占用大量内存。
```





## memset( )

头文件#include<cstring>

memset 函数是内存赋值函数，用来给某一块内存空间进行赋值的。 其原型是：void* memset(void *_Dst, int _Val, size_t _Size)_——————sizeof(数组名)

Dst是目标起始地址，_Val是要赋的值，_Size是要赋值的字节数。

memset是逐字节拷贝的，给char以外的数组赋值时，只能初始化为0或者-1

- 1、可以使用memset函数对char类型数组的元素进行赋值（0值或非0值）。
- 2、可以使用memset函数对非char类型数组的元素进行赋0值或-1，但不能使用memset函数直接对非char类型数组的元素赋非0值。这里的非char类型数组，是指数据类型大小不是1个字节的，比如short、int、long、占用字节数大于1个字节的结构体等。

```c++
memset(a,0,sizeof(a));
```



## 常用sort( )

**头文件：**

```c++
#include <algorithm>
using namespace std;
```

**基本使用办法**

sort()函数可以对给定区间所有元素进行排序。它有三个参数<font color='red'>sort(begin, end, cmp)</font>，其中begin为指向待sort()的数组的<font color='red'>第一个元素的指针</font>，end为指向待sort()的数组的<font color='red'>最后一个元素的下一个位置的指针</font>，cmp参数为排序准则，cmp参数<font color='red'>可以不写（即为sort（begin, end））</font>，**默认从小到大进行排序**。如果我们想从大到小排序可以将cmp参数写为greater<int>()就是对int数组进行排序，当然<>中我们也可以写double、long、float等等。

如果我们需要按照其他的排序准则，那么就需要我们自己定义一个bool类型的函数来传入:

升序：第一个参数小于第二个该函数,返回true。
降序：第一个参数大于第二个该函数,返回true。

**对一个整型数组进行从大到小排序：**

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int main(){
	int num[10] = {6,5,9,1,2,8,7,3,4,0};
	sort(num,num+10,greater<int>());
	for(int i=0;i<10;i++){
		cout<<num[i]<<" ";
	}//输出结果:9 8 7 6 5 4 3 2 1 0
	
	return 0;
	
} 
```

**自定义排序准则**

```c++
//按照每个数的个位进行从大到小排序
#include<iostream>
#include<algorithm>
using namespace std;

bool cmp(int x,int y){
	return x % 10 > y % 10;
}

int main(){
	int num[10] = {65,59,96,13,21,80,72,33,44,99};
	sort(num,num+10,cmp);
	for(int i=0;i<10;i++){
		cout<<num[i]<<" ";
	}//输出结果：59 99 96 65 44 13 33 72 21 80
	
	return 0;
	
} 
```

**对结构体进行排序**

```c++
#include<iostream>
#include<string>
#include<algorithm>
using namespace std;

struct Student{
	string name;
	int score;
	Student() {}
	Student(string n,int s):name(n),score(s) {}
};

bool cmp_score(Student x,Student y){
	return x.score > y.score;
}

int main(){
	Student stu[3];
	string n;
	int s;
	for(int i=0;i<3;i++){
		cin>>n>>s;
		stu[i] = Student(n,s);
	}
	
	sort(stu,stu+3,cmp_score);
	
	for(int i=0;i<3;i++){
		cout<<stu[i].name<<" "<<stu[i].score<<endl;
	}
	
	return 0;
}
```



## qsort( )

头文件#include<cstdlib>

“比较函数”的原型应是：int 函数名(const void * elem1, const void * elem2)

/*参数列表是两个空指针，现在他要去指向你的数组元素。所以转型为你当前的类型，然后取值。

升序排列时：

若第一个参数指针指向的“值”**大于**第二个参数指针指向的“值”，则返回正；
若第一个参数指针指向的“值”**等于**第二个参数指针指向的“值”，则返回零；
若第一个参数指针指向的“值”**小于**第二个参数指针指向的“值”，则返回负。

降序排列时，则刚好相反。

*/

```c++
用法示例：
#include<cstdlib>
int cmpfunc (const void * a, const void * b) {
   return *(int *)a - *(int *)b;//升序排序
   return *(int *)b - *(int *)a; //降序排序
}
qsort(nums, numsSize, sizeof(int), cmpfunc);//写在需要进行排序操作的函数里
```



## 位运算

标准运算符，不用头文件

转换为二进制后，对每一位进行运算，生成新的数

& 与

```c++
2的幂：若 n = 2^x，恒有 (n > 0) && (n & (n - 1)) == 0
4的幂：若 n = 4^x，恒有 (n > 0) && (n & (n - 1)) == 0 && (n & 0xAAAAAAAA) ==0
- n二进制最高位为 1，其余所有位为 0；
- n - 1二进制最高位为 0，其余所有位为 1；
```

| 或

~ 非

^ 异或

\>> 右移，相当于除2

<< 左移，相当于乘2





## calloc

头文件#include<cstdlib>

分配所需的内存空间，并返回一个指向它的指针。**malloc** 和 **calloc** 之间的不同点是，malloc 不会设置内存为零，而 calloc 会设置分配的内存为零。

不需要memset置0，calloc = malloc+memset ，但是推荐calloc

```c++
 void *calloc(size_t nitems, size_t size)
 nitems -- 要被分配的元素个数。
 size -- 元素的大小。
 a = (int*)calloc(n, sizeof(int));
例：int *arr = (int *) calloc(10, sizeof(int))
```



## NULL 和 nullptr

C++11版本中新加入nullptr，解决NULL表示空指针在C++中具有二义性

如：ListNode* l1 = nullptr

c 和 c++ 对比阐述

```c
c语言中NULL为空指针
#define NULL ((void *)0)
int  *pi = NULL;
char *pc = NULL;
C语言中把空指针赋给int和char指针的时候，发生了隐式类型转换，把void指针转换成了相应类型的指针。
C语言中，void 类型的变量可以赋值给任意类型的指针，void也可以被任意类型的指针赋值，两个方向都不会报错。    
```

```c++
C++是强类型语言，void*是不能隐式转换成其他类型的指针的
#ifdef __cplusplus
#define NULL 0                 NULL为0
#else
#define NULL ((void *)0)       用作空指针可能是为了兼容C，迫于无奈
#endif
C++具有更严格的类型检查，void 类型的变量不能赋值给任意类型的指针，但void可以被任意类型的指针赋值(void* 是万能指针)。    
```

**总结**

c++中 NULL为0 ，nullptr为空指针

没有c++11如何解决？

```c++
const class nullptr_t
{
public:
    template<class T>
    inline operator T*() const
        { return 0; }
 
    template<class C, class T>
    inline operator T C::*() const
        { return 0; }
 
private:
void operator&() const;
} nullptr = {};
```



## push_back( )

- push_back() 在Vector最后添加一个元素（参数为要插入的值），位置为当前最后一个元素的下一个元素

  ```c++
  //在vec尾部添加10
  vector<int> vec;
  vec.push_back(10);
  ```

  

- 在string的最后插入一个字符

  ```c++
  string str;
  str.push_back('d');
  ```

  

## reverse( )

实现翻转数组，字符串，向量

std :: reverse反转了[first，**last**）范围内的元素

注意last是开区间，所以尾部要比需要反转的最后一个元素地址**大1**（数组）

1、翻转数组

```c++
//头文件
#include <algorithm>
//使用方法
reverse(a, a+n);//n为数组中的元素个数
a为指针首地址，a+k为数组第k+1个元素的地址，a+n为数组第n+1的地址
```

2、翻转字符串

```c++
//头文件
#include <algorithm>
//用法为
reverse(str.begin(), str.end());
```

3、翻转向量

```c++
//头文件
#include <algorithm>
//用法
reverse(vec.begin(), vec.end());
```



## swap( )

```c++
该函数在 <algorithm> 头文件中声明。
交换位置
swap(a, b);
```



## uhash——哈希函数（T217）

uhash以宏的方式定义了对哈希函数的操作函数

```c++
#include "uthash.h"
struct hashTable {
    int id;                    /* key */
    UT_hash_handle hh;         /* makes this structure hashable */
};
struct hashTable *users = NULL;    /* important! initialize to NULL */
```



## abs( )

求绝对值函数

头文件#include<cmath>

c++中 abs() 可以支持整数、浮点数和复数的求绝对值运算

```c++
整型：
int abs(int i)  //返回整型参数i的绝对值 

复数（complex）：
double cabs(struct complex znum)  //返回复数znum的绝对值  

双精度浮点型：
double fabs(double x)  //返回双精度参数x的绝对值  

长整型：
long labs(long n)  //返回长整型参数n的绝对值 
```



## pow( )函数

```c++
#include<cmath> //必要头文件
pow(x,y); //x的y次方
一般来说的正确用法是pow(int,double)
如：pow(2,2.0)
```



## 增强for循环

```c++
for(声明语句 : 表达式)
{
   //代码句子
   //声明语句：声明新的局部变量，与数组元素的类型匹配，用作输出或传值
   //表达式：访问的数组名
}
例：for (char ch: s)
```



## cctype函数

**#include<cctype>//头文件**

**isalnum( )**

```c++
判断一个字符是否是字母或者（十进制）数字，若为字母或者数字，则返回True(非0值)，否者返回False(0)
isalnum (c)
#include<cctype>//头文件
```

**isalpha( )**

```c++
判断参数“c”是否是一个字母。如果是字母，返回true，否则返回false。返回true的范围正则可表示为：[a-z，A-Z]。
isalpha (c);
```

**isblank( )**

```c++
isblank()将空白字符视为制表符(“ \ t”)和空格字符(“”)。
检查字符c是否为空白字符。空白字符是用于分隔文本行内的单词的空格字符。如果是，则返回true；如果不是，则返回false。
空格字符的ascii值是32.空格字符用正则表达式为：\s
isblank (c);
```

**isspace( )**

```c++
isspace()考虑空格字符：('')-空格，('\ t')-水平制表符，('\ n')-换行符，('\ v')-垂直制表符，('\ f')-提要，( '\ r')-回车
如果是，则返回true；如果不是，则返回false。
isspace(c);
```

**isdigit( )**

```c++
判断参数“c”是否是一个十进制数字字符。如果是十进制数字字符，返回true，否则返回false。十进制数字字符用正则表达式为：[0-9]
isdigit (c);
```

**islower( )**

```
判断参数“c”是否是一个小写字母。如果是小写字母，返回true，否则返回false。小写字母用正则表达式为：[a-z]
islower (c);
```

**isupper( )**

```c++
判断参数“c”是否是一个大写字母。如果是大写字母，返回true，否则返回false。大写字母用正则表达式为：[A-Z]
isupper (c);
```

**isxdigit( )**

```c++
判断参数“c”是否是一个十六进制数字字符。如果是十六进制数字字符，返回true，否则返回false。十六进制数字字符用正则表达式为：[a-f0-9A-F]。通常x在代码中有代表十六进制的含义，因此函数名为isxdigit。它比十进制数字字符多了小写a到f，大写A到F。因为十六进制表示时，是不区分大小写的，a和A表示的十六进制值都是十进制的10，所以十六进制数字字符有小写的abcdef,也包含大写的ABCDEF。

isxdigit (c);
```

**tolower( )、toupper( )函数**

```c++
将给定一个字符转换为小写
tolower(ch);
将给定一个字符转换为大写
toupper(ch);
```



## String类

```c++
#include <string> //注意这里不是string.h，这是C字符串头文件
using namespace std;
```

**std::string中的反向迭代器rbegin（）、rend（）**

```c++
rbegin()：表示string字符串的倒数第一个字符
rend()：表示string字符串的正数第一个字符
string sgood_rev(sgood.rbegin(), sgood.rend());//定义一个新的翻转string类
```

**size**

求string长度

```c++
string.size(); 等价 string.length();
```



## stack栈用法

```c++
#include<stack>//头文件
stack<int> q;	//以int型为例
int x;
//常用操作：
q.push(x);		//将x压入栈顶,括号内需要有变量
q.top();		//返回栈顶的元素
q.pop();		//删除栈顶的元素
q.size();		//返回栈中元素的个数
q.empty();		//检查栈是否为空,若为空返回true,否则返回false
```



## unordered_map 容器

*无序的map容器*

```c++
#include <unordered_map>
using namespace std;
```

- 以键值对（pair类型）的形式存储数据，存储的各个键值对的键互不相同且不允许被修改

- 使用<font color='red'>[ ]操作</font>符来访问key值对应的value值，pairs[ch]



## exp( )、log( )

```c++
头文件：#include<cmath>
exp(x):求e的x次方
log(x):求e为底，x的对数
```

## 指定序列生成不同的排列

```c++
头文件：#include<algorithm>
    next_permutation按照字母顺序生成给定序列的下一个较大的序列，直到整个序列为减序位置
    prev_premutation按照字母顺序生成给定序列的上一个较小的序列
    二者原理相同，仅遍历顺序相反。
```

