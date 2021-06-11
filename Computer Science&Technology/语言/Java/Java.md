#CS/Java

# 参考
- [[Java核心技术 卷1 基础知识 原书第10版.pdf]]
- [[Java核心技术 卷2 高级特性 原书第10版.pdf]]
- [[Java基础.pdf]]
- [[Java编程那些事儿.pdf]]
- [[Java编程思想第4版.pdf]]
- [[Fundamentals of Java Programming.pdf]]

# 软件构成

- `JDK=JRE+Java开发工具`
- `JRE=JVM+Java核心类库`

# 环境变量配置

1. path 中新建环境变量`E:\MinGW\bin`
2. 新建`JAVA_HOME=jdk`安装位置
3. 新建`CLASSPATH=.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`

# 常用命令行命令

- dir : 列出当前目录下的文件以及文件夹
- md : 创建目录
- rd : 删除目录
- d: ：进入D盘
- cd directory : 进入指定目录
- cd .. : 退回到上一级目录
- cd\ : 退回到根目录
- del : 删除文件
- exit : 退出 dos 命令行
- echo something>1.doc ：将something写入1.doc
- javac filename.java ：编译
- java filename ：运行

# 命名规范
- 类名：XxxYyyZzz
- 变量名：xxxYyyZzz
- 常量名：XXX_YYY_ZZZ
- 包名：全是小写
# 基本数据类型
- 整型：byte(-128~127)、short、int、long(定义时必须以 l 或 L 结尾)
- 浮点型：float(定义时必须以 f 或 F 结尾)、double
- 字符型：char(1字符=2字节=16位)
- 布尔型：boolean
## 基本数据类型转换

### 短数据类型与长数据类型运算时转换成长数类型

```java
byte char short-->int-->long-->float-->double
byte char short 做运算(同种和异种)转换成 int
long l1=123321;//int类型提升为long
long l1=123321123122323;//超出int容量，必须再末尾添加l或L
整型默认为 int 浮点型默认为 double
byte b=12;
byte b1=b+1;//编译不通过，1默认为int，右边自动提升为int
float f1=b+12.3;//编译不通过，12.3默认为double，右边自动提升为double
char c=65,c1='A';//c就是65，c1是A的arcll码值，也是65
BigDecimal bigNumber=new BigDecimal(1.000……001);//更精确的数用BigDecimal类   
```

### 强制类型转换

```java
int i=1;
byte b=(byte)i;
```
## 进制

```java
int n1=0b110;//二进制：0b或0B开头
int n2=0127;//八进制：0开头
int n3=0x110A;//十六进制：0x或0X开头
//输出时均为10进制
```

计算机底层以补码得方式储存数，正数原码和补码一致，负数的补码由非符号位取反加1得到

# 运算符 

## 算数运算符

~~~java
     int a1=12;
     int a2=5;
     double n1=a1/a2;//2.0
     double n2=(double)n1/n2//2.4
     //开发中，经常使用%来判断能否被除尽的情况 m%n=m-n*(m/n)
         int m1 = 12;
         int n1 = 5;
         System.out.println("m1 % n1 = " + m1 % n1);//2
     
         int m2 = -12;
         int n2 = 5;
         System.out.println("m2 % n2 = " + m2 % n2);//-2
     
         int m3 = 12;
         int n3 = -5;
         System.out.println("m3 % n3 = " + m3 % n3);//2
     
         int m4 = -12;
         int n4 = -5;
     
         System.out.println("m4 % n4 = " + m4 % n4);//-2
         //(前)++ :先自增1，后运算
         //(后)++ :先运算，后自增1
         int a1 = 10;
         int b1 = ++a1;//a先自增再赋值给b，b=11
         System.out.println("a1 = " + a1 + ",b1 = " + b1);
     
         int a2 = 10;
         int b2 = a2++;//a先赋值给一个中间量再自增，中间量再赋值给b，b=10
         System.out.println("a2 = " + a2 + ",b2 = " + b2);
     
         int a3 = 10;
         ++a3;//a3++;没区别
         int b3 = a3;//11        
             
     //注意点：
         short s1 = 10;
         //s1 = s1 + 1;//编译失败，右边是int
         //s1 = (short)(s1 + 1);//11，正确的
         //s1+=1//11，正确，不会改变自身数据类型
         //s1+=0.1//10，正确，不会改变自身数据类型
         s1++;//自增1不会改变本身变量的数据类型
         System.out.println(s1);
         int m=2;
         int n=3;
         n*=m++//6
         n+=(n++)+(++n)//n=n+(n++)+(++n),10+10+12//“先运算，后自增1”指的是和执行一个运算符后就自增1
~~~

## 逻辑运算符

```java
&和&&、|和||的区别：一旦结果能确定便不执行后面的运算，为了省时开发中多用后者
注意if(x=true)和if(x==true)
 ==对于基本数据类型，比较的是基本数据类型的值，对于引用数据类型，比较的是地址值
```

### 位运算

```java
//最高效的计算 2*8 2<<3 或 8<<2
>>：有符号右移，符号位不变
>>>：无符号右移，最高位补0
```

## 三元运算符

```java
Object o1 = true ? 1: 2.0;//1自动提升为double
System.out.println(o1);// 1.0
```

# 流程控制

## if-else

```java
//if没被{}起来的时候，else服从就近原则
```

## switch-case

```java
switch 结构中的表达式，只能是如下6种： byte short char int 枚举 String
default 放在第一行也要加 break 才不执行余下的代码
```

```java
//为达成目的，有时候可以不在 case 后加 break ，例如求某一天是一年的第几天
import java.util.Scanner;
class SwitchCaseExer {
    public static void main(String[] args) {        
        Scanner scan = new Scanner(System.in);
        System.out.println("请输入year：");
        int year = scan.nextInt();
        System.out.println("请输入month：");
        int month = scan.nextInt();
        System.out.println("请输入day：");
        int day = scan.nextInt();
        //定义一个变量来保存总天数
        int sumDays = 0;
        switch(month){
        case 12:
            sumDays += 30;
        case 11:
            sumDays += 31;
        case 10:
            sumDays += 30;
        case 9:
            sumDays += 31;
        case 8:
            sumDays += 31;
        case 7:
            sumDays += 30;
        case 6:
            sumDays += 31;
        case 5:
            sumDays += 30;
        case 4:
            sumDays += 31;
        case 3:
            //判断year是否是闰年
            sumDays += ((year % 4 == 0 && year % 100 != 0 ) || year % 400 == 0)?29:28;
        case 2:
            sumDays += 31;
        case 1:
            sumDays += day;
        }
        System.out.println(year + "年" + month + "月" + day + "日是当年的第" + sumDays + "天");
    }
}
```

## Loop

```java
 //读入未知个数
 for(;;)
 while(true)
```

```java
 break continue 后面不能跟语句，否则编译报错
 break continue 默认作用包裹它们的最近一层循环
 lable:for ……………… break/continue lable//作用lable对应循环
 //输出质数
  label:for(int i=3;i<=100;i++){ 
                     for(int j=2;j<=Math.sqrt(i);j++){ 
                         if(i%j==0)continue lable;
                     } System.out.println(i);
              }
```

# 数组

## 初始化

```java
 //数组长度一旦确定就不可修改
 //1.1 静态初始化:数组的初始化和数组元素的赋值操作同时进行
 int[] arr = new int[]{1,2,3,4,5};//可以省略new int[]
 //1.2动态初始化:数组的初始化和数组元素的赋值操作分开进行
 String[] names = new String[5];
 int[] ids;//声明
 ids = new int[]{1001,1002,1003,1004};//不能省略new int[]
 int [] arr=new int[3];
 arr[0]=1;
 System.out.println(arr[0]);//1
 arr=new int[4];//覆盖掉原来的arr
 System.out.println(arr[0]);//0
```

### 数组元素的默认初始化值

```java
 数组元素是整型： 0
 数组元素是浮点型： 0.0
 数组元素是 char 型： 0(码值)或'\u0000'，而非'0'
 数组元素是 boolean 型： false
 数组元素是引用数据类型： null
 数组元素的默认初始化值 
         * 针对于初始化方式一：比如：int[][] arr = new int[4][3]; 
         * 外层元素的初始化值为：地址值 
         * 内层元素的初始化值为：与一维数组初始化情况相同 
 
         * 针对于初始化方式二：比如：int[][] arr = new int[4][]; 
         * 外层元素的初始化值为：null 
         * 内层元素的初始化值为：不能调用，否则报错。
 int [][] arr=new int[3][4];
 System.out.println(arr);//[[I@54bedef2,"[["表示维数，"I"表示数据类型，"54bedef2"表示地址
 System.out.println(arr[0]);//[I@5caf905d
 System.out.println(arr[0][0]);//0
 int [][] arr1=new int[3][];
 System.out.println(arr1[0]);//null
 System.out.println(arr1[0][0]);//报错
```

## 数组赋值

```java
 array2=array1;//将array1的地址给了array2，改变array2的元素将改变array1
```

## 排序
[[Java算法#排序|排序]]

# 面向对象

## 类的成员

### 对象

#### 匿名对象

```java
  new Person().name();//匿名对象，可以直接调用变量或函数
  //匿名对象的使用
  PoneMall mall = new PhoneMall();
  mall.show(new Phone());     
  class PhoneMall{
      public void show(Phone phone){
          phone.sendEmail();
          phone.playGame();
      }   
  }
```
### 方法

#### 重载

```java
/*
   方法的重载（overload）  loading...
  
	1.定义：在同一个类中，允许存在一个以上的同名方法，只要它们的参数个数或者参数类型不同即可。    
	2. 举例：
    Arrays类中重载的sort() / binarySearch()
   
	3.判断是否是重载：
    跟方法的权限修饰符、返回值类型、形参变量名、方法体都没有关系！
     
	4. 在通过对象调用方法时，如何确定某一个指定的方法：
      方法名 ---> 参数列表
  */
 public void getSum(int i,int j){
     System.out.println("1");
 }
 //如下的3个方法不能与上述方法构成重载
 public int getSum(int i,int j){
     return 0;
 }   
 public void getSum(int m,int n){
 }   
 private void getSum(int i,int j){   
 }
```
####  可变个数形参

```java
 //可接受不同的形参个数(包括0个)，与本类中方法名相同，形参不同的其他方法构成重载，优先调用固定参数个数的方法，与形参类型相同的数组不构成重载，方法中最多只能有一个可变个数形参，且必须写在末尾。
 public void show(String...strs ) {
 }
```
#### 参数传递

```java
Person p1=new Person("小明");
Person p2=p1;//将p1的地址给了p2，p2相当于p1的别名，改变p2的变量将改变p1
的变量
Person p1=new Person("小红");//p2仍是小明
```

### 构造器
一旦我们显式的定义了构造器，系统就不会提供默认构造器
#### 使用 this 调用构造器
1. 我们在类的构造器中，可以显式的使用"this(形参列表)"方式，调用本类中指定的其他构造器
2. 构造器中不能通过"this(形参列表)"方式调用自己
3. 如果一个类中有 $n$ 个构造器，则最多有 $n - 1$ 构造器中使用了"this(形参列表)"
4. 规定："this(形参列表)"必须声明在当前构造器的首行
5. 构造器内部，最多只能声明一个"this(形参列表)"，用来调用其他的构造器
        
```java
this();
 this(Strig name,int age);
 method(this);//this是当前对象，可以作为参数
```

## 修饰符

### static

#### 静态属性（类变量）

1. 静态变量随着类而加载，可以通过类直接调用静态变量
2. 静态变量加载先于对象创建
3. 由于类只会加载一次，则静态变量在内存中也只会存在一份：存在方法区的静态域中
```java
class Chinese{
                 static String nation;
                 String name;
                 public void eat(){}
                 public static void walk(){}
                 public static void show(){
                     System.out.println("我是一个中国人！");
                     //不能调用非静态的结构
                     //eat();
                     //name = "Tom";
                     //可以调用静态的结构
                     System.out.println(Chinese.nation);
                     walk();
             }
             }
             c1.nation="CN";
             System.out.println(c2.nation);//"CN"，多个对象共享一个变量
             System.out.println(Chinese.nation);//"CN"
         Chinese.nation="中国";
         Chinese.show();  
```

#### 静态方法

1. 静态变量随着类而加载，可以通过类直接调用静态变量
2. 静态方法只能调用静态方法和属性
3. 在静态的方法内，不能使用this关键字、super关键字

#### 代码块

1. 代码块的作用：用来初始化类、对象
2. 代码块如果用修饰关键字的话，只能用static
3. 静态代码块
    1. 内部可以有输出语句
    2. 随着类加载而执行，只执行一次
    3. 作用：初始化类的信息
    4. 如果一个类中定义了多个静态代码块，则按照声明的先后顺序执行
    5. 静态代码块的执行要优先于非静态代码块的执行
    6. 静态代码块内只能调用静态的属性、静态的方法，不能调用非静态的结构
4. 非静态代码块
    1. 内部可以有输出语句
    2. 随着对象创建而执行，每创建一个对象就执行一次
    3. 作用：可以在创建对象时，对对象的属性等进行初始化
    4. 如果一个类中定义了多个非静态代码块，则按照声明的先后顺序执行
    5. 非静态代码块内可以调用静态的属性、静态的方法，或非静态的属性、非静态的方法

#### 属性赋值

可以对属性赋值的位置（按先后顺序）：
-  ①默认初始化
-  ②显式初始化/⑤在代码块中赋值
-  ③构造器中初始化
-  ④有了对象以后，可以通过"对象.属性"或"对象.方法"的方式，进行赋值

#### 内部类
1. Java中允许将一个类A声明在另一个类B中，则类A就是内部类，类B称为外部类
2. 内部类的分类：成员内部类（静态、非静态） vs 局部内部类(方法内、代码块内、构造器内)
3. 成员内部类：
    1. 一方面，作为外部类的成员：
        1. 调用外部类的结构
        2. 可以被 static 修饰
        3. 可以被4种不同的权限修饰
    2. 另一方面，作为一个类：
        1. 类内可以定义属性、方法、构造器等
        2. 可以被 final 修饰，表示此类不能被继承。言外之意，不使用 final, 就可以被继承
        3. 可以被 abstract 修饰
4. 关注如下的3个问题
    1. 如何实例化成员内部类的对象
    2. 如何在成员内部类中区分调用外部类的结构
    3. 开发中局部内部类的使用 见《InnerClassTest1.java》

```java
class Person{

     static class Dog{
     public void show(){}
     }
     class Bird{
     	public void sing(){}
     }
}


public class InnerClassTest {

	public static void main(String[] args){
	
		//创建Dog实例(静态的成员内部类):
		Person.Dog dog = new Person.Dog();
		dog.show();
		
		//创建Bird实例(非静态的成员内部类):
		//Person.Bird bird = new Person.Bird();//错误的
		Person p = new Person();
		Person.Bird bird = p.new Bird();
		bird.sing();
	}
}
```

### final

- final 可以修饰类、方法、变量、对象
- final 类不能被继承，比如 String、System、StringBuffer
- final 方法不能被重写，比如 Object 中的 getClass()
- final 变量称为“常量”
    1. final 属性可以考虑赋值的位置有：显示初始化、代码块、构造器
    2. final 修饰局部变量，形参
    3. static final  全局常量

### abstract

- abstract 修饰类：抽象类
	1. 不能实例化
	2. 出现了在一定有构造器，便于子类实例化，开发中都会提供构造器
- abstract 修饰方法
	1. 抽象方法只有声明，没有方法体
	2. 抽象方法只能放在抽象类中，抽象类中可以没有抽象方法
	3. 子类重写了父类中所有的抽象方法，才能实例化，否则子类也是一个抽象类
- abstract 使用的注意点
	1. abstract 不能修饰属性、构造器
	2. abstract 不能修饰私有方法，静态方法

## 继承

- object类是所有类的父类object 没有属性，构造器只有一个空参构造器
- 父类中声明为private的成员能被子类继承但不能被直接调用
- 子类构造器没有显式调用父类的某一个构造器时，默认在第一行调用父类空参构造器，所以此情况下父类必须含有空参构造器，如果父类无空参构造器，子类构造器必须显式调用父类的某一个有参构造器
- 初始化子类实例时，先从上到下初始化父类静态属性和静态代码块，再从上到下初始化子类静态属性和静态代码块，再从上到下初始化父类非静态属性和代码块，再从上到下初始化子类非静态属性和代码块，此期间调用父类被重写的方法时实际调用子类方法。


### 重写
#### 重写的原则
1. 子类重写的方法名和形参列表与父类相同
2. 子类重写的方法的权限修饰符不小于对应父类方法的权限修饰符
3. 子类不能重写父类中权限为private的方法
4. 返回值类型
	- 父类中被重写方法返回值类型是void，则子类重写方法返回值类型必须是void
	- 父类中被重写方法返回值类型是A类型，则子类重写方法返回值类型可以是A类型和A的子类
	- 父类中被重写方法返回值类型是基本数据类型，则子类重写方法返回值类型必须是相同的基本数据类型
5. 父类中被重写方法抛出的异常类型不大于父类被重写方法的异常类型
6. 子类和父类中的同名方法要么都生成非static方法（考虑重写），要么都声明成static方法（不是重写）
- equals()默认比较地址值，有时需要重写
- toString()默认是地址值，需要重写
#### super关键字的使用

```java
         //子类中定义了同名的属性后，子类就有两个同名属性
     name 或 this.name //调用子类属性
         super.name//调用父类属性
         //子类重写了父类方法后，我们想在子类中调用父类中被重写的方法必须使用
         super.method
         //与this类似，在子类构造器中调用“super(形参列表)”的方式，调用父类的构造器，且只能放在首行
         //super(形参列表)与this(形参列表) 只能有一个
         //构造器的首行没有super(形参列表)与this(形参列表) ，则默认调用了父类中的空参构造器
         //多个构造器中，至少有一个类的构造器使用了super(形参列表)
```

### 多态
```java
         定义：父类引用指向子类的对象
         Person p = new student();
         p.eat();//在编译期间，只能调用父类的方法，但实际执行的是子类重写的方法
         多态性只适用于方法，不适用于属性
         不能调用子类中特有的方法和属性
         student s = (student) p;//使用强转将声明为父类型的子类对象转化为子类对象
         强转可能出现异常，使用instanceof关键字来判断
         a instanceof A;//a是A定的实例，则返回 true,否则返回 false
         B 是 A 的父类，若 a instanceof A 返回 true，则 a instanceof B 返回 true
         //例子
         class Base {
             int count = 10;
         
             public void display() {
                 System.out.println(this.count);
             }
         }
         
         class Sub extends Base {
             int count = 20;
             
             public void display() {
                 System.out.println(this.count);
             }
         }
         
         public class FieldMethodTest {
             public static void main(String[] args) {
                 Sub s = new Sub();
             System.out.println(s.count);//20
                 s.display();//20
                 
                 Base b = s;//多态性
                 //==：对于引用数据类型来讲，比较的是两个引用数据类型变量的地址值是否相同
                 System.out.println(b == s);//true
                 System.out.println(b.count);//10
                 b.display();//20
             }
         }
```

## interface

1. 接口使用 interface 定义
2. Java中，接口和类是并列的两个结构
3. 如何定义接口：定义接口中的成员
    - JDK7及以前：只能定义全局常量和抽象方法，但是书写时，可以省略不写修饰符
        - 全局常量: public static final (可以省略 public static final
    - 抽象方法: public abstract (可以省略 abstract)
    - JDK8：除了定义全局常量和抽象方法之外，还可以定义静态方法(只能通过接口来调用)、默认方法(通过实现类的对象。可以调用接口中的默认方法)。除了定义全局常量和抽象方法之外，还可以定义静态方法、默认方法
4. 接口中不能定义构造器的！意味着接口不可以实例化
5. Java开发中，接口通过让类去实现(implements)的方式来使用.
    - 如果实现类覆盖了接口中的所有抽象方法，则此实现类就可以实例化
    - 如果实现类没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类
6. Java类可以实现多个接口 --->弥补了Java单继承性的局限，格式: class AA extends BB implements CC,DD,EE
7. 接口与接口之间可以继承，而且可以多继承
8. 接口的具体使用，体现多态性
9. 接口，实际上可以看做是一种规范

## 匿名子类与匿名对象

```java
 //非匿名的类非匿名的对象
     Worker worker = new Worker();
     method1(worker);
 
 //非匿名的类匿名的对象        
     method1(new Worker());
         
 //创建了一匿名子类的对象：p
     Person p = new Person(){
         @Override
         public void eat() {
                 System.out.println("吃东西");
         }
         @Override
         public void breath() {
             System.out.println("好好呼吸");
         }           
     };      
     method1(p);
         
 //创建匿名子类的匿名对象
     method1(new Person(){
         @Override
         public void eat() {
             System.out.println("吃好吃东西");
         }
         @Override
         public void breath() {
             System.out.println("好好呼吸新鲜空气");
         }
     });
```

```java
 //1.创建了接口的非匿名实现类的非匿名对象
         Flash flash = new Flash();
         com.transferData(flash);
         
 //2. 创建了接口的非匿名实现类的匿名对象
     com.transferData(new Printer());
     
 //3. 创建了接口的匿名实现类的非匿名对象
     USB phone = new USB(){
         @Override
         public void start() {
             System.out.println("手机开始工作");
         }
         @Override
         public void stop() {
             System.out.println("手机结束工作");
         }       
     };
     com.transferData(phone);
     
 //4. 创建了接口的匿名实现类的匿名对象   
     com.transferData(new USB(){
         @Override
         public void start() {
             System.out.println("mp3开始工作");
         }
         @Override
         public void stop() {
             System.out.println("mp3结束工作");
         }
     });
```

# main

1. main()方法作为程序的入口
2. main()方法也是一个普通的静态方法
3. main()方法可以作为我们与控制台交互的方式。（之前：使用Scanner）

# String

- String能和八种基本类型做运算，且只能连接(+)运算，结果仍是String，String不能强制转换
- 使用字面值定义的String，相同的字符串有相同的地址值，
- 对于有两个相同地址值的String，对其中一个1String进行修改时重新造了一个String(与没改变得String具有不同地址值)，另外一个的字符串不变
- 常量与常量拼接的结果仍是常量，常量只有一个地址值1

```Java
 String s="";//通过
 char c='';//不行，必须且只能放一个字符
 char c='a';
 int i=10;
 String s="hello";
 System.out.println(c+i+s);//107hello
 System.out.println(s+(c+i));//hello107
 System.out.println(s+c+i);//hellloa10
 System.out.println(s+i+c);//helllo10a
 "\t"//tab键 String类型
 String.equals("String");
 charAt(int index)//string的某个字符
```

# 包装类

## 基本数据类型和其包装类相互转换(自动拆箱和装箱)

```java
 int num=10;
 Integer Num=num;
 
 Integer Num1=11;
 int num1=Num1;
 
 Integer 内部定义了 IntegerCache 结构，IntegerCache 中定义了 Integer[]，保存了从 -128 ~ 127 范围的整数。如果我们使用自动装箱的方式，给 Integer 赋值的范围在 -128 ~ 127 范围内时，可以直接使用数组中的元素，不用再去 new 了。目的：提高效率。   
 Integer m = 1;
 Integer n = 1;
 System.out.println(m == n);//true
 
 Integer x = 128;//相当于new了一个Integer对象
 Integer y = 128;//相当于new了一个Integer对象
 System.out.println(x == y);//false
```

## 基本数据类型及其包装类与String相互转化

```java
 String str1="123";
 int num2=Integer.parseInt(str1);
 
 int num3=12;
 String str2=String.valueOf(num3);
```

# collection
[[Java数据结构]]
## list


## set

### 向HashSet中添加元素的过程

当向 HashSet 集合中存入一个元素时，HashSet 会调用该对象的 hashCode() 方法 来得到该对象的 hashCode 值，然后根据 hashCode 值，通过某种散列函数决定该对象 在 HashSet 底层数组中的存储位置。（这个散列函数会与底层数组的长度相计算得到在 数组中的下标，并且这种散列函数计算还尽可能保证能均匀存储元素，越是散列分布， 该散列函数设计的越好）

- 如果两个元素的hashCode()值相等，会再继续调用equals方法，如果equals方法结果 为true，添加失败；如果为false，那么会保存该元素，但是该数组的位置已经有元素了， 那么会通过链表的方式继续链接。
- 如果两个元素的 equals() 方法返回 true，但它们的 hashCode() 返回值不相 等，hashSet 将会把它们存储在不同的位置，但依然可以添加成功。

![setAdd](https://gitee.com/weinixiong97/chrome-bookmark/raw/master/Image/setAdd.png)

```java
  HashSet set = new HashSet();
  Person p1 = new Person(1001,"AA"); 
  Person p2 = new Person(1002,"BB");
  set.add(p1); 
  set.add(p2); 
  p1.name = "CC"; //原来p1位置现在是新的p1(1001,"cc")
  set.remove(p1);//移除失败，因为要移除一个元素，remove中的对象得hash值和属性必须与set中某一个一样，但是set中的p1(1001,"cc")的hash值是根据p1(1001,"AA")算得的，所以p1移除失败
  System.out.println(set);//两个
  set.add(new Person(1001,"CC"));//三个 
  System.out.println(set); 
  set.add(new Person(1001,"AA"));//四个，这个person与p1以链表的方式链接
  System.out.println(set);
```


# IO流

## 键盘读入

```java
 Scanner scan=new Scanner(System.in);
 int n=scan.nextInt();
 //Scanner不能获取char
```

# 多线程

# 异常处理

## Error

是Java 虚拟机无法解决的严重问题，我们不进行处理，而是修改程序解决问题

```java
  public class ErrorTest {
      public static void main(String[] args) {
          //1.栈溢出：java.lang.StackOverflowError
  //      main(args);
          //2.堆溢出：java.lang.OutOfMemoryError 
          Integer[] arr = new Integer[1024*1024*1024];        
      }
  }
```

## Exception

可以进行异常处理，分为以下两种异常

### 编译时异常

```java
  File file = new File("hello.txt");
  FileInputStream fis = new FileInputStream(file);
  int data = fis.read();
  while(data != -1){
      System.out.print((char)data);
      data = fis.read();
  }
  fis.close();
```

### 运行时异常

```java
  //空指针异常
  int[] arr = null;
  System.out.println(arr[10]);
  
  //角标越界异常
  int[] arr = int[10];
  System.out.println(arr[10]);
  
  //类型转换异常
  Object obj = new Date();
  String str = (String) obj;
  
  ////NumberFormatException
  String str = "123";
  str = "abc";
  int num = Integer.parseInt(str);
  
  //输入不匹配
  Scanner scanner = new Scanner(System.in);
  int score = scanner.nextInt();//输入非int
  System.out.println(score);
  scanner.close();
  
  //算数异常
  int a=10;
  int b=0;
  System.out.println(a/b);
```

### 处理Exception

#### 异常处理方式一

```java
  finally 可写可不写，但在某些情况下，JVM不能回收资源，就需要在 finally 中手动释放
  try一旦出现异常，就会生成一个异常对象去 catch 匹配
  一旦匹配到异常就进行处理，处理完毕后如果没有 finally 就继续执行剩下的代码
  catch 中的异常如果没有子父类关系，就没有放置顺序要求，否则父类必须放在子类下边
  常用异常处理方式：1 String getMessage()，2 printStackTrace()
  在 try 中声明的变量，在出了 try 结构后就不能被调用
  try-catch-finally 结构可以嵌套
  try{
      //可能出现的异常
  }
  catch(异常类型1 e1){
      //处理异常的方式1
      e1.printStackTrace();
  }
  catch(异常类型2 e2){
      //处理异常的方式2
      String getMessage();
      e2.getMessage();
  }
  catch(异常类型3 e3){
      //处理异常的方式3
  }
  ......
  finally{
      //一定会执行的代码
  }
```

#### 异常处理方式二

"throws + 异常类型"写在方法的声明处。指明此方法执行时，可能会抛出的异常类型。一旦当方法体执行时，出现异常，仍会在异常代码处生成一个异常类的对象，此对象满足throws后异常类型时，就会被抛出。异常代码后续的代码，就不再执行！

```java
  public void method() throws Exception1{
  }
```

#### 异常处理方式选择

1. 如果父类方法没用throws方式处理异常，总类重写的方法就不能用throws，如多子类重写方法要处理异常，就要用try-catch-finally
2. 如果方法调用是递进式的，建议用throws方式处理异常

```java
  public class ReturnExceptionDemo {
      static void methodA() {
          try {
              System.out.println("进入方法A");
              throw new RuntimeException("制造异常");
          } finally {
              System.out.println("用A方法的finally");
          }
      }
  
      static void methodB() {
          try {
              System.out.println("进入方法B");
              return;
          } finally {
              System.out.println("调用B方法的finally");
          }
      }
  
      public static void main(String[] args) {
          try {
              methodA();
          } catch (Exception e) {
              System.out.println(e.getMessage());
          }                   
          methodB();
      }
  }
  //结果 
  /*  进入方法A
      用A方法的finally
      制造异常
      进入方法B
      调用B方法的finally */
```

# 设计模式

## 单例设计模式

是指用一定方法使得某个类在整个软件中只有一个实例对象，有以下两种实现方式

### 懒汉式

线程不安全，延迟对象的创建，减少加载时间
#### 线程安全的懒汉式

##### 使用线程锁

```java
  //懒汉式
  class Order{
		//1.私有化类的构造器
		private Order(){        
		}
		//2.声明当前类对象，没有初始化
		//4.此对象也必须声明为static的
		private static Order instance = null;
		//3.声明public、static的返回当前类对象的方法
		public static Order getInstance(){
			 if(instance == null){
					synchronized(Order.class){
						 if(instance == null)
						instance = new Order(); 
					}                  
			 }
			 return instance;
		}   
  }
```

##### 使用内部类

```java
public class Singleton {
	 private Singleton(){
	 }
	 private static class Inner {
		  private static final Singleton instance = new Singleton();
	 }
	 public static Singleton getInstance() {
		  return Inner.instance;
	 }
}
```

### 饿汉式

线程安全，但是加载时间过长

```java
  //饿汉式
  class Bank{
      
      //1.私有化类的构造器
      private Bank(){     
      }
      
      //2.内部创建类的对象
      //4.要求此对象也必须声明为静态的
      private static Bank instance = new Bank();
   
      //3.提供公共的静态的方法，返回类的对象
      public static Bank getInstance(){
          return instance;
      }
  }
```

