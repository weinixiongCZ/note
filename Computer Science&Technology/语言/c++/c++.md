#CS/Cpp

# c与c++对比

| 特性 | C | C++ |
| :--- | :--- | :--- |
| Algorithms|5|119|
|Atomic operations|35|76|
|Concepts||31|
|Containers||585|
|C keywords|46|96|
|C language|94|188|
|Date and time|21||
|Dynamic memory management|6|91|
|Error handling|9||
|Feature testing||1|
|File input/output|101|161+390|
|iterator||91|
|Localization support|10|206|
|Numeric|309|685|
|Named requirement||69|
|Program support|27||
|Ranges||35|
|Regular expressions||78|
|Standard library headers||96|
|Strings|146|242|
|Thread support|38|198|
|Type support|11||
|Utilities||1066|
|Variadic functions|6||



# 入门

## 结构

每个 C++ 程序至少有一个名为`main`的函数，[[操作系统]]通过调用`main`函数来执行程序，`main`函数则返回一个值给操作系统来表明程序执行完毕，返回 0 表示执行完毕，任何其他非零的返回值都有操作系统定义的含义， 通常非零返回值表明有错误出现。每一种操作系统都有自己的方式告诉用户`main`函数返回什么内容。

 C++ 程序文件的后缀与运行的具体编译器有关，包括`.cxx`，`.cpp`，`.cp`，`.C`

## 编译和执行

- GNU：`g++ fileName.cpp -o outputName`，`-o`是可选的，不选的话输出文件名为`a.out`(UNIX),`a.exe`(Windows)。 
	- UNIX： 命令行输入`./outputName`(无后缀) 或`./a.out`执行程序
	- Windows：命令行输入`outputName`或`a`执行程序(后缀`.exe`可省略)
- 微软编译器：cl -GX fileName.cpp，输出文件与源文件同名，命令行输入`fileName`执行程序。

## 输入和输出

### 标准输入和输出对象

- `istream`：`cin`被称为标准输出
- `ostream`：`cout`被称为标准输出，`cerr`被称为标准错误，`clog`用于产生一般信息 ，

- `<<`：输出操作符，接受左右两个参数，左操作数必须是`ostream`对象；右操作数是要输出的值，结果仍是左操作数，即输出流。

>前缀`std::`表明`cout`和`endl`是定义在命名空间`std`中 的。使用命名空间程序员可以避免与库中定义的名字相同而引起无意冲突。因为标准库定义的名字是定义在命名空间中，所以我们可以按自己的意图使用相同的名字。

- `>>`：输入操作符，接受左右两个参数，左操作数必须是`istream`对象；右操作数将被赋予输入值，结果仍是左操作数，即输入流。遇到无效输入时结果为无效输入流，将导致条件判断为否，比如
	
	```cpp
	int a
	while(std::cin>>a)//输入非整数值将结束循环
	```

>在写 C++ 程序时，大部分出现空格符的地方可用换行符代替。这条规则的一个例外是字符串字面值中的空格符不能用换行符代替。另一个例外是空格符不允许出现在预处理指示中。

>定义变量时，应该给变量赋初始值，除非确定第一次使用变量时会赋予初值。如果不能保证读取变量之前变量已经赋值，就应该初始化变量。

# 变量和基本类型

>不同与某些语言，c++中可以把负数赋值给无符号类型

>为了兼容 C 语言，C++ 中所有的字符串字面值都由编译器自动在末尾添加一个空字符

## 多行书写字符串

### 方式一

```cpp
"a multi-line " 
"string literal " 
"using concatenation"
```

### 方式二

```cpp
"a multi-line \
string literal \
using a backslash"
```

## 左值和右值

1. 左值（发音为 ell-value）：左值可以出现在赋值语句的左边或右边。
2. 右值（发音为 are-value）：右值只能出现在赋值的右边，不能出现在赋值语句的左边。

## 初始化

`int a=b=0`b未定义时此语句是非法的，因为同一定义语句中不同变量的初始化应分别进行。

### 声明

```cpp
// file_1.cc 
int counter; // definition 
// file_2.cc
extern int counter; // uses counter from file_1 
++counter;// increments counter defined in file_1
```

> `extern`声明不是定义，也不分配存储空间。事实上，它只是说明变量定义在程序的其他地方。程序中变量可以声明多次，但只能定义一次。任何在多个文件中使用的变量都需要有与定义分离的声明。在这种情况下， 一个文件含有变量的定义，使用该变量的其他文件则包含该变量的声明（而不是定义）。

```cpp
// file_1.cc 
extern const int counter=0; // definition 
// file_2.cc
extern const int counter; // uses counter from file_1 
int i = counter;// user counter defined in file_1
```

> 与其他变量不同，除非特别说明，在全局作用域声明的`const`变量是定义该对象的文件的局部变量。此变量只存在于那个文件中，不能被其他文件访问。通过指定`const`变更为`extern`，就可以在整个程序中访问`const`对象

## 引用

- 引用就是对象的另一个名字。在实际程序中，引用主要用作函数的形式参数。

- 引用是一种复合类型，通过在变量名前添加“&”符号来定义。复合类型是指用其他类型定义的类型。在引用的情况下，每一种引用类型都“关联到”某一其他类型。不能定义引用类型的引用，但可以定义任何其他类型的引用。

- 引用必须用与该引用同类型的对象初始化。

- 因为引用只是它绑定的对象的另一名字，作用在引用上的所有操作事实上都 是作用在该引用绑定的对象上。

- `const`对象必须用`const`引用，`const`引用可以初始化为不同类型的对象或者初始化为右值

```cpp
int i=42;
const int &r=42;
const int &r1=i;
const int &r2=r+i;
double dval = 3.14;
const int &ri = dval;
```

## typedef

```c++
//typedef 可以用来定义类型的同义词：
typedef double wages;// wages is a synonym for double
typedef int exam_score; // exam_score is a synonym for int
typedef wages salary;// indirect synonym for double
//typedef 名字可以用作类型说明符： 
wages hourly, weekly;  // double hourly, weekly; 
exam_score test_result; // int test_result;
```

typedef 通常被用于以下三种目的：

1. 为了隐藏特定类型的实现，强调使用类型的目的。 
2. 简化复杂的类型定义，使其更易理解。 
3. 允许一种类型用于多个目的，同时使得每次使用该类型的目的明确。

## 枚举

```c++
enum open_modes {input, output, append};//input被默认赋值为0，后面的值比前面大1
enum Forms {shape = 1, sphere, cylinder, polygon};//shape显式赋值为1，后面的值比前面大1
enum Points { point2d = 2, point2w, point3d = 3, point3w };//point2w=3，point3w=4
```

枚举类型是常量，每个枚举类型都被定义为一种唯一的类型，枚举类型必须用相应的枚举对象初始化或赋值

```c++
Points pt3d = point3d; // ok: point3d is a Points enumerator 
Points pt2w = 3; // error: pt2w initialized with int 
pt2w = polygon; //error: polygon is not a Points enumerator
pt2w = pt3d;//ok: both are objects of Points enum type
```



## 类

用 class 和 struct 关键字定义类的唯一差别在于默认访问 级别：默认情况下，struct 的成员为 public，而 class 的成 员为 private。

### 编译多个源文件

```shell
g++ -c main.cc A.cc//generates main.o A.o
g++ main.o A.o//generates a.exe
```



## 使用头文件

### 避免多重包含

```cpp
#ifndef MYFILE_H
#define MYFILE_H
/*
	definiton of clas and function
*/
#endif
```

### 使用自定义头文件

```cpp
#include <standard_>
#include "my_file.h"
```

# 标准库类型

## 命名空间的`using`声明

```cpp
using namespace::name;
```

> 在头文件中必须总是使用完全限定的标准库名字，理由是头文件的内容会被预处理器复制到程序中。用`#include`包含文件时，相当于头文件中的文本将成为我们编写的文件的一部分。如果在头文件中放置`using`声明，就相当于在包含该头文件`using`的每个程序中都放置了同一`using`，不论 该程序是否需要`using`声明

## 标准库`string`

```cpp
#include <string> 
using std::string;
```

> 因为历史原因以及为了与 C 语言兼容，字符串字面值与标准库`string`类型不是同一种类型。

### 从标准输入读取`string`

- 读取并忽略开头所有的空白字符（如空格，换行符，制表符）。

- 读取字符直至再次遇到空白字符，读取终止。

### 使用`getline`读取整行文本

`getline`读取到换行符时将前面的内容存为一个`string`，由于`getline`函数返回时丢弃换行符，换行符将不会存储在`string`对象中，逐行输出时要自行添加。

```cpp
int main() {
    string line;
    while (getline(cin, line)) 
        cout << line << endl;
    return 0; 
}
```

### `string`操作符

> `string`对象比较操作是区分大小写的，即同一个字符的大小写形式被认为是两个不同的字符。在多数计算机上，大写的字母位于小写之前：任何一个大写之母都小于任意的小写字母。

关系操作符比较两个 string 对象时采用了和（大小写敏感的）字典排序相 同的策略：

- 如果两个 string 对象长度不同，且短的 string 对象与长的 string 对 象的前面部分相匹配，则短的 string 对象小于长的 string 对象。
- 如果 string 对象的字符不同，则比较第一个不匹配的字符。

> 当进行`string`对象和字符串字面值混合连接操作时，`+`操作符的左右操作数必须至少有一个是`string`类型的

> 下标操作可用作左值：`str[i]='*'`

## vector

> 虽然可以对给定元素个数的`vector`对象预先分配内存，但更有效的方法是先初始化一个空`vector`对象， 然后再动态地增加元素

> 在使用循环时调用`size`成员函数而不保存它返回的值不是必需的，但这反映了一种良好的编程习惯。在 C++ 中，有些数据结构（如`vector`）可以动态增长。如果循环时增加了新元素的话，那么测试已保存的`size`值作为循环的结束条件就会有问题，所以我们倾向于在每次循环中测试`size`的当前值，而不是在进入循环前，存储`size`值的副本。
>
> C++ 中有些函数可以声明为内联（`inline`）函 数。编译器遇到内联函数时就会直接扩展相应代码，而不是进行实际的函数调用。像`size`这样的小库函数几乎都定义为内联函数，所以每次 循环过程中调用它的运行时代价是比较小的。

## 迭代器

```cpp
vector<int>::iterator iter = ivec.begin();
```

由`end`操作返回的迭代器指向`vector`的“末端元素的下一个”。它指向了一个不存在的元素。 如果`vector`为空，begin 返回的迭代器与 end 返回的迭代器相同。

迭代器类型可使用解引用操作符来访问迭代器所指向的元素：`*iter = 0` 对被迭代对象的某个元素赋值为0

任何改变`vector`长度的操作都会使已存在的迭代器失效。

# 数组和指针

## 自以为指向`const`的指针和`const`指针

- `cont int *p`：不可以改变所指向的内容，可以改变指向，可以指向`const`对象
- `int *cont p`：不可以改变指向，可以改变所指向的内容，必须在定义时初始化，不可以指向`const`对象
- `cont int *cont p`：不可以改变所指向的内容，也不可以改变指向，必须在定义时初始化，可以指向`const`对象

```cpp
typedef int *ip;
const ip p;//p是const指针
```



## 指针数组和数组指针

```c++
int a[2][2];
int *p1[2]={a[0],a[1]}; // 这是一个数组，元素为2个int型指针，p[i]指向单个int，可用来创建二维动态数组
int **p=p1;//p1可以赋值给双重指针，p2不行
int (*p2)[2]=a; // 这是一个指针，指向含有2个元素的数组，p指向列为4的二维数组的某一行
typedef int int_array[2];
int_array *ip=a;//ip与p2同类型
```

| 表达式     | 输出结果                                   |
| ---------- | ------------------------------------------ |
| `p1`       | `0x64fdf0` 即`p1[0]`的地址                 |
| `p1[0]`    | `0x64fe00` 即`a[0][0]`的地址               |
| `p1[0][0]` | 0 即`a[0][0]`的内容                        |
| `p2`       | `0x64fe00` 即`a[0]`的地址，与`a`相同       |
| `p2[0]`    | `0x64fe00` 即`a[0][0]`的地址，与`a[0]`相同 |
| `p2[0][0]` | 0 即`a[0][0]`的内容                        |

`p1[0]`和`p2`的输出结果一样，因为对于首元素，无论是数组还是元素，其地址都相同，但是他们本质却不同，`p1[0]`指向一维数组的首元素，解引用一次即可输出`a[0][0]`的内容,`p2`指向一维数组，解引用一次得到指向此一维数组首元素的指针，再解引用才得到`a[0][0]`的内容。

# 表达式

## 前置运算符和后置运算符

```cpp
int i;
i=++i+i++;
cout<<i;//2*i+3
```

第二行表达式的运行步骤如下（设`a=i`，用`j`和`k`来帮助理解）：

| `i`自增                                                 | `i=a+1`            |
| ------------------------------------------------------- | ------------------ |
| `&j=i`，表达式中++i部分替换为`j`，表达式目前变为`j+i++` | `j=a+1`            |
| `k=i`，表达式中i++部分替换为`k`，表达式目前变为`j+k`    | `k=a+1`            |
| `i`自增，`j`也随之加1                                   | `j=i=a+2`，`k=a+1` |
| 将`j+k`赋值给`i`                                        | `i=2a+3`           |

上述步骤可以理解成前置运算符返回对象的引用，后置运算符返回操作前的值。

下面的代码与上面代码不同之处在于对于前置运算，解应用操作直接得到了结果

```c++
int a[5]={1,2,3,4,5};
int *p=a;
cout<<(*(++p)+*(p++));//a[1]+a[1]
```

# 语句

# 函数

## 交换指针的函数

```cpp
void ptrswap(int *&p1, int *&v2){
    int *temp=v1;
    v1=v2;
    v2=temp;
}
```

从避免复制`vector`的角度出发，应考虑将形参声明为引用类型。然而，看过第十一章后我们会知道，事实上，C++ 程序员倾向于通过传递指向容器中需要处理的元素的迭代器来传递容器：

```cpp
void print(vector<int>::const_iterator beg, vector<int>::const_iterator end)
```

## `main`函数的形参

在执行可执行文件时输入的参数(包括文件名)作为第二个参数，类型为c风格字符串数组`char**`，参数个数作为第一个参数`int`

## 函数指针

```cpp
int iFun(int a){
    return a*a*a;
}

double dFun(double a){
    return a*a;
}

//接受和dFun同类型的函数指针，返回和iFun同类型的指针
int (*pFunction(double dFun(double)))(int) {
    cout << dFun(2.2);
    return iFun;
}

int main() {
    cout<<pFunction(dFun)(2);
}
```

### 使用`typedef`简化

```cpp
typedef int (*pf)(int);

int fun(int a){
    return a*a;
}

pf pFunction(pf fun){
    return fun;
}

int main() {
    pf p=pFunction(fun);
    cout<<p(2);
}
```

# 标准`IO`库

