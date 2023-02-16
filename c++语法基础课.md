#  c++语法基础注意点

## 一、简单顺序结构

### main( )

最新版的c++**不允许**使用void main( ) 

### printf格式

```c++
%05d    宽度为5，左端自动补4个0
%-5d    宽度为5，右端自动补空格
%5.1f   保留小数点一位，宽度为5
```

## 三、循环

#### 增强for循环

范围遍历

```c++
string s = "HELLO WORLD";
for(变量类型  新的遍历变量名 ： 被遍历的变量)
for(char c : s) cout << c << endl;
//取地址改变字符串内容
for(char &c : s) c = 'a';
//auto类型
//自动类型推导，但是必须初始化
for(auto c : s)//用于类型比较长的时候
```



## 四、数组

### 分配内存

指针数组初始化需要提前分配内存，并置0，**calloc**

一般数组（已经设置数组边界值）已经分配好内存，只需置0，**memset**、

### 获取数组长度

- 字符串数组长度：strlen( )

- 万能方法：

  sizeof(a) / sizeof(a[0]) ——使用sizeof关键字
  
  注意：因为字符串结尾处还有一个‘ \n ’字符，所以使用该方法时会比真实长度大了1，即为strlen( ) + 1

### 定义变量的默认值

```c++
int n;//默认值为0
```

## 五、字符串

### 用地址调用数组元素

```c++
*(a+k);/*调用数组第k+1的元素*/
```

### ASCII码值

每个常用字符都对应一个-128~127的数字

空格" "是32

’0’-‘9’是48-57

’A’-‘Z’ 是65~90

’a’-‘z’是97-122

字符可以**参与运算**，需要用**'单引号 '**，运算时会将其当做**整数**

```c++
'1' != 1
```

### 字符数组

字符数组的长度至少要比字符串的长度**多1**(必须要有一个空间存放'\0')

字符串就是字符数组加上**结束符’\0’**

Difference：

```c++
/*单个字符用单引号'', 字符串用双引号""*/
char a[] = {'C', '+', '+'};//列表初始化，没有空字符
char a[] = {'C', '+', '+', '\0'};//列表初始化，含有空字符
char a[] = "C++";//列表初始化，自动添加空字符'\0'
```

### 字符串输入

#### scanf

**过滤空格**

%s格式的输入不需要加上&，因为**字符串的数组名**就是指针，指向首地址（！仅限字符串数组！）

遇到空格结束，不会过滤回车

```c++
//从数组下标唯一1开始输入,输出类似
scanf("%s", s + 1);
cin >> s + 1;
//字符串用空格或回车隔开即可
scanf("%s%s", s1, s2);
//过滤回车
scanf("\n%s",s);
```

#### cin

**过滤空格**

cin >> 字符串首地址，遇到空格或回车会停止，只能输入没有空格的字符串

#### cin.getline

**可读空格，可以读取一整行**

```c++
两个头文件
<string>
<iostream>
```

cin.getline(s, 100);

cin.getline(字符串首地址，最多读入长度)；

遇到**回车'\r'**结束，可以有空格

#### fgets（容易出错）

**可读空格，可以读取一整行**

```c++
char s[100];
//fgets(s, 100, stdin)
//fgets(字符串首地址，最多读入字符数，读入的文件名（一般为stdin）)
```

- 该函数从`stream`所指的文件中读取以`'\n'`结尾的一行（包括`'\n'`在内）存到缓冲区`s`中，并且在该行末尾添加一个 `'\0'`组成完整的字符串。
- **`fgets()`函数的最大读取大小是其“`第二个参数减1`”，这是由于字符串是以`’\0’`为结束符的**

- **输入回车时会读入'\n' ，输入`n`个字符按下回车输入，`fgets()`存储进第一个参数指定内存地址的是`n+2`个字节**







### 字符串输出

#### puts

puts(字符串数组名)；

puts输出自带有换行

#### printf

printf("%s", s);

### 常用操作

```c++
头文件：<cstring>
```

 #### strlen( )

strlen(str)，求字符串的长度

**一般提前用新变量保存好字符串的长度再进入循环**

#### strcmp( )

strcmp(a, b)，比较两个字符串的大小,按照**字典序**方式比较

字典序(按照ASCII码)：abc < adbe

a < b 返回-1

a == b 返回0

a > b返回1

#### strcpy( )

strcpy(a, b)，将字符串b复制给从a开始的字符数组



### 思想：统计字符中字符出现的次数

开辟新的长度为26的数组，统计每个字幕出现的次数

```c++
for(int i = 0; str[i]; i ++) //str[i]至'\0'结束，循环也就停止  
    cnt[str[i] - 'a'] ++;
```

### 思想：小写字母变为下一位

```c++
//c为增强for循环中设置的变量
c = (c - 'a' + 1) % 26 + 'a';
```



### 标准库类型String(80%用string处理，常用)

#### 头文件

```c++
//头文件
#include<string>
```

#### 初始化定义

```c++
string s1; //默认的空字符串
string s2 = s1;//s2等于s1
string s3 = "jjj";
string s4(10, 'c');//s4为cccccccccc
```

#### 输入

**scanf不能用，会报错**

##### cin

**过滤空格**

cin >> s;

##### getline

**可读空格，可以读取一整行**

getline(cin, s);

#### 输出

##### cout

cout << s;

##### printf(耗时更少)

printf("%s\n", s.c_str());

c_str()调用成员函数：返回字符数组的首地址

##### puts

puts(s1.c_str());

c_str()调用函数返回字符数组的首地址

#### empty

s.empty( )

返回布尔值，s为空返回1，非空返回0

#### size

s.size( )

返回无符号整型的字符串长度

与strlen( )遍历一次求长的o( n )时间复杂度不同，该函数时间复杂度为o( 1 )

#### string比较

支持 > < >= <= == !=等所有比较操作，按字典序进行比较。

#### 赋值

```c++
s1 = s2;
```

给s1赋值为s2的值

#### 相加

必须确保每个加法运算符的两侧的运算对象**至少有一个是string**

不能都为字符或字符串类型

```c++
s3 = s1 + s2;
s3 += s1;
/*可以加上字符或字符串*/
s3 = s3 + "Hello" + 'H';
```

#### 处理字符

- 当成字符数组，例如可以for循环使用s[i]
- 使用增强for循环



## 六、函数

### 组成

- 返回类型(必须写)、函数名字、由0个或多个形参组成的列表以及函数体

- **return语句**负责结束函数并返回一个值。不写会返回一个随机值。

### 调用

- 用实参初始化函数对应的形参
- 将控制权转移给被调用函数。此时，主调函数的执行被暂时中断，被调函数开始执行。

### 声明和定义

声明：没有函数体

定义：必须写函数体

### 形参列表

函数的形参列表可以为空，但是不能省略。

```c++
void f1() {/* …. */}        // 隐式地定义空形参列表
void f2(void) {/* … */}      // 显式地定义空形参列表
```

形参列表中的形参通常用逗号隔开，其中每个形参都是含有一个声明符的声明。即使两个形参的类型一样，也必须把两个类型都写出来：

```c++
int f3(int v1, v2) {/* … */}       // 错误
int f4(int v1, int v2) {/* … */}    // 正确
```

 ### 返回类型

- 大多数类型都可作为返回类型
- 特殊：void——表示函数不返回任何值、
- 函数的返回类型不能是数组类型或函数类型，但可以是**指向数组或者函数的指针**。

### 全局/局部/静态变量

- 局部变量只可以在函数内部使用（重名时优先选择）
- 全局变量可以在所有函数内使用
- static静态，可以设置一个只在该函数内用的全局变量（节省空间，存入堆中，非栈）

### 参数传递

#### 传值参数（int a）

- 初始化一个非引用类型的变量时，函数中设定的初始值被拷贝给主函数中的变量。

- 在函数中对变量的改动不会影响主函数中的初始值。

#### 传引用参数（int &a）

- 当函数的形参为引用类型时，函数中对形参的修改会影响主函数中实参的值。
- 使用引用的作用：避免拷贝、让函数返回额外信息。

#### 重载

函数名一样的情况无大碍，还取决于**参数类型**

### 数组形参

**传引用参数**

- 一维数组形参的写法：

  ```c++
  void print(int *a) {/* … */}
  void print(int a[]) {/* … */}
  void print(int a[10]) {/* … */}
  ```

- 多维数组形参的写法：

  多维数组中，除了**第一维**之外，其余维度的大小必须指定

  （c++中多维数组会被转化为一维数组的指针样式进行保存）

  ```c++
  void print(int (*a)[10]) {/* … */}
  void print(int a[][10]) {/* … */}
  ```

  

### 返回类型和return语句

#### 两种形式

```c++
return;
return expression;
```

#### 返回类型和return语句

##### 无返回值函数

- 没有返回值的return只能用在返回类型是void的函数中，该类函数也没必要写上return
- 有点类似于我们用break语句退出循环。

##### 有返回值的函数

- 返回类型不是void，每条return都必须返回一个与函数类型相同的值

### 函数递归

函数内部可以调用函数本身

## 七、类&结构体 指针&引用

### 类

类可以将变量、数组和函数完美地打包在一起

**复杂抽象，比较庞大**

- private

  后面的内容是私有成员变量，在类的外部不能访问

- public

  后面的内容是公有成员变量，在类的外部可以访问

```c++
class Person {
    int age;//类默认为private
    private:
    	int age, height;
    	double monney;
    	string books[N];
    public:
    	int get_height()
        {
            return height;
        }
    public:
    	string name;
		void say()
        {
            cout << "I'm" << endl;
        }
    	int get_age()
        {
            return age;
        }
    	void add_money(double x)
        {
            money += x;
        }
}Person1, Person2;
int main()
{
    Person c;
    c.name = "hxh";
    c.age = 18;//错误！因为age是private类型的变量
    c.add_money(10000);
}
```

### 结构体

**比较短，存和数据相关的**

```c++
struct Person {
	int age;//结构体默认是public
};
```

### 内存空间分配方式

程序的进程保存在堆栈中，保存形式为**十六进制**

- 动态数据区：
  - 局部变量存在**栈**里，未设定初值，每次分配的位置不一样，所以每次都不一样
  - 向下增长，从上往下分配

- 静态数据区：
  - 全局/静态变量存在**堆**里，设定初始值为0
  - 向上增长，从下往上分配

`1 byte = 8 bit`

### 指针

指针指向存放变量的值的地址。因此我们可以通过指针来修改变量的值。

```c++
//找到变量地址，需要转化成指针类型
char c = 'a';
cout << (void*)&c << endl;

//将变量值赋给指针
int* p = &a;//(int*)类型的p的值是变量a的地址
cout << *p << endl;//读取指针p指向的变量的值
*p = a;//修改p指向的变量的值
```

### 区别&注意点

- 不同点在于类默认是private，结构体默认是public。

- **指针访问 ->**

- **普通访问 **

- new

  ```c++
  struct Node {
      int val;
      Node* next;
      /*构造函数初始值列表*/
     // 结点类型(输入值) : 变量1(传值), 变量2(传值) {}
      Node(int _val) : val(_val), next(nullptr) {}
  };
  int main()
  {
      //定义Node类型的变量，p保存的是变量地址
      Node* p = new Node(1);
      auto q = new Node(2);//auto自动设置，因为new Node()自动返回Node*类型
      auto o = new Node(3);
      //定义Node类型的变量，结点值是1
      Node node = Node(1);
  }
  ```

#### 数组——特殊的指针

```c++
int a[5] = {1, 2, 3, 4, 5};
int *p = a;//p的值是数组a的地址
```

#### C++的引用语法

- 指针指向一块内存，内部存储的内容是所指的内存的地址

- 引用是模块内存的别名，跟原来的变量实质上是同一个东西。
- 指针和引用都可以作为函数参数，改变实参的值。

```c++
//和指针类似，相当于给a取个别名
int& p = a;

int a = 996;
int *p = &a; // p是指针, &在此是求地址运算
int &r = a; // r是引用, &在此起标识作用
```

#### 单链表

```c++
#include<iostream>

using namespace std;

struct Node
{
    int val;
    Node* next;
    
    Node(int _val) : val(_val), next(nullptr) {}
}
int main()
{
    auto p = new Node(1);
    auto q = new Node(2);
    auto o = new Node(3);
    
    p->next = q;
    q->next = o;
    
    Node* head = p;
    /*添加结点*/
    Node* u = new Node(4);
    u->next = head;
    head = u;
    /*删除结点*/
    head->next = head->next->next;
    /*链表的遍历*/
    for(Node* i = head; i; i = i->next)
        cout << i->val << endl;
   
    return 0;
}
```



# 八、STL

STL是提高c++编写效率的一个利器。

## vector

vector是**变长数组**，支持**随机访问**，**不支持**在任意位置O(1)插入。为了保证效率，元素的增删一般应该在末尾进行。

- 利用倍增实现动态增长
  - 长度不够时进行1/2拷贝，n(1/2 + 1/4 + 1/8 + ....)，平均每次时间复杂度是o(1)
  - 定义的耗时比数组慢，使用的效率快

### 声明

```c++
#include <vector> 	//头文件
vector<int> a;		//相当于一个长度动态变化的int数组
vector<int> b[233];	//相当于第一维长233，第二位长度动态变化的int数组
    
struct rec{…};
vector<rec> c;		//自定义的结构体类型也可以保存在vector中

//二维数组
vector<vector<int>> dp(m, vector<int>(n, 0));
```

### size( )

- size函数返回vector的实际长度（包含的元素个数）
- 时间复杂度都是O(1)
- 所有的STL容器都支持这个方法，含义也相同

```c++
a.size();
```

### empty( )

- empty函数返回一个bool类型，表明vector是否为空
- 时间复杂度都是O(1)
- 所有的STL容器都支持这两个方法，含义也相同

```c++
a.empty;
```

### clear

- clear函数把vector清空，只有0个元素

```c++
a.clear();
```

### 迭代器

迭代器就像STL容器的“指针”，可以用星号“*****”**操作符解除引用**。

```c++
//一个保存int的vector的迭代器声明方法为：
//it保存a的首地址，
vector<int>::iterator it = a.begin();
```

#### begin( )

```c++
a.begin(); === &a[0]
*a.begin(); === a[0]
```

#### end( )

- 左开右闭，[begin, end)

- end函数返回vector的尾部，即第n个元素再往后的“边界n + 1“。
- *a.end()与a[n]都是越界访问，其中n=a.size()，即容器长度

#### 遍历方法

- 类似数组

  ```c++
  for(int i = 0; i < a.size(); i++) cout << a[i] << ' ';
  //增强for循环
  for(int x : a) cout << x << ' ';
  ```

- 迭代器遍历

  ```c++
  //可以用auto代替i的类型定义
  for(vector<int>::iterator i = a.begin(); i != a.end(); i++) cout << *i << ' ';
  ```

#### front / back

- front函数返回vector的第一个元素，等价于*a.begin() 和 a[0]。

- back函数返回vector的最后一个元素，等价于 a[a.size() – 1]，a.end()的前一个位置。

#### push_back() / pop_back() 

- a.push_back(x) 把元素x插入到vector a的尾部。时间复杂度o(1)

- b.pop_back() 删除vector a的最后一个元素。时间复杂度o(1)

  

## queue

头文件queue主要包括循环队列queue和优先队列priority_queue两个容器。

**先进先出**的顺序

### 循环队列queue

#### 声明

```c++
#include<queue> 	//头文件
queue<int> q;
```

#### 操作

```c++
q.push(1);//队头插入一个元素
q.pop();//弹出队尾元素
q.front();//返回队头元素
q.back();//返回队尾元素
```

### 优先队列priority_queue

#### 声明

```c++
#include<queue> 	//头文件
priority_queue<int> q;		// 大根堆(优先返回大的数)
priority_queue<int, vector<int>, greater<int>> q;	// 小根堆(返回最小值)
priority_queue<pair<int, int>>q;

struct rec{
    int a,b;
    //重载小于号
	bool operator< (const Rec& t) const
	{
		return a < t.a;//降序出列，从小到大排序，从大到小出列
        或者
        return a > t.a;//升序排列，从大到小排序，从小到大出列
	};
}; 
priority_queue<rec> q;//结构体rec中必须重载小于号函数
```

#### 操作

```c++
a.push(1);//插入一个数，按顺序自动调整
a.top();//取最大值
a.pop();//删除最大值
```

#### 清空队列

```c++
q = queue<int>();//重新初始化
```



## stack

### 声明

```c++
#include <stack>//头文件
stack<int> stk;
```

### 操作

```c++
int x;
stk.push();//向栈顶插入
stk.top();//返回栈顶元素
stk.pop;//弹出删除栈顶元素
q.size();		//返回栈中元素的个数
q.empty();		//检查栈是否为空,若为空返回true,否则返回false
```



## deque

- 双端队列deque是一个支持在两端高效插入或删除元素的连续线性存储空间。它就像是vector和queue的结合。

- 与vector相比，deque在头部增删元素仅需要O(1)的时间，vector需要o(n)时间

- 与queue相比，deque像数组一样支持随机访问。

### 声明

```c++
#include<deque>;
deque<int> a;
```

### 操作

```c++
[] 随机访问
a.begin/end();/*返回deque的头/尾迭代器*/
a.front/back(); /*返回队头/队尾元素*/
a.push_back(1); /*从队尾入队*/
a.push_front(1); /*从队头入队*/
a.pop_back(); /*从队尾出队*/
a.pop_front(); /*从队头出队*/
a.clear(); /*清空队列*/
```



## set

- 头文件set主要包括set和multiset两个容器，分别是“有序集合”和“有序多重集合”

- 前者的元素不能重复，而后者可以包含若干个相等的元素。

- set和multiset的内部实现是一棵红黑树，它们支持的函数基本相同。

### 声明

```c++
#include<set>
using namespace std;

set<T泛型> name;//定义的标准方式
set<int> a;//元素不能重复
multiset<double> a;//元素可以重复

struct rec{
	int a,b;
	bool operator< (const Rec& t) const
	{
		return a<t.a;
	};//重载小于号，使其从小到大排列，默认小顶堆
}; 
set<rec> s;	// 结构体rec中必须重载小于号函数
```

### size/empty/clear

与vector类似

### 迭代器

- set和multiset的迭代器称为“双向访问迭代器”，不支持“随机访问”，支持星号(*)解除引用，仅支持”++”和--“两个与算术相关的操作。

- 设it是一个迭代器，例如set<int>::iterator it;

- 若把it++，则it会指向“下一个”元素。这里的“下一个”元素是指在元素从小到大排序的结果中，排在it下一名的元素。同理，若把it--，则it将会指向排在“上一个”的元素。

```c++
set<int>::iterator it = a.begin();
it++; it--;
++it; --it;

//遍历时常用
for(it = s.begin(); it != s.end(); it++)
    printf("%d\n", *it);//解引用
```

### begin/end

- s.begin() 是指向集合中最小元素的迭代器。
- s.end() 是指向集合中**最大元素的下一个位置**的迭代器。换言之，就像vector一样，是一个“前闭后开”的形式。因此--s.end()是指向集合中最大元素的迭代器。

### insert元素插入

- s.insert(x)把一个元素x插入到集合s中
- 时间复杂度为O(logn)。
- 在set中，若元素已存在，则不会重复插入该元素，对集合的状态无影响。

### find

- s.find(x) 在集合s中查找等于x的元素，并返回指向该元素的迭代器。若不存在，则返回s.end()。

  ```c++
  if(a.find(x) == a.end()) //判断x在a中是否存在
  ```

- 时间复杂度为O(logn)。

### lower_bound/upper_bound

- s.lower_bound(x) 查找**大于等于**x的元素中最小的一个，并返回指向该元素的迭代器。
- s.upper_bound(x) 查找**大于**x的元素中最小的一个，并返回指向该元素的迭代器。

### erase

- 设x是一个**元素**，s.erase(x) 从s中删除**所有等于x的元素**，时间复杂度为O(k+logn)，其中k是被删除的元素个数。
- 设it是一个**迭代器**，s.erase(it) 从s中**删除迭代器it指向的元素**，时间复杂度为O(logn)

### count

s.count(x) 返回集合s中**等于x的元素个数**，时间复杂度为 O(k +logn)，其中k为元素x的个数。

- set不存在返回1，存在返回0
- multiset存在返回个数



## map

### 声明

- map容器是一个键值对key-value的映射，其内部实现是一棵以key为关键码的红黑树。
- Map的key和value可以是任意类型，其中key必须定义小于号运算符。

```c++
#include<map>
using namespace std;
//程序中默认指定了std命令空间，可以省略std:
std::map<std::string, int>mymap{{"emm", 10}, {"STL", 20}};
//创建空容器 + 初始化
map<key_type, value_type> name;

//此处和数组差不多
map<int, int> a;//二元组
a[1] = 2;
cout << a[1] << endl;

map<string, vector<int>> a;
a["hhh"] = vector<int>({1, 2, 3, 4});
cout << a["hhh"][2] << endl;

//重载小于号，使从小到大排列
struct Node {  
	int d, e;  
	bool operator < (const Node x) const 
    {  
	return d < x.d;      //从小到大排序
    }   
    Node(int d, int e):d(d), e(e){}  
}; 
```

### size/empty/clear/begin/end/count/lower_bound/upper_bound/max_size/swap

均与set类似。

### Insert/erase

与set类似，但其参数均是pair<key_type, value_type>

```c++
a.insert({"a", {}});
```

### find

h.find(x) 在变量名为h的map中查找key为x的二元组，用法与set类似。

```c++
a.find(key) == a.end()
```

### [ ]操作符

- h[key] 返回key映射的value的引用，时间复杂度为O(logn)。

- []操作符是map最吸引人的地方。我们可以很方便地通过h[key]来得到key对应的value，还可以对h[key]进行赋值操作，改变key对应的value。



# 九、位运算、常用库函数

### 位运算

#### 位运算符

移位运算符优先级最高

& 与

```c++
0 & 0 = 0
0 & 1 = 0
1 & 1 = 1
```

| 或

```c++
0 | 0 = 0
1| 0 = 1
0 | 1 = 1
1 | 1 = 1
```

**~ 非**

```c++
~ 0 = 1
~ 1 = 0
```

**^ 异或**

a⊕b = (¬a ∧ b) ∨ (a ∧¬b)

```c++
0 ^ 0 = 0
1 ^ 1 = 0
1 ^ 0 = 1
    
//int类型的两个数异或
3 ^ 6 = (011) & (110) = (101) = 5
```

\>> 右移

- 右边减一个数字位，相当于 / 2

- a >> k === a/pow(2, k)

<< 左移

- 右边加0，相当于 * 2

- a << k === a * pow(2, k)

#### 常用操作：

- 求x的第k位数字 x >> k & 1

  ```c++
  a = 110110
  a >> k = 1101
  a >> k & 1 = (1101) & (0001) = 1
  ```

- lowbit(x) = x & -x，lowbit(x) 为返回x的**最后一位1和后i面的0**

```c++
a = 10101100100000
~a = 01010011011111
~a + 1 = 01010011100000
a & (~a + 1) = 100000
负数用补码表示，补码和反码一样
```

### 常用库函数

#### reverse 翻转

时间复杂度为o（n）

```c++
//头文件
#include <algorithm>
using namespace std;
```

- 翻转一个**vector**

  ```c++
  reverse(a.begin(), a.end());
  ```

- 翻转一个**数组**

  左闭右合[   ,    )

  ```c++
  reverse(a, a + n);
  ```

- 翻转一个**字符串**

  ```c++
  reverse(str.begin(),str.end();
  ```

#### unique 去重

```c++
//头文件
#include <algorithm>
using namespace std;
```

- 使用unique的容器重复元素**必须靠在一块**
- 返回去重之后的尾迭代器（或指针），仍然为前闭后开，即这个迭代器是去重之后末尾元素的下一个位置。
- 该函数常用于离散化，利用迭代器（或指针）的减法，可计算出去重后的元素个数。

把一个vector去重：

```c++
int m = unique(a.begin(), a.end()) – a.begin();//m为去重后的元素个数
a.erase(unique(a.begin(), a.end()), a.end());//删除后面重复元素，保留前面不重复的部分
```

把一个数组去重，元素存放在下标1~n：

```c++
int m = unique(a, a + n) – a;//m为去重后的元素个数
```

#### random_shuffle 随机打乱

```c++
//头文件
#include <algorithm>
using namespace std;
```

用法与reverse相同

```c++
random_shuffle(a.begin(), a.end());
random_shuffle(a, a + n)
```

#### sort

**头文件：**

```C++
#include <algorithm>
using namespace std;
```

- 对两个迭代器（或指针）指定的部分进行**快速排序**

- 参数和reverse的用法一样，可以在第三个参数传入定义大小比较的函数，或者重载“小于号”运算符。
- sort()函数可以对给定区间所有元素进行排序。它有三个参数<font color='red'>sort(begin, end, cmp)</font>，其中begin为指向待sort()的数组的<font color='red'>第一个元素的指针</font>，end为指向待sort()的数组的<font color='red'>最后一个元素的下一个位置的指针</font>，cmp参数为排序准则，cmp参数<font color='red'>可以不写（即为sort（begin, end））</font>，**默认从小到大进行排序**。如果我们想从大到小排序可以将cmp参数写为greater<int>()就是对int数组进行排序，当然<>中我们也可以写double、long、float等等。

```c++
sort(a.begin(),a.end());//从小到大排序
sort(a.begin(), a.end(), greater<int>());//从大到小排序
```

```c++
int a[MAX_SIZE];
//全局函数
bool cmp(int a, int b)//a是否应该排在b的前面 
{
    return a > b; //如果a > b, 那么a应该排在b的前面，则为降序排列
    或者
    return a < b;//如果a < b，那么a应该排在b的前面，则为升序排列
}
sort(a, a + n, cmp);
```

把自定义的结构体vector排序，重载“小于号”运算符：

```c++
struct rec
{
    int id, x, y; 
    bool operator <(const rec &t)const 
	{
		return x < t.x;
	}
}
vector<rec> a;
sort(a.begin(), a.end()); 
```

#### lower_bound/upper_bound 二分

**头文件：**

```c++
#include <algorithm>
using namespace std;
```

- lower_bound 的第三个参数传入一个元素x，在两个迭代器（指针）指定的部分上执行二分查找，返回指向**第一个大于等于x**的元素的位置的**迭代器**（指针）。

  ```c++
  int a[] = {1, 2, 3, 4, 5,, 6};
  int* p = lower_bound(a, a + 5, 7);
  ```

  - 有序int数组中查找大于等于x的最小整数的**下标**

    ```c++
    int t = lower_bound(a, a + n, x) – a;
    ```

  - 有序vector<int> 中查找小于等于x的最大整数（假设一定存在）

    ```c++
    int y = upper_bound(a.begin(), a.end(), x) - a.begin();
    ```

- upper_bound 的用法和lower_bound大致相同，唯一的区别是查找**第一个大于x的元素**。当然，两个迭代器（指针）指定的部分应该是提前排好序的。
  
  - 用法与lower_bound一致