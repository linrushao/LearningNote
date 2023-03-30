# Java基础与进阶

## 1. Java概述

**1.1 Java语言发展史（了解）**

语言：人与人交流沟通的表达方式

计算机语言：人与计算机之间进行信息交流沟通的一种特殊语言

Java语言是美国Sun公司（Stanford University Network）在1995年推出的计算机语言

Java之父：詹姆斯·高斯林（James Gosling）

2009年，Sun公司被甲骨文公司收购，oracle官网：[https://www.oracle.com](https://www.oracle.com/) 

**1.2 Java语言跨平台原理（理解）**

Java程序并非是直接运行的，Java编译器将Java源程序==编译==成与平台无关的字节码文件(class文件)，然后由Java虚拟机（JVM）对字节码文件解释==执行==。所以在不同的操作系统下，只需安装不同的Java虚拟机即可实现java程序的跨平台。

**1.3 JRE和JDK（记忆）**

| 参数                            | 说明                                                |
| ------------------------------- | --------------------------------------------------- |
| JVM（Java Virtual Machine）     | Java虚拟机                                          |
| JRE（Java Runtime Environment） | Java运行环境，包含了JVM和Java的核心类库（Java API） |
| JDK（Java Development Kit）     | 称为Java开发工具，包含了JRE和开发工具               |

总结：我们只需安装JDK即可，它包含了java的运行环境和虚拟机。

**1.3.1 JDK的安装目录介绍**

| 目录名称 | 说明                                           |
| -------- | ---------------------------------------------- |
| bin      | JDK的各种工具命令。javac和java就放在这个目录。 |
| conf     | JDK的相关配置文件。                            |
| include  | 一些平台特定的头文件。                         |
| jmods    | JDK的各种模块。                                |
| legal    | JDK各模块的授权文档。                          |
| lib      | JDK工具的一些补充JAR包。                       |

**1.4 Path环境变量的配置（应用）**

**1.4.1 为什么配置环境变量**

开发Java程序，需要使用JDK提供的开发工具（比如javac.exe、java.exe等命令），而这些工具在JDK的安装目录的bin目录下，如果不配置环境变量，那么这些命令只可以在该目录下执行。我们不可能把所有的java文件都放到JDK的bin目录下，所以配置环境变量的作用就是可以使bin目录下的java相关命令可以在任意目录下使用。

**1.5 Java程序开发运行流程**

开发Java程序，需要三个步骤：编写程序，编译程序，运行程序。

**1.6 HelloWorld案例常见问题（理解）**

**1.6.1 BUG**

在电脑系统或程序中，隐藏着的一些未被发现的缺陷或问题统称为bug（漏洞）。

**1.6.2 HelloWorld案例常见问题**

1、非法字符问题。Java中的符号都是英文格式的。

2、大小写问题。Java语言对大小写敏感（区分大小写）。

3、在系统中显示文件的扩展名，避免出现HelloWorld.java.txt文件。

4、编译命令后的java文件名需要带文件后缀.java

5、运行命令后的class文件名（类名）不带文件后缀.class

## 2. java基础语法

**2.1 注释（理解）**

注释是对代码的解释和说明文字，可以提高程序的可读性，因此在程序中添加必要的注释文字十分重要。Java中的注释分为三种：

单行注释。单行注释的格式是使用//，从//开始至本行结尾的文字将作为注释文字。

~~~java
// 这是单行注释文字
~~~

多行注释。多行注释的格式是使用/* 和 */将一段较长的注释括起来。

~~~java
/*
这是多行注释文字
这是多行注释文字
这是多行注释文字
*/
注意：多行注释不能嵌套使用。
~~~

文档注释。文档注释以`/**`开始，以`*/`结束。

**2.2 关键字（理解）**

关键字是指被java语言赋予了特殊含义的单词。

关键字的特点：

- 关键字的字母全部==小写==。
- 常用的代码编辑器对关键字都有高亮显示，比如现在我们能看到的public、class、static等。

**2.3 常量（应用）**

常量：在程序运行过程中，其值==不可以发生改变==的量。

Java中的常量分类：

​	字符串常量  用双引号括起来的多个字符（可以包含0个、一个或多个），例如"a"、"abc"、"中国"等

​	整数常量  整数，例如：-10、0、88等

​	小数常量  小数，例如：-5.5、1.0、88.88等

​	字符常量  用单引号括起来的一个字符，例如：'a'、'5'、'B'、'中'等

​	布尔常量  布尔值，表示真假，只有两个值true和false

​	空常量  一个特殊的值，空值，值为null

除空常量外，其他常量均可使用输出语句直接输出。

~~~java
public class Demo {
    public static void main(String[] args) {
        System.out.println(10); // 输出一个整数
        System.out.println(5.5); // 输出一个小数
        System.out.println('a'); // 输出一个字符
        System.out.println(true); // 输出boolean值true
        System.out.println("欢迎来到"); // 输出字符串
    }
}
~~~



**2.4 数据类型（记忆、应用）**

**2.4.1 计算机存储单元**

我们知道计算机是可以用来存储数据的，但是无论是内存还是硬盘，计算机存储设备的最小信息单元叫“位（bit）”，我们又称之为“比特位”，通常用小写的字母”b”表示。而计算机中最基本的存储单元叫“字节（byte）”，

通常用大写字母”B”表示，字节是由连续的8个位组成。

除了字节外还有一些常用的存储单位，其换算单位如下：

1B（字节） = 8bit

1KB = 1024B

1MB = 1024KB

1GB = 1024MB

1TB = 1024GB

**2.4.2 Java中的数据类型**

Java是一个强类型语言，Java中的数据必须明确数据类型。在Java中的数据类型包括==基本数据类型==和==引用数据类型==两种。

Java中的基本数据类型：

| 数据类型 | 关键字       | 内存占用 | 取值范围                                                     |
| :------- | ------------ | -------- | :----------------------------------------------------------- |
| 整数类型 | byte         | 1        | -128~127                                                     |
|          | short        | 2        | -32768~32767                                                 |
|          | int(默认)    | 4        | -2的31次方到2的31次方-1                                      |
|          | long         | 8        | -2的63次方到2的63次方-1                                      |
| 浮点类型 | float        | 4        | 负数：-3.402823E+38到-1.401298E-45                                                              正数：1.401298E-45到3.402823E+38 |
|          | double(默认) | 8        | 负数：-1.797693E+308到-4.9000000E-324                                                        正数：4.9000000E-324   到1.797693E+308 |
| 字符类型 | char         | 2        | 0-65535                                                      |
| 布尔类型 | boolean      | 1        | true，false                                                  |

说明：

​	e+38表示是乘以10的38次方，同样，e-45表示乘以10的负45次方。

​	==在java中整数默认是int类型，浮点数默认是double类型==。

**2.5 变量（应用）**

**2.5.1 变量的定义**

变量：在程序运行过程中，其值可以发生改变的量。

从本质上讲，变量是内存中的一小块区域，其值可以在一定范围内变化。

变量的定义格式：

```java
数据类型 变量名 = 初始化值; // 声明变量并赋值
int age = 18;
System.out.println(age);
```

或者

```java
// 先声明，后赋值（使用前赋值即可）
数据类型 变量名;
变量名 = 初始化值;
double money;
money = 55.5;
System.out.println(money);
```

还可以在同一行定义多个同一种数据类型的变量，中间使用逗号隔开。但不建议使用这种方式，降低程序的可读性。

```java
int a = 10, b = 20; // 定义int类型的变量a和b，中间使用逗号隔开
System.out.println(a);
System.out.println(b);

int c,d; // 声明int类型的变量c和d，中间使用逗号隔开
c = 30;
d = 40;
System.out.println(c);
System.out.println(d);
```

变量的使用：通过变量名访问即可。

**2.5.2 使用变量时的注意事项**

1. 在同一对花括号中，变量名不能重复。
2. 变量在使用之前，必须初始化（赋值）。
3. 定义long类型的变量时，需要在整数的后面加L（大小写均可，建议大写）。因为整数默认是int类型，整数太大可能超出int范围。
4. 定义float类型的变量时，需要在小数的后面加F（大小写均可，建议大写）。因为浮点数的默认类型是double， double的取值范围是大于float的，类型不兼容。

**2.6 标识符（记忆、理解）**

标识符是用户编程时使用的名字，用于给类、方法、变量、常量等命名。

Java中标识符的组成规则：

​	由字母、数字、下划线“_”、美元符号“$”组成，第一个字符不能是数字。

​	不能使用java中的关键字作为标识符。	

​	标识符对大小写敏感（区分大小写）。

Java中标识符的命名约定：

​	小驼峰式命名：变量名、方法名

​		首字母小写，从第二个单词开始每个单词的首字母大写。

​	大驼峰式命名：类名

​		每个单词的首字母都大写。

​	另外，标识符的命名最好可以做到见名知意

​		例如：username、studentNumber等。

**2.7 类型转换（理解）**

在Java中，一些数据类型之间是可以相互转换的。分为两种情况：自动类型转换和强制类型转换。

自动类型转换：

​	把一个表示数据范围小的数值或者变量赋值给另一个表示数据范围大的变量。这种转换方式是自动的，直接书写即可。例如：

```java
double num = 10; // 将int类型的10直接赋值给double类型
System.out.println(num); // 输出10.0
```

强制类型转换：

​	把一个表示数据范围大的数值或者变量赋值给另一个表示数据范围小的变量。

​	强制类型转换格式：目标数据类型 变量名 = (目标数据类型)值或者变量;

​	例如：

```java
double num1 = 5.5;
int num2 = (int) num1; // 将double类型的num1强制转换为int类型
System.out.println(num2); // 输出5（小数位直接舍弃）
```

![图片1](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E5%9B%BE%E7%89%871.png)

说明：

1. char类型的数据转换为int类型是按照码表中对应的int值进行计算的。比如在ASCII码表中，'a'对应97。

```java
int a = 'a';
System.out.println(a); // 将输出97
```

2. 整数默认是int类型，byte、short和char类型数据参与运算均会自动转换为int类型。

```java
byte b1 = 10;
byte b2 = 20;
byte b3 = b1 + b2; 
// 第三行代码会报错，b1和b2会自动转换为int类型，计算结果为int，int赋值给byte需要强制类型转换。
// 修改为:
int num = b1 + b2;
// 或者：
byte b3 = (byte) (b1 + b2);
```

1. boolean类型不能与其他基本数据类型相互转换。

## 3. 运算符

**3.1 算术运算符（理解）**

**3.1.1 运算符和表达式**

运算符：对常量或者变量进行操作的符号

表达式：用运算符把常量或者变量连接起来符合java语法的式子就可以称为表达式。

​                    不同运算符连接的表达式体现的是不同类型的表达式。

举例说明：

```java
int a = 10;
int b = 20;
int c = a + b;
```

  +：是运算符，并且是算术运算符。

  a + b：是表达式，由于+是算术运算符，所以这个表达式叫算术表达式。

**3.1.2 算术运算符**

| 符号 | 作用 | 说明                         |
| ---- | ---- | ---------------------------- |
| +    | 加   | 参看小学一年级               |
| -    | 减   | 参看小学一年级               |
| *    | 乘   | 参看小学二年级，与“×”相同    |
| /    | 除   | 参看小学二年级，与“÷”相同    |
| %    | 取余 | 获取的是两个数据做除法的余数 |

注意：

/和%的区别：两个数据做除法，/取结果的商，%取结果的余数。

整数操作只能得到整数，要想得到小数，必须有浮点数参与运算。

~~~java
int a = 10;
int b = 3;
System.out.println(a / b); // 输出结果3
System.out.println(a % b); // 输出结果1
~~~

**3.1.3 字符的“+”操作**

char类型参与算术运算，使用的是计算机底层对应的十进制数值。需要我们记住三个字符对应的数值：

'a'  --  97		a-z是连续的，所以'b'对应的数值是98，'c'是99，依次递加

'A'  --  65		A-Z是连续的，所以'B'对应的数值是66，'C'是67，依次递加

'0'  --  48		0-9是连续的，所以'1'对应的数值是49，'2'是50，依次递加

~~~java
// 可以通过使用字符与整数做算术运算，得出字符对应的数值是多少
char ch1 = 'a';
System.out.println(ch1 + 1); // 输出98，97 + 1 = 98

char ch2 = 'A';
System.out.println(ch2 + 1); // 输出66，65 + 1 = 66

char ch3 = '0';
System.out.println(ch3 + 1); // 输出49，48 + 1 = 49
~~~

算术表达式中包含不同的基本数据类型的值的时候，整个算术表达式的类型会自动进行提升。

提升规则：

byte类型，short类型和char类型将被提升到int类型，不管是否有其他类型参与运算。

整个表达式的类型自动提升到与表达式中最高等级的操作数相同的类型

​       等级顺序：byte,short,char --> int --> long --> float --> double

例如：

~~~java
byte b1 = 10;
byte b2 = 20;
// byte b3 = b1 + b2; // 该行报错，因为byte类型参与算术运算会自动提示为int，int赋值给byte可能损失精度
int i3 = b1 + b2; // 应该使用int接收
byte b3 = (byte) (b1 + b2); // 或者将结果强制转换为byte类型
-------------------------------
int num1 = 10;
double num2 = 20.0;
double num3 = num1 + num2; // 使用double接收，因为num1会自动提升为double类型
~~~

tips：正是由于上述原因，所以在程序开发中我们很少使用byte或者short类型定义整数。也很少会使用char类型定义字符，而使用字符串类型，更不会使用char类型做算术运算。



**3.1.4 字符串的“+”操作**

当“+”操作中出现字符串时，这个”+”是字符串连接符，而不是算术运算。

~~~java
System.out.println("itheima"+ 666); // 输出：itheima666
~~~

在”+”操作中，如果出现了字符串，就是连接运算符，否则就是算术运算。当连续进行“+”操作时，从左到右逐个执行。

~~~java
System.out.println(1 + 99 + "年黑马"); // 输出：100年黑马
System.out.println(1 + 2 + "itheima" + 3 + 4); // 输出：3itheima34
// 可以使用小括号改变运算的优先级 
System.out.println(1 + 2 + "itheima" + (3 + 4)); // 输出：3itheima7
~~~

**3.2 赋值运算符（应用）**

赋值运算符的作用是将一个表达式的值赋给左边，左边必须是可修改的，不能是常量。

| 符号 | 作用       | 说明                  |
| ---- | ---------- | --------------------- |
| =    | 赋值       | a=10，将10赋值给变量a |
| +=   | 加后赋值   | a+=b，将a+b的值给a    |
| -=   | 减后赋值   | a-=b，将a-b的值给a    |
| *=   | 乘后赋值   | a*=b，将a×b的值给a    |
| /=   | 除后赋值   | a/=b，将a÷b的商给a    |
| %=   | 取余后赋值 | a%=b，将a÷b的余数给a  |

注意：

扩展的赋值运算符隐含了强制类型转换。

~~~java
short s = 10;
s = s + 10; // 此行代码报出，因为运算中s提升为int类型，运算结果int赋值给short可能损失精度

s += 10; // 此行代码没有问题，隐含了强制类型转换，相当于 s = (short) (s + 10);
~~~

**3.3 自增自减运算符（理解）**

| 符号 | 作用 | 说明        |
| ---- | ---- | ----------- |
| ++   | 自增 | 变量的值加1 |
| --   | 自减 | 变量的值减1 |

注意事项：

​	++和-- 既可以放在变量的后边，也可以放在变量的前边。

​	单独使用的时候， ++和-- 无论是放在变量的前边还是后边，结果是一样的。

​	参与操作的时候，如果放在变量的后边，先拿变量参与操作，后拿变量做++或者--。

​	参与操作的时候，如果放在变量的前边，先拿变量做++或者--，后拿变量参与操作。

​	最常见的用法：单独使用。

~~~java
int i = 10;
i++; // 单独使用
System.out.println("i:" + i); // i:11

int j = 10;
++j; // 单独使用
System.out.println("j:" + j); // j:11

int x = 10;
int y = x++; // 赋值运算，++在后边，所以是使用x原来的值赋值给y，x本身自增1
System.out.println("x:" + x + ", y:" + y); // x:11，y:10

int m = 10;
int n = ++m; // 赋值运算，++在前边，所以是使用m自增后的值赋值给n，m本身自增1
System.out.println("m:" + m + ", m:" + m); // m:11，m:11
~~~

练习：

~~~java
int x = 10;
int y = x++ + x++ + x++;
System.out.println(y); // y的值是多少？
/*
解析，三个表达式都是++在后，所以每次使用的都是自增前的值，但程序自左至右执行，所以第一次自增时，使用的是10进行计算，但第二次自增时，x的值已经自增到11了，所以第二次使用的是11，然后再次自增。。。
所以整个式子应该是：int y = 10 + 11 + 12;
输出结果为33。
*/
注意：通过此练习深刻理解自增和自减的规律，但实际开发中强烈建议不要写这样的代码！小心挨打！
~~~

**3.4 关系运算符（应用）**

关系运算符有6种关系，分别为小于、小于等于、大于、等于、大于等于、不等于。

| 符号 | 说明                                                    |
| ---- | ------------------------------------------------------- |
| ==   | a==b，判断a和b的值是否相等，成立为true，不成立为false   |
| !=   | a!=b，判断a和b的值是否不相等，成立为true，不成立为false |
| >    | a>b，判断a是否大于b，成立为true，不成立为false          |
| >=   | a>=b，判断a是否大于等于b，成立为true，不成立为false     |
| <    | a<b，判断a是否小于b，成立为true，不成立为false          |
| <=   | a<=b，判断a是否小于等于b，成立为true，不成立为false     |

注意事项：

​	关系运算符的结果都是boolean类型，要么是true，要么是false。

​	千万不要把“==”误写成“=”，"=="是判断是否相等的关系，"="是赋值。

~~~java
int a = 10;
int b = 20;
System.out.println(a == b); // false
System.out.println(a != b); // true
System.out.println(a > b); // false
System.out.println(a >= b); // false
System.out.println(a < b); // true
System.out.println(a <= b); // true

// 关系运算的结果肯定是boolean类型，所以也可以将运算结果赋值给boolean类型的变量
boolean flag = a > b;
System.out.println(flag); // 输出false
~~~

**3.5 逻辑运算符（应用）**

逻辑运算符把各个运算的关系表达式连接起来组成一个复杂的逻辑表达式，以判断程序中的表达式是否成立，判断的结果是 true 或 false。

| 符号 | 作用     | 说明                                         |
| ---- | -------- | -------------------------------------------- |
| &    | 逻辑与   | a&b，a和b都是true，结果为true，否则为false   |
| \|   | 逻辑或   | a\|b，a和b都是false，结果为false，否则为true |
| ^    | 逻辑异或 | a^b，a和b结果不同为true，相同为false         |
| !    | 逻辑非   | !a，结果和a的结果正好相反                    |

~~~java
//定义变量
int i = 10;
int j = 20;
int k = 30;

//& “与”，并且的关系，只要表达式中有一个值为false，结果即为false
System.out.println((i > j) & (i > k)); //false & false,输出false
System.out.println((i < j) & (i > k)); //true & false,输出false
System.out.println((i > j) & (i < k)); //false & true,输出false
System.out.println((i < j) & (i < k)); //true & true,输出true
System.out.println("--------");

//| “或”，或者的关系，只要表达式中有一个值为true，结果即为true
System.out.println((i > j) | (i > k)); //false | false,输出false
System.out.println((i < j) | (i > k)); //true | false,输出true
System.out.println((i > j) | (i < k)); //false | true,输出true
System.out.println((i < j) | (i < k)); //true | true,输出true
System.out.println("--------");

//^ “异或”，相同为false，不同为true
System.out.println((i > j) ^ (i > k)); //false ^ false,输出false
System.out.println((i < j) ^ (i > k)); //true ^ false,输出true
System.out.println((i > j) ^ (i < k)); //false ^ true,输出true
System.out.println((i < j) ^ (i < k)); //true ^ true,输出false
System.out.println("--------");

//! “非”，取反
System.out.println((i > j)); //false
System.out.println(!(i > j)); //!false，,输出true
~~~

**短路逻辑运算符**

| 符号 | 作用   | 说明                         |
| ---- | ------ | ---------------------------- |
| &&   | 短路与 | 作用和&相同，但是有短路效果  |
| \|\| | 短路或 | 作用和\|相同，但是有短路效果 |

在逻辑与运算中，只要有一个表达式的值为false，那么结果就可以判定为false了，没有必要将所有表达式的值都计算出来，短路与操作就有这样的效果，可以提高效率。同理在逻辑或运算中，一旦发现值为true，右边的表达式将不再参与运算。

- 逻辑与&，无论左边真假，右边都要执行。

- 短路与&&，如果左边为真，右边执行；如果左边为假，右边不执行。

- 逻辑或|，无论左边真假，右边都要执行。

- 短路或||，如果左边为假，右边执行；如果左边为真，右边不执行。

~~~java
int x = 3;
int y = 4;
System.out.println((x++ > 4) & (y++ > 5)); // 两个表达都会运算
System.out.println(x); // 4
System.out.println(y); // 5

System.out.println((x++ > 4) && (y++ > 5)); // 左边已经可以确定结果为false，右边不参与运算
System.out.println(x); // 4
System.out.println(y); // 4
~~~

**3.6 三元运算符（理解）**

三元运算符语法格式：

~~~java
关系表达式 ? 表达式1 : 表达式2;
~~~

解释：问号前面的位置是判断的条件，判断结果为boolean型，为true时调用表达式1，为false时调用表达式2。其逻辑为：如果条件表达式成立或者满足则执行表达式1，否则执行第二个。

举例：

~~~java
int a = 10;
int b = 20;
int c = a > b ? a : b; // 判断 a>b 是否为真，如果为真取a的值，如果为假，取b的值
~~~

三元运算符案例：

1、需求：动物园里有两只老虎，已知两只老虎的体重分别为180kg、200kg，请用程序实现判断两只老虎的体重是否相同。

~~~java
public class OperatorTest01 {
	public static void main(String[] args) {
		//1：定义两个变量用于保存老虎的体重，单位为kg，这里仅仅体现数值即可。
		int weight1 = 180;
		int weight2 = 200;	
		//2：用三元运算符实现老虎体重的判断，体重相同，返回true，否则，返回false。
		boolean b = weight1 == weight2 ? true : false;	
		//3：输出结果
		System.out.println("b:" + b);
	}
}
~~~

2、需求：一座寺庙里住着三个和尚，已知他们的身高分别为150cm、210cm、165cm，请用程序实现获取这三个和尚的最高身高。

~~~java
public class OperatorTest02 {
	public static void main(String[] args) {
		//1：定义三个变量用于保存和尚的身高，单位为cm，这里仅仅体现数值即可。
		int height1 = 150;
		int height2 = 210;
		int height3 = 165;	
		//2：用三元运算符获取前两个和尚的较高身高值，并用临时身高变量保存起来。
		int tempHeight = height1 > height2 ? height1 : height2;		
		//3：用三元运算符获取临时身高值和第三个和尚身高较高值，并用最大身高变量保存。
		int maxHeight = tempHeight > height3 ? tempHeight : height3;	
		//4：输出结果
		System.out.println("maxHeight:" + maxHeight);
	}
}
~~~

## 4. 数据输入（应用）

我们可以通过 Scanner 类来获取用户的输入。使用步骤如下：

1、导包。Scanner 类在java.util包下，所以需要将该类导入。导包的语句需要定义在类的上面。

~~~java
import java.util.Scanner; 
~~~

2、创建Scanner对象。

~~~java
Scanner sc = new Scanner(System.in);// 创建Scanner对象，sc表示变量名，其他均不可变
~~~

3、接收数据

 ~~~java
int i = sc.nextInt(); // 表示将键盘录入的值作为int数返回。
 ~~~

示例：

~~~java
import java.util.Scanner;
public class ScannerDemo {
	public static void main(String[] args) {
		//创建对象
		Scanner sc = new Scanner(System.in);
		//接收数据
		int x = sc.nextInt();
		//输出数据
		System.out.println("x:" + x);
	}
}
~~~

改写三个和尚案例，数据使用键盘录入。

~~~java
import java.util.Scanner;
public class ScannerTest {
	public static void main(String[] args) {
		//身高未知，采用键盘录入实现。首先导包，然后创建对象。
		Scanner sc = new Scanner(System.in);
		//键盘录入三个身高分别赋值给三个变量。
		System.out.println("请输入第一个和尚的身高：");
		int height1 = sc.nextInt();
		System.out.println("请输入第二个和尚的身高：");
		int height2 = sc.nextInt();
		System.out.println("请输入第三个和尚的身高：");
		int height3 = sc.nextInt();
		//用三元运算符获取前两个和尚的较高身高值，并用临时身高变量保存起来。
		int tempHeight = height1 > height2 ? height1 : height2;
		//用三元运算符获取临时身高值和第三个和尚身高较高值，并用最大身高变量保存。
		int maxHeight = tempHeight > height3 ? tempHeight : height3;
		//输出结果。
		System.out.println("这三个和尚中身高最高的是：" + maxHeight +"cm");
	}
}
~~~

## 5 流程控制语句（应用）

在一个程序执行的过程中，各条语句的执行顺序对程序的结果是有直接影响的。所以，我们必须清楚每条语句的执行流程。而且，很多时候要通过控制语句的执行顺序来实现我们想要的功能。

**5.1 流程控制语句分类**

​	顺序结构

​	分支结构(if, switch)

​	循环结构(for, while, do…while)

**5.2 顺序结构**

顺序结构是程序中最简单最基本的流程控制，没有特定的语法结构，按照代码的先后顺序，依次执行，程序中大多数的代码都是这样执行的。

顺序结构执行流程图：

![1545615769372](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/1545615769372.png)

**5.3 分支结构之if语句**

**if语句格式1**

~~~java
格式：
if (关系表达式) {
    语句体;	
}
~~~

执行流程：

①首先计算关系表达式的值

②如果关系表达式的值为true就执行语句体

③如果关系表达式的值为false就不执行语句体

④继续执行后面的语句内容

![1545616039363](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/1545616039363.png)

示例：

~~~java
public class IfDemo {
	public static void main(String[] args) {
		System.out.println("开始");	
		//定义两个变量
		int a = 10;
		int b = 20;	
		//需求：判断a和b的值是否相等，如果相等，就在控制台输出：a等于b
		if(a == b) {
			System.out.println("a等于b");
		}		
		//需求：判断a和c的值是否相等，如果相等，就在控制台输出：a等于c
		int c = 10;
		if(a == c) {
			System.out.println("a等于c");
		}		
		System.out.println("结束");
	}
}
~~~

**if语句格式2**

~~~java
格式：
if (关系表达式) {
    语句体1;	
} else {
    语句体2;	
}
~~~

执行流程：

①首先计算关系表达式的值

②如果关系表达式的值为true就执行语句体1

③如果关系表达式的值为false就执行语句体2

④继续执行后面的语句内容

![1545616221283](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/1545616221283.png)

示例：

~~~java
public class IfDemo02 {
	public static void main(String[] args) {
		System.out.println("开始");		
		//定义两个变量
		int a = 10;
		int b = 20;
		b = 5;	
		//需求：判断a是否大于b，如果是，在控制台输出：a的值大于b，否则，在控制台输出：a的值不大于b
		if(a > b) {
			System.out.println("a的值大于b");
		} else {
			System.out.println("a的值不大于b");
		}		
		System.out.println("结束");
	}
}
~~~

if语句案例：奇偶数

需求：任意给出一个整数，请用程序实现判断该整数是奇数还是偶数，并在控制台输出该整数是奇数还是偶数。

分析：

​	①为了体现任意给出一个整数，采用键盘录入一个数据

​	②判断整数是偶数还是奇数要分两种情况进行判断，使用if..else结构

​	③判断是否偶数需要使用取余运算符实现该功能 number % 2 == 0

​	④根据判定情况，在控制台输出对应的内容

~~~java
import java.util.Scanner;
public class IfTest01 {
	public static void main(String[] args) {
		//为了体现任意给出一个整数，采用键盘录入一个数据。(导包，创建对象，接收数据)
		Scanner sc = new Scanner(System.in);		
		System.out.println("请输入一个整数：");
		int number = sc.nextInt();	
		//判断整数是偶数还是奇数要分两种情况进行判断，使用if..else结构		
		//判断是否偶数需要使用取余运算符实现该功能 number % 2 == 0
		//根据判定情况，在控制台输出对应的内容
		if(number%2 == 0) {
			System.out.println(number + "是偶数");
		} else {
			System.out.println(number + "是奇数");
		}	
	}
}
~~~

**if语句格式3**

~~~java
格式：
if (关系表达式1) {
    语句体1;	
} else if (关系表达式2) {
    语句体2;	
} 
…
else {
    语句体n+1;
}
~~~

执行流程：

①首先计算关系表达式1的值

②如果值为true就执行语句体1；如果值为false就计算关系表达式2的值

③如果值为true就执行语句体2；如果值为false就计算关系表达式3的值

④…

⑤如果没有任何关系表达式为true，就执行语句体n+1。

![1545616667104](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/1545616667104.png)

示例：键盘录入一个星期数(1,2,...7)，输出对应的星期一，星期二，...星期日

~~~java
import java.util.Scanner;
public class IfDemo03 {
	public static void main(String[] args) {
		System.out.println("开始");
		// 需求：键盘录入一个星期数(1,2,...7)，输出对应的星期一，星期二，...星期日
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个星期数(1-7)：");
		int week = sc.nextInt();
		if(week == 1) {
			System.out.println("星期一");
		} else if(week == 2) {
			System.out.println("星期二");
		} else if(week == 3) {
			System.out.println("星期三");
		} else if(week == 4) {
			System.out.println("星期四");
		} else if(week == 5) {
			System.out.println("星期五");
		} else if(week == 6) {
			System.out.println("星期六");
		} else {
			System.out.println("星期日");
		}	
		System.out.println("结束");
	}
}
~~~

if语句格式3案例：

需求：小明快要期末考试了，小明爸爸对他说，会根据他不同的考试成绩，送他不同的礼物，假如你可以控制小明的得分，请用程序实现小明到底该获得什么样的礼物，并在控制台输出。

分析：

​	①小明的考试成绩未知，可以使用键盘录入的方式获取值

​	②由于奖励种类较多，属于多种判断，采用if...else...if格式实现

​	③为每种判断设置对应的条件

​	④为每种判断设置对应的奖励

~~~java
import java.util.Scanner;
public class IfTest02 {
	public static void main(String[] args) {
		//小明的考试成绩未知，可以使用键盘录入的方式获取值
		Scanner sc = new Scanner(System.in);	
		System.out.println("请输入一个分数：");
		int score = sc.nextInt();
		//由于奖励种类较多，属于多种判断，采用if...else...if格式实现
		//为每种判断设置对应的条件
		//为每种判断设置对应的奖励	
		//数据测试：正确数据，边界数据，错误数据
		if(score>100 || score<0) {
			System.out.println("你输入的分数有误");
		} else if(score>=95 && score<=100) {
			System.out.println("山地自行车一辆");
		} else if(score>=90 && score<=94) {
			System.out.println("游乐场玩一次");
		} else if(score>=80 && score<=89) {
			System.out.println("变形金刚玩具一个");
		} else {
			System.out.println("胖揍一顿");
		}
	}
}
~~~

**5.4 switch语句**

**5.1.1 switch语句结构（掌握）**

* 格式

  ```java
  switch (表达式) {
  	case 1:
  		语句体1;
  		break;
  	case 2:
  		语句体2;
  		break;
  	...
  	default:
  		语句体n+1;
  		break;
  }
  ```

* 执行流程：

  * 首先计算出表达式的值 
  * 其次，和case依次比较，一旦有对应的值，就会执行相应的语句，在执行的过程中，遇到break就会结 束。 
  * 最后，如果所有的case都和表达式的值不匹配，就会执行default语句体部分，然后程序结束掉。 

**5.1.2 switch语句练习-春夏秋冬（应用）**

* 需求：一年有12个月，分属于春夏秋冬4个季节，键盘录入一个月份，请用程序实现判断该月份属于哪个季节，并输出。 
* 运行结果：

```
春：3、4、5
夏：6、7、8
秋：9、10、11
冬：1、2、12
```

* 示例代码：

```java
public class Demo1 {
    public static void main(String[] args) {
        //键盘录入月份数据，使用变量接收
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个月份：");
        int month = sc.nextInt();
        //case穿透
        switch(month) {
            case 1:
            case 2:
            case 12:
                System.out.println("冬季");
                break;
            case 3:
            case 4:
            case 5:
                System.out.println("春季");
                break;
            case 6:
            case 7:
            case 8:
                System.out.println("夏季");
                break;
            case 9:
            case 10:
            case 11:
                System.out.println("秋季");
                break;
            default:
                System.out.println("你输入的月份有误");
        }
    }
}
```

* 注意：如果switch中得case，没有对应break的话，则会出现case穿透的现象。

**5.5 for循环**

**5.5.1 for循环结构（掌握）**

* 循环：

  循环语句可以在满足循环条件的情况下，反复执行某一段代码，这段被重复执行的代码被称为循环体语句，当反复 执行这个循环体时，需要在合适的时候把循环判断条件修改为false，从而结束循环，否则循环将一直执行下去，形 成死循环。 

* for循环格式：

```java
for (初始化语句;条件判断语句;条件控制语句) {
	循环体语句;
}
```

* 格式解释：

  * 初始化语句：  用于表示循环开启时的起始状态，简单说就是循环开始的时候什么样
  * 条件判断语句：用于表示循环反复执行的条件，简单说就是判断循环是否能一直执行下去
  * 循环体语句：  用于表示循环反复执行的内容，简单说就是循环反复执行的事情
  * 条件控制语句：用于表示循环执行中每次变化的内容，简单说就是控制循环是否能执行下去

* 执行流程：

  ①执行初始化语句

  ②执行条件判断语句，看其结果是true还是false

  ​             如果是false，循环结束

  ​             如果是true，继续执行

  ③执行循环体语句

  ④执行条件控制语句

  ⑤回到②继续

**5.5.2 for循环练习-输出数据（应用）**

* 需求：在控制台输出1-5和5-1的数据 
* 示例代码：

```java
public class ForTest01 {
    public static void main(String[] args) {
		//需求：输出数据1-5
        for(int i=1; i<=5; i++) {
			System.out.println(i);
		}
		System.out.println("--------");
		//需求：输出数据5-1
		for(int i=5; i>=1; i--) {
			System.out.println(i);
		}
    }
}
```

**5.5.3 for循环练习-求和（应用）**

* 需求：求1-5之间的数据和，并把求和结果在控制台输出 
* 示例代码：

```java
public class ForTest02 {
    public static void main(String[] args) {
		//求和的最终结果必须保存起来，需要定义一个变量，用于保存求和的结果，初始值为0
		int sum = 0;
		//从1开始到5结束的数据，使用循环结构完成
		for(int i=1; i<=5; i++) {
			//将反复进行的事情写入循环结构内部
             // 此处反复进行的事情是将数据 i 加到用于保存最终求和的变量 sum 中
			sum += i;
			/*
				sum += i;	sum = sum + i;
				第一次：sum = sum + i = 0 + 1 = 1;
				第二次：sum = sum + i = 1 + 2 = 3;
				第三次：sum = sum + i = 3 + 3 = 6;
				第四次：sum = sum + i = 6 + 4 = 10;
				第五次：sum = sum + i = 10 + 5 = 15;
			*/
		}
		//当循环执行完毕时，将最终数据打印出来
		System.out.println("1-5之间的数据和是：" + sum);
    }
}
```

* 本题要点：
  * 今后遇到的需求中，如果带有求和二字，请立即联想到求和变量
  * 求和变量的定义位置，必须在循环外部，如果在循环内部则计算出的数据将是错误的

**5.5.4 for循环练习-求偶数和（应用）**

* 需求：求1-100之间的偶数和，并把求和结果在控制台输出 }
* 示例代码：

```java
public class ForTest03 {
    public static void main(String[] args) {
		//求和的最终结果必须保存起来，需要定义一个变量，用于保存求和的结果，初始值为0
		int sum = 0;
		//对1-100的数据求和与1-5的数据求和几乎完全一样，仅仅是结束条件不同
		for(int i=1; i<=100; i++) {
			//对1-100的偶数求和，需要对求和操作添加限制条件，判断是否是偶数
			if(i%2 == 0) {
				sum += i;
			}
		}
		//当循环执行完毕时，将最终数据打印出来
		System.out.println("1-100之间的偶数和是：" + sum);
    }
}
```

5.5.5 for循环练习-水仙花（应用）

* 需求：在控制台输出所有的“水仙花数” 
* 解释：什么是水仙花数？
  * 水仙花数，指的是一个三位数，个位、十位、百位的数字立方和等于原数
    * 例如`153  3*3*3 + 5*5*5 + 1*1*1 = 153`
* 思路：
  1. 获取所有的三位数，准备进行筛选，最小的三位数为100，最大的三位数为999，使用for循环获取
  2. 获取每一个三位数的个位，十位，百位，做if语句判断是否是水仙花数
* 示例代码

```java
public class ForTest04 {
    public static void main(String[] args) {
		//输出所有的水仙花数必然要使用到循环，遍历所有的三位数，三位数从100开始，到999结束
		for(int i=100; i<1000; i++) {
			//在计算之前获取三位数中每个位上的值
			int ge = i%10;
			int shi = i/10%10;
			int bai = i/10/10%10;
			
			//判定条件是将三位数中的每个数值取出来，计算立方和后与原始数字比较是否相等
			if(ge*ge*ge + shi*shi*shi + bai*bai*bai == i) {
				//输出满足条件的数字就是水仙花数
				System.out.println(i);
			}
		}
    }
}
```

**5.5.6 for循环练习-统计水仙花数个数（应用）**

* 需求：统计“水仙花数”一共有多少个，并在控制台输出个数 
* 示例代码：

```java
public class ForTest05 {
    public static void main(String[] args) {
		//定义变量count，用于保存“水仙花数”的数量，初始值为0
		int count = 0;
		//输出所有的水仙花数必然要使用到循环，遍历所有的三位数，三位数从100开始，到999结束
		for(int i=100; i<1000; i++) {
			//在计算之前获取三位数中每个位上的值
			int ge = i%10;
			int shi = i/10%10;
			int bai = i/10/10%10;
			//在判定水仙花数的过程中，满足条件不再输出，更改为修改count的值，使count+1
			if(ge*ge*ge + shi*shi*shi + bai*bai*bai == i) {
				count++;
			}
		}
		//打印输出最终结果
		System.out.println("水仙花共有：" + count + "个");
    }
}
```

* 本题要点：
  * 今后如果需求带有统计xxx，请先想到计数器变量
  * 计数器变量定义的位置，必须在循环外部

**5.6 while循环**

**5.6.1 while结构（掌握）**

* while循环完整格式：

  ```java
  初始化语句;
  while (条件判断语句) {
  	循环体语句;
      条件控制语句;
  }
  ```

* while循环执行流程：

  ①执行初始化语句

  ②执行条件判断语句，看其结果是true还是false

  ​             如果是false，循环结束

  ​             如果是true，继续执行

  ③执行循环体语句

  ④执行条件控制语句

  ⑤回到②继续

* 示例代码：

```java
public class WhileDemo {
    public static void main(String[] args) {
        //需求：在控制台输出5次"HelloWorld"
		//for循环实现
		for(int i=1; i<=5; i++) {
			System.out.println("HelloWorld");
		}
		System.out.println("--------");
		//while循环实现
		int j = 1;
		while(j<=5) {
			System.out.println("HelloWorld");
			j++;
		}
    }
}
```

**5.6.2 while循环练习-珠穆朗玛峰（应用）**

* 需求：世界最高山峰是珠穆朗玛峰(8844.43米=8844430毫米)，假如我有一张足够大的纸，它的厚度是0.1毫米。请问，我折叠多少次，可以折成珠穆朗玛峰的高度?
* 示例代码：

```java
public class WhileTest {
    public static void main(String[] args) {
		//定义一个计数器，初始值为0
		int count = 0;
		//定义纸张厚度
		double paper = 0.1;
		//定义珠穆朗玛峰的高度
		int zf = 8844430;
		//因为要反复折叠，所以要使用循环，但是不知道折叠多少次，这种情况下更适合使用while循环
		//折叠的过程中当纸张厚度大于珠峰就停止了，因此继续执行的要求是纸张厚度小于珠峰高度
		while(paper <= zf) {
			//循环的执行过程中每次纸张折叠，纸张的厚度要加倍
			paper *= 2;
			//在循环中执行累加，对应折叠了多少次
			count++;
		}
		//打印计数器的值
		System.out.println("需要折叠：" + count + "次");
    }
}
```

**5.7 循环细节**

**5.7.1 do...while循环结构（掌握）**

* 完整格式：

  ```java
  初始化语句;
  do {
  	循环体语句;
  	条件控制语句;
  }while(条件判断语句);
  ```

* 执行流程：

  ① 执行初始化语句

  ② 执行循环体语句

  ③ 执行条件控制语句

  ④ 执行条件判断语句，看其结果是true还是false

  如果是false，循环结束

  如果是true，继续执行

  ⑤ 回到②继续

* 示例代码：

```java
public class DoWhileDemo {
    public static void main(String[] args) {
        //需求：在控制台输出5次"HelloWorld"
		//for循环实现
		for(int i=1; i<=5; i++) {
			System.out.println("HelloWorld");
		}
		System.out.println("--------");
		//do...while循环实现
		int j = 1;
		do {
			System.out.println("HelloWorld");
			j++;
		}while(j<=5);
    }
}
```

**5.7.2 三种循环的区别（理解）**

* 三种循环的区别
  * for循环和while循环先判断条件是否成立，然后决定是否执行循环体（先判断后执行）
  * do...while循环先执行一次循环体，然后判断条件是否成立，是否继续执行循环体（先执行后判断）
* for循环和while的区别
  * 条件控制语句所控制的自增变量，因为归属for循环的语法结构中，在for循环结束后，就不能再次被访问到了
  * 条件控制语句所控制的自增变量，对于while循环来说不归属其语法结构中，在while循环结束后，该变量还可以继续使用
* 死循环（无限循环）的三种格式
  1. for(;;){}
  2. while(true){}
  3. do {} while(true);

**5.7.3 跳转控制语句（掌握）**

* 跳转控制语句（break）
  * 跳出循环，结束循环
* 跳转控制语句（continue）
  * 跳过本次循环，继续下次循环
* 注意： continue只能在循环中进行使用！

**5.7.4 循环嵌套（理解）**

* 循环嵌套概述：在循环中，继续定义循环

* 示例代码：

  ```java
  	public static void main(String[] args) {
          //外循环控制小时的范围，内循环控制分钟的范围
          for (int hour = 0; hour < 24; hour++) {
              for (int minute = 0; minute < 60; minute++) {
                  System.out.println(hour + "时" + minute + "分");
              }
              System.out.println("--------");
          }
      }
  ```

* 理解：

  * 请反复理解这句话（整个内循环，就是外循环的一个循环体，内部循环体没有执行完毕，外循环是不会继续向下执行的）

* 结论：

  * 外循环执行一次，内循环执行一圈

## 6 Random

**6.1 Random产生随机数（掌握）**

* 概述：

  * Random类似Scanner，也是Java提供好的API，内部提供了产生随机数的功能
    * API后续课程详细讲解，现在可以简单理解为Java已经写好的代码

* 使用步骤：

  1. 导入包

     import java.util.Random;

  2. 创建对象

     Random r = new Random();

  3. 产生随机数

     int num = r.nextInt(10);

     解释： 10代表的是一个范围，如果括号写10，产生的随机数就是0-9，括号写20，参数的随机数则是0-19

* 示例代码：

```java
import java.util.Random;
public class RandomDemo {
	public static void main(String[] args) {
		//创建对象
		Random r = new Random();
		//用循环获取10个随机数
		for(int i=0; i<10; i++) {
			//获取随机数
			int number = r.nextInt(10);
			System.out.println("number:" + number);
		}
		//需求：获取一个1-100之间的随机数
		int x = r.nextInt(100) + 1;
		System.out.println(x);
	}
}
```

**6.2 Random练习-猜数字（应用）**

* 需求：

  程序自动生成一个1-100之间的数字，使用程序实现猜出这个数字是多少？

  当猜错的时候根据不同情况给出相应的提示

  A. 如果猜的数字比真实数字大，提示你猜的数据大了

  B. 如果猜的数字比真实数字小，提示你猜的数据小了

  C. 如果猜的数字与真实数字相等，提示恭喜你猜中了

* 示例代码：

```java
import java.util.Random;
import java.util.Scanner;

public class RandomTest {
	public static void main(String[] args) {
		//要完成猜数字的游戏，首先需要有一个要猜的数字，使用随机数生成该数字，范围1到100
		Random r = new Random();
		int number = r.nextInt(100) + 1;
		
		while(true) {
			//使用程序实现猜数字，每次均要输入猜测的数字值，需要使用键盘录入实现
			Scanner sc = new Scanner(System.in);
			
			System.out.println("请输入你要猜的数字：");
			int guessNumber = sc.nextInt();
			
			//比较输入的数字和系统产生的数据，需要使用分支语句。
             //这里使用if..else..if..格式，根据不同情况进行猜测结果显示
			if(guessNumber > number) {
				System.out.println("你猜的数字" + guessNumber + "大了");
			} else if(guessNumber < number) {
				System.out.println("你猜的数字" + guessNumber + "小了");
			} else {
				System.out.println("恭喜你猜中了");
				break;
			}
		}
		
	}
}
```

## 7 数组

**7.1什么是数组【理解】**

​	数组就是存储数据长度固定的容器，存储多个数据的数据类型要一致。 

**7.2数组定义格式【记忆】**

**7.2.1第一种**

​	数据类型[] 数组名

​	示例：

```java
int[] arr;        
double[] arr;      
char[] arr;
```

**7.2.2第二种**

​	数据类型 数组名[]

​	示例：

```java
int arr[];
double arr[];
char arr[];
```

**7.3数组动态初始化【应用】**

**7.3.1什么是动态初始化**

​	数组动态初始化就是只给定数组的长度，由系统给出默认初始化值

**7.3.2动态初始化格式**

```java
数据类型[] 数组名 = new 数据类型[数组长度];
```

```java
int[] arr = new int[3];
```

**7.3.3动态初始化格式详解**

- 等号左边：

  -  int:数组的数据类型

  -  []:代表这是一个数组

  -  arr:代表数组的名称

- 等号右边：

  -   new:为数组开辟内存空间

  -   int:数组的数据类型

  -   []:代表这是一个数组

  -   5:代表数组的长度

**7.4数组元素访问【应用】**

**7.4.1什么是索引**

​	每一个存储到数组的元素，都会自动的拥有一个编号，从0开始。

​	这个自动编号称为数组索引(index)，可以通过数组的索引访问到数组中的元素。 	

**7.4.2访问数组元素格式**

```java
数组名[索引];
```

**7.4.3示例代码**

```java
public class ArrayDemo {
    public static void main(String[] args) {
        int[] arr = new int[3];

        //输出数组名
        System.out.println(arr); //[I@880ec60

        //输出数组中的元素
        System.out.println(arr[0]);
        System.out.println(arr[1]);
        System.out.println(arr[2]);
    }
}
```

**7.5内存分配【理解】**

**7.5.1内存概述**

​	内存是计算机中的重要原件，临时存储区域，作用是运行程序。

​	我们编写的程序是存放在硬盘中的，在硬盘中的程序是不会运行的。

​	必须放进内存中才能运行，运行完毕后会清空内存。 

​	Java虚拟机要运行程序，必须要对内存进行空间的分配和管理。 

**7.5.2java中的内存分配**

- 目前我们只需要记住两个内存，分别是：栈内存和堆内存

| 区域名称   | 作用                                                       |
| ---------- | ---------------------------------------------------------- |
| 寄存器     | 给CPU使用，和我们开发无关。                                |
| 本地方法栈 | JVM在使用操作系统功能的时候使用，和我们开发无关。          |
| 方法区     | 存储可以运行的class文件。                                  |
| 堆内存     | 存储对象或者数组，new来创建的，都存储在堆内存。            |
| 方法栈     | 方法运行时使用的内存，比如main方法运行，进入方法栈中执行。 |

**7.5.3什么是静态初始化**

​	在创建数组时，直接将元素确定	

**7.5.4静态初始化格式**

- 完整版格式

  ```java
  数据类型[] 数组名 = new 数据类型[]{元素1,元素2,...};
  ```

- 简化版格式

  ```java
  数据类型[] 数组名 = {元素1,元素2,...};
  ```

**7.5.5示例代码**

```java
public class ArrayDemo {
    public static void main(String[] args) {
        //定义数组
        int[] arr = {1, 2, 3};

        //输出数组名
        System.out.println(arr);

        //输出数组中的元素
        System.out.println(arr[0]);
        System.out.println(arr[1]);
        System.out.println(arr[2]);
    }
}
```

**7.6数组操作的两个常见小问题【应用】**

**7.6.1索引越界异常**

- 出现原因

  ```java
  public class ArrayDemo {
      public static void main(String[] args) {
          int[] arr = new int[3];
          System.out.println(arr[3]);
      }
  }
  ```

  数组长度为3，索引范围是0~2，但是我们却访问了一个3的索引。

  程序运行后，将会抛出ArrayIndexOutOfBoundsException 数组越界异常。在开发中，数组的越界异常是不能出现的，一旦出现了，就必须要修改我们编写的代码。 

- 解决方案

  将错误的索引修改为正确的索引范围即可！

**7.6.2空指针异常**

- 出现原因

  ```java
  public class ArrayDemo {
      public static void main(String[] args) {
          int[] arr = new int[3];
  
          //把null赋值给数组
          arr = null;
          System.out.println(arr[0]);
      }
  }
  ```

  arr = null 这行代码，意味着变量arr将不会在保存数组的内存地址，也就不允许再操作数组了，因此运行的时候会抛出 NullPointerException 空指针异常。在开发中，数组的越界异常是不能出现的，一旦出现了，就必须要修改我们编写的代码。

- 解决方案

  给数组一个真正的堆内存空间引用即可！

**7.7数组遍历【应用】**

- 数组遍历：就是将数组中的每个元素分别获取出来，就是遍历。遍历也是数组操作中的基石。

  ```java
  public class ArrayTest01 {
  	public static void main(String[] args) {
  		int[] arr = { 1, 2, 3, 4, 5 };
  		System.out.println(arr[0]);
  		System.out.println(arr[1]);
  		System.out.println(arr[2]);
  		System.out.println(arr[3]);
  		System.out.println(arr[4]);
  	}
  }
  ```

   以上代码是可以将数组中每个元素全部遍历出来，但是如果数组元素非常多，这种写法肯定不行，因此我们需要改造成循环的写法。数组的索引是 0 到 lenght-1 ，可以作为循环的条件出现。 

  ```java
  public class ArrayTest01 {
      public static void main(String[] args) {
          //定义数组
          int[] arr = {11, 22, 33, 44, 55};
  
          //使用通用的遍历格式
          for(int x=0; x<arr.length; x++) {
              System.out.println(arr[x]);
          }
      }
  }
  ```

**7.8数组最值【应用】**

- 最大值获取：从数组的所有元素中找出最大值。

- 实现思路：

  - 定义变量，保存数组0索引上的元素
  - 遍历数组，获取出数组中的每个元素
  - 将遍历到的元素和保存数组0索引上值的变量进行比较
  - 如果数组元素的值大于了变量的值，变量记录住新的值
  - 数组循环遍历结束，变量保存的就是数组中的最大值 

- 代码实现：

  ```java
  public class ArrayTest02 {
      public static void main(String[] args) {
          //定义数组
          int[] arr = {12, 45, 98, 73, 60};
  
          //定义一个变量，用于保存最大值
          //取数组中第一个数据作为变量的初始值
          int max = arr[0];
  
          //与数组中剩余的数据逐个比对，每次比对将最大值保存到变量中
          for(int x=1; x<arr.length; x++) {
              if(arr[x] > max) {
                  max = arr[x];
              }
          }
  
          //循环结束后打印变量的值
          System.out.println("max:" + max);
  
      }
  }
  ```

## 8 方法概述

**8.1 方法的概念（理解）**

​	方法（method）是将具有独立功能的代码块组织成为一个整体，使其具有特殊功能的代码集

* 注意：
  * 方法必须先创建才可以使用，该过程成为方法定义
  * 方法创建后并不是直接可以运行的，需要手动使用后，才执行，该过程成为方法调用

**8.2 方法的定义和调用**

**8.2.1 无参数方法定义和调用（掌握）**

* 定义格式：

  ```java
  public static void 方法名 (   ) {
  	// 方法体;
  }
  ```

* 范例：

  ```java
  public static void method (    ) {
  	// 方法体;
  }
  ```

* 调用格式：

  ```java
  方法名();
  ```

* 范例：

  ```java
  method();
  ```

* 注意：

  ​	方法必须先定义，后调用，否则程序将报错

**8.2.2 方法调用过程图解（理解）**

![无参数方法调用图解](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E6%97%A0%E5%8F%82%E6%95%B0%E6%96%B9%E6%B3%95%E8%B0%83%E7%94%A8%E5%9B%BE%E8%A7%A3.png)

* 总结：每个方法在被调用执行的时候，都会进入栈内存，并且拥有自己独立的内存空间，方法内部代码调用完毕之后，会从栈内存中弹栈消失。

**8.2.3 无参数方法的练习（应用）**

* 需求：设计一个方法用于打印两个数中的较大数 
* 思路：
  * ①定义一个方法，用于打印两个数字中的较大数，例如getMax() 
  * ②方法中定义两个变量，用于保存两个数字 
  * ③使用分支语句分两种情况对两个数字的大小关系进行处理 
  * ④在main()方法中调用定义好的方法 
* 代码：

```java
public class MethodTest {
    public static void main(String[] args) {
        //在main()方法中调用定义好的方法
        getMax();
    }

    //定义一个方法，用于打印两个数字中的较大数，例如getMax()
    public static void getMax() {
        //方法中定义两个变量，用于保存两个数字
        int a = 10;
        int b = 20;

        //使用分支语句分两种情况对两个数字的大小关系进行处理
        if(a > b) {
            System.out.println(a);
        } else {
            System.out.println(b);
        }
    }
}
```

**8.3 带参数方法定义和调用**

**8.3.1 带参数方法定义和调用（掌握）**

* 定义格式：

  参数：由数据类型和变量名组成 -  数据类型 变量名

  参数范例：int a

  ```java
  public static void 方法名 (参数1) {
  	方法体;
  }
  
  public static void 方法名 (参数1, 参数2, 参数3...) {
  	方法体;
  }
  ```

* 范例：

  ```java
  public static void isEvenNumber(int number){
      ...
  }
  public static void getMax(int num1, int num2){
      ...
  }
  ```

  * 注意：

    方法定义时，参数中的数据类型与变量名都不能缺少，缺少任意一个程序将报错

    	方法定义时，多个参数之间使用逗号( ，)分隔

* 调用格式：

  ```java
  方法名(参数)；
  
  方法名(参数1,参数2);
  ```

* 范例：

  ```java
  isEvenNumber(10);
  
  getMax(10,20);
  ```

  * 方法调用时，参数的数量与类型必须与方法定义中的设置相匹配，否则程序将报错 

**8.3.2 形参和实参（理解）**

1. 形参：方法定义中的参数

​          等同于变量定义格式，例如：int number

2. 实参：方法调用中的参数

​          等同于使用变量或常量，例如： 10  number

**8.3.3 带参数方法练习（应用）**

* 需求：设计一个方法用于打印两个数中的较大数，数据来自于方法参数 }
* 思路：
  * ①定义一个方法，用于打印两个数字中的较大数，例如getMax() 
  * ②为方法定义两个参数，用于接收两个数字 
  * ③使用分支语句分两种情况对两个数字的大小关系进行处理 
  * ④在main()方法中调用定义好的方法（使用常量）
  * ⑤在main()方法中调用定义好的方法（使用变量） 
* 代码：

```java
public class MethodTest {
    public static void main(String[] args) {
        //在main()方法中调用定义好的方法（使用常量）
        getMax(10,20);
        //调用方法的时候，人家要几个，你就给几个，人家要什么类型的，你就给什么类型的
        //getMax(30);
        //getMax(10.0,20.0);

        //在main()方法中调用定义好的方法（使用变量）
        int a = 10;
        int b = 20;
        getMax(a, b);
    }

    //定义一个方法，用于打印两个数字中的较大数，例如getMax()
    //为方法定义两个参数，用于接收两个数字
    public static void getMax(int a, int b) {
        //使用分支语句分两种情况对两个数字的大小关系进行处理
        if(a > b) {
            System.out.println(a);
        } else {
            System.out.println(b);
        }
    }
}
```

**8.4 带返回值方法的定义和调用**

**8.4.1 带返回值方法定义和调用（掌握）**

* 定义格式

  ```java
  public static 数据类型 方法名 ( 参数 ) { 
  	return 数据 ;
  }
  ```

* 范例

  ```java
  public static boolean isEvenNumber( int number ) {           
  	return true ;
  }
  public static int getMax( int a, int b ) {
  	return  100 ;
  }
  ```

  * 注意：
    * 方法定义时return后面的返回值与方法定义上的数据类型要匹配，否则程序将报错

* 调用格式

  ```java
  方法名 ( 参数 ) ;
  数据类型 变量名 = 方法名 ( 参数 ) ;
  ```

* 范例

  ```java
  isEvenNumber ( 5 ) ;
  boolean  flag =  isEvenNumber ( 5 ); 
  ```

  * 注意：
    * 方法的返回值通常会使用变量接收，否则该返回值将无意义

**8.4.2 带返回值方法练习（应用）**

* 需求：设计一个方法可以获取两个数的较大值，数据来自于参数

* 思路：

  * ①定义一个方法，用于获取两个数字中的较大数 
  * ②使用分支语句分两种情况对两个数字的大小关系进行处理 
  * ③根据题设分别设置两种情况下对应的返回结果 
  * ④在main()方法中调用定义好的方法并使用变量保存 
  * ⑤在main()方法中调用定义好的方法并直接打印结果 

* 代码：

  ```java
  public class MethodTest {
      public static void main(String[] args) {
          //在main()方法中调用定义好的方法并使用变量保存
          int result = getMax(10,20);
          System.out.println(result);
  
          //在main()方法中调用定义好的方法并直接打印结果
          System.out.println(getMax(10,20));
      }
  
      //定义一个方法，用于获取两个数字中的较大数
      public static int getMax(int a, int b) {
          //使用分支语句分两种情况对两个数字的大小关系进行处理
          //根据题设分别设置两种情况下对应的返回结果
          if(a > b) {
              return a;
          } else {
              return b;
          }
      }
  }
  ```

**8.5 方法的注意事项**

**8.5.1 方法的注意事项（掌握）**

* 方法不能嵌套定义

  * 示例代码：

    ```java
    public class MethodDemo {
        public static void main(String[] args) {
    
        }
    
        public static void methodOne() {
    		public static void methodTwo() {
           		// 这里会引发编译错误!!!
        	}
        }
    }
    ```

* void表示无返回值，可以省略return，也可以单独的书写return，后面不加数据

  * 示例代码：

    ```java
    public class MethodDemo {
        public static void main(String[] args) {
    
        }
        public static void methodTwo() {
            //return 100; 编译错误，因为没有具体返回值类型
            return;	
            //System.out.println(100); return语句后面不能跟数据或代码
        }
    }
    ```

**8.5.2 方法的通用格式（掌握）**

* 格式：

  ```java
  public static 返回值类型 方法名(参数) {
     方法体; 
     return 数据 ;
  }
  ```

* 解释：

  * public static 	修饰符，目前先记住这个格式

    返回值类型	方法操作完毕之后返回的数据的数据类型

    ​			如果方法操作完毕，没有数据返回，这里写void，而且方法体中一般不写return

     方法名		调用方法时候使用的标识

     参数		由数据类型和变量名组成，多个参数之间用逗号隔开

     方法体		完成功能的代码块

     return		如果方法操作完毕，有数据返回，用于把数据返回给调用者

* 定义方法时，要做到两个明确

  * 明确返回值类型：主要是明确方法操作完毕之后是否有数据返回，如果没有，写void；如果有，写对应的数据类型
  * 明确参数：主要是明确参数的类型和数量

* 调用方法时的注意：

  * void类型的方法，直接调用即可
  * 非void类型的方法，推荐用变量接收调用

**8.6 方法重载**

**8.6.1 方法重载（理解）**

* 方法重载概念

  方法重载指同一个类中定义的多个方法之间的关系，满足下列条件的多个方法相互构成重载

  * 多个方法在同一个类中
  * 多个方法具有相同的方法名
  * 多个方法的参数不相同，类型不同或者数量不同

* 注意：

  * 重载仅对应方法的定义，与方法的调用无关，调用方式参照标准格式
  * 重载仅针对同一个类中方法的名称与参数进行识别，与返回值无关，换句话说不能通过返回值来判定两个方法是否相互构成重载

* 正确范例：

  ```java
  public class MethodDemo {
  	public static void fn(int a) {
      	//方法体
      }
      public static int fn(double a) {
      	//方法体
      }
  }
  
  public class MethodDemo {
  	public static float fn(int a) {
      	//方法体
      }
      public static int fn(int a , int b) {
      	//方法体
      }
  }
  ```

* 错误范例：

  ```java
  public class MethodDemo {
  	public static void fn(int a) {
      	//方法体
      }
      public static int fn(int a) { 	/*错误原因：重载与返回值无关*/
      	//方法体
      }
  }
  
  public class MethodDemo01 {
      public static void fn(int a) {
          //方法体
      }
  } 
  public class MethodDemo02 {
      public static int fn(double a) { /*错误原因：这是两个类的两个fn方法*/
          //方法体
      }
  }
  ```

**8.6.2 方法重载练习（掌握）**

* 需求：使用方法重载的思想，设计比较两个整数是否相同的方法，兼容全整数类型（byte,short,int,long） 

* 思路：

  * ①定义比较两个数字的是否相同的方法compare()方法，参数选择两个int型参数
  * ②定义对应的重载方法，变更对应的参数类型，参数变更为两个long型参数
  * ③定义所有的重载方法，两个byte类型与两个short类型参数 
  * ④完成方法的调用，测试运行结果 

* 代码：

  ```java
  public class MethodTest {
      public static void main(String[] args) {
          //调用方法
          System.out.println(compare(10, 20));
          System.out.println(compare((byte) 10, (byte) 20));
          System.out.println(compare((short) 10, (short) 20));
          System.out.println(compare(10L, 20L));
      }
  
      //int
      public static boolean compare(int a, int b) {
          System.out.println("int");
          return a == b;
      }
  
      //byte
      public static boolean compare(byte a, byte b) {
          System.out.println("byte");
          return a == b;
      }
  
      //short
      public static boolean compare(short a, short b) {
          System.out.println("short");
          return a == b;
      }
  
      //long
      public static boolean compare(long a, long b) {
          System.out.println("long");
          return a == b;
      }
  
  }
  ```

**8.7 方法的参数传递**

**8.7.1 方法参数传递基本类型（理解）**

* 测试代码：

  ```java
  public class ArgsDemo01 {
      public static void main(String[] args) {
          int number = 100;
          System.out.println("调用change方法前：" + number);
          change(number);
          System.out.println("调用change方法后：" + number);
      }
  
      public static void change(int number) {
          number = 200;
      }
  }
  
  ```

* 结论：

  * 基本数据类型的参数，形式参数的改变，不影响实际参数 

* 结论依据：

  * 每个方法在栈内存中，都会有独立的栈空间，方法运行结束后就会弹栈消失

    ![方法传参-基本数据类型](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E6%96%B9%E6%B3%95%E4%BC%A0%E5%8F%82-%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.png)

**8.7.2 方法参数传递引用类型（理解）**

* 测试代码：

  ```java
  public class ArgsDemo02 {
      public static void main(String[] args) {
          int[] arr = {10, 20, 30};
          System.out.println("调用change方法前：" + arr[1]);
          change(arr);
          System.out.println("调用change方法后：" + arr[1]);
      }
  
      public static void change(int[] arr) {
          arr[1] = 200;
      }
  }
  
  ```

* 结论：

  * 对于引用类型的参数，形式参数的改变，影响实际参数的值 

* 结论依据：

  * 引用数据类型的传参，传入的是地址值，内存中会造成两个引用指向同一个内存的效果，所以即使方法弹栈，堆内存中的数据也已经是改变后的结果 

    ![方法传参-引用数据类型](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E6%96%B9%E6%B3%95%E4%BC%A0%E5%8F%82-%E5%BC%95%E7%94%A8%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B-1677397104781.png)

**8.7.3 数组遍历（应用）**

* 需求：设计一个方法用于数组遍历，要求遍历的结果是在一行上的。例如：[11, 22, 33, 44, 55] 

* 思路：

  * ①因为要求结果在一行上输出，所以这里需要在学习一个新的输出语句System.out.print(“内容”);

    System.out.println(“内容”); 输出内容并换行

    System.out.print(“内容”); 输出内容不换行

    System.out.println(); 起到换行的作用

  * ②定义一个数组，用静态初始化完成数组元素初始化

  * ③定义一个方法，用数组遍历通用格式对数组进行遍历

  * ④用新的输出语句修改遍历操作

  * ⑤调用遍历方法

* 代码：

  ```java
  public class MethodTest01 {
      public static void main(String[] args) {
          //定义一个数组，用静态初始化完成数组元素初始化
          int[] arr = {11, 22, 33, 44, 55};
  
          //调用方法
          printArray(arr);
      }
  
      //定义一个方法，用数组遍历通用格式对数组进行遍历
      /*
          两个明确：
              返回值类型：void
              参数：int[] arr
       */
      public static void printArray(int[] arr) {
          System.out.print("[");
          for(int x=0; x<arr.length; x++) {
              if(x == arr.length-1) {
                  System.out.print(arr[x]);
              } else {
                  System.out.print(arr[x]+", ");
              }
          }
          System.out.println("]");
      }
  }
  ```

**8.7.4 数组最大值（应用）**

* 需求：设计一个方法用于获取数组中元素的最大值 

* 思路：

  * ①定义一个数组，用静态初始化完成数组元素初始化
  * ②定义一个方法，用来获取数组中的最大值，最值的认知和讲解我们在数组中已经讲解过了
  * ③调用获取最大值方法，用变量接收返回结果
  * ④把结果输出在控制台

* 代码：

  ```java
  public class MethodTest02 {
      public static void main(String[] args) {
          //定义一个数组，用静态初始化完成数组元素初始化
          int[] arr = {12, 45, 98, 73, 60};
  
          //调用获取最大值方法，用变量接收返回结果
          int number = getMax(arr);
  
          //把结果输出在控制台
          System.out.println("number:" + number);
      }
  
      //定义一个方法，用来获取数组中的最大值
      /*
          两个明确：
              返回值类型：int
              参数：int[] arr
       */
      public static int getMax(int[] arr) {
          int max = arr[0];
  
          for(int x=1; x<arr.length; x++) {
              if(arr[x] > max) {
                  max = arr[x];
              }
          }
          return max;
      }
  }
  ```

## 9 类和对象

**9.1 类和对象的理解【理解】**

客观存在的事物皆为对象 ，所以我们也常常说万物皆对象。

* 类
  * 类的理解
    * 类是对现实生活中一类具有共同属性和行为的事物的抽象
    * 类是对象的数据类型，类是具有相同属性和行为的一组对象的集合
    * 简单理解：类就是对现实事物的一种描述
  * 类的组成
    * 属性：指事物的特征，例如：手机事物（品牌，价格，尺寸）
    * 行为：指事物能执行的操作，例如：手机事物（打电话，发短信）
* 类和对象的关系
  * 类：类是对现实生活中一类具有共同属性和行为的事物的抽象
  * 对象：是能够看得到摸的着的真实存在的实体
  * 简单理解：**类是对事物的一种描述，对象则为具体存在的事物**

**9.2 类的定义【应用】**

类的组成是由属性和行为两部分组成

* 属性：在类中通过成员变量来体现（类中方法外的变量）
* 行为：在类中通过成员方法来体现（和前面的方法相比去掉static关键字即可）

类的定义步骤：

①定义类

②编写类的成员变量

③编写类的成员方法

```java
public class 类名 {
	// 成员变量
	变量1的数据类型 变量1；
	变量2的数据类型 变量2;
	…
	// 成员方法
	方法1;
	方法2;	
}
```

示例代码：

```java
/*
    手机类：
        类名：
        手机(Phone)

        成员变量：
        品牌(brand)
        价格(price)

        成员方法：
        打电话(call)
        发短信(sendMessage)
 */
public class Phone {
    //成员变量
    String brand;
    int price;

    //成员方法
    public void call() {
        System.out.println("打电话");
    }

    public void sendMessage() {
        System.out.println("发短信");
    }
}

```

**9.3 对象的使用【应用】**

* 创建对象的格式：
  * 类名 对象名 = new 类名();
* 调用成员的格式：
  * 对象名.成员变量
  * 对象名.成员方法();
* 示例代码

```java
/*
    创建对象
        格式：类名 对象名 = new 类名();
        范例：Phone p = new Phone();

    使用对象
        1：使用成员变量
            格式：对象名.变量名
            范例：p.brand
        2：使用成员方法
            格式：对象名.方法名()
            范例：p.call()
 */
public class PhoneDemo {
    public static void main(String[] args) {
        //创建对象
        Phone p = new Phone();

        //使用成员变量
        System.out.println(p.brand);
        System.out.println(p.price);

        p.brand = "小米";
        p.price = 2999;

        System.out.println(p.brand);
        System.out.println(p.price);

        //使用成员方法
        p.call();
        p.sendMessage();
    }
}
```

**9.5 对象内存图**

**9.5.1 单个对象内存图【理解】**

* 成员变量使用过程

![1](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/1.png)

* 成员方法调用过程

![2](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/2.png)

**9.5.2 多个对象内存图【理解】**

* 成员变量使用过程

![3](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/3.png)

* 成员方法调用过程

![4](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/4.png)

* 总结：

  多个对象在堆内存中，都有不同的内存划分，成员变量存储在各自的内存区域中，成员方法多个对象共用的一份

**9.5.3 多个对象指向相同内存图【理解】**

![4](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/4.png)

* 总结

  当多个对象的引用指向同一个内存空间（变量所记录的地址值是一样的）

  只要有任何一个对象修改了内存中的数据，随后，无论使用哪一个对象进行数据获取，都是修改后的数据。

**9.6 成员变量和局部变量**

**9.6.1 成员变量和局部变量的区别【理解】**

* 类中位置不同：成员变量（类中方法外）局部变量（方法内部或方法声明上）
* 内存中位置不同：成员变量（堆内存）局部变量（栈内存）
* 生命周期不同：成员变量（随着对象的存在而存在，随着对象的消失而消失）局部变量（随着方法的调用而存在，醉着方法的调用完毕而消失）
* 初始化值不同：成员变量（有默认初始化值）局部变量（没有默认初始化值，必须先定义，赋值才能使用）

## 10 封装

**10.1 private关键字【理解】**

private是一个修饰符，可以用来修饰成员（成员变量，成员方法）

* 被private修饰的成员，只能在本类进行访问，针对private修饰的成员变量，如果需要被其他类使用，提供相应的操作

  * 提供“get变量名()”方法，用于获取成员变量的值，方法用public修饰
  * 提供“set变量名(参数)”方法，用于设置成员变量的值，方法用public修饰

* 示例代码：

  ```java
  /*
      学生类
   */
  class Student {
      //成员变量
      String name;
      private int age;
  
      //提供get/set方法
      public void setAge(int a) {
          if(a<0 || a>120) {
              System.out.println("你给的年龄有误");
          } else {
              age = a;
          }
      }
  
      public int getAge() {
          return age;
      }
  
      //成员方法
      public void show() {
          System.out.println(name + "," + age);
      }
  }
  /*
      学生测试类
   */
  public class StudentDemo {
      public static void main(String[] args) {
          //创建对象
          Student s = new Student();
          //给成员变量赋值
          s.name = "林青霞";
          s.setAge(30);
          //调用show方法
          s.show();
      }
  }
  ```

**10.2 private的使用【应用】**

* 需求：定义标准的学生类，要求name和age使用private修饰，并提供set和get方法以及便于显示数据的show方法，测试类中创建对象并使用，最终控制台输出  林青霞，30 

* 示例代码：

  ```java
  /*
      学生类
   */
  class Student {
      //成员变量
      private String name;
      private int age;
  
      //get/set方法
      public void setName(String n) {
          name = n;
      }
  
      public String getName() {
          return name;
      }
  
      public void setAge(int a) {
          age = a;
      }
  
      public int getAge() {
          return age;
      }
  
      public void show() {
          System.out.println(name + "," + age);
      }
  }
  /*
      学生测试类
   */
  public class StudentDemo {
      public static void main(String[] args) {
          //创建对象
          Student s = new Student();
  
          //使用set方法给成员变量赋值
          s.setName("林青霞");
          s.setAge(30);
  
          s.show();
  
          //使用get方法获取成员变量的值
          System.out.println(s.getName() + "---" + s.getAge());
          System.out.println(s.getName() + "," + s.getAge());
  
      }
  }
  ```

**10.3 this关键字【应用】**

* this修饰的变量用于指代成员变量，其主要作用是（区分局部变量和成员变量的重名问题）
  * 方法的形参如果与成员变量同名，不带this修饰的变量指的是形参，而不是成员变量
  * 方法的形参没有与成员变量同名，不带this修饰的变量指的是成员变量

```java
public class Student {
    private String name;
    private int age;

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void show() {
        System.out.println(name + "," + age);
    }
}
```

**10.4 this内存原理【理解】**

* this代表当前调用方法的引用，哪个对象调用的方法，this就代表哪一个对象

* 示例代码：

  ```java
  public class StudentDemo {
      public static void main(String[] args) {
          Student s1 = new Student();
          s1.setName("林青霞");
          Student s2 = new Student();
          s2.setName("张曼玉");
      }
  }
  ```

* 图解：

  ![5](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/5.png)

  ![6](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/6.png)

**10.5 封装思想【理解】**

1. 封装概述
   是面向对象三大特征之一（封装，继承，多态）
   是面向对象编程语言对客观世界的模拟，客观世界里成员变量都是隐藏在对象内部的，外界是无法直接操作的
2. 封装原则
   将类的某些信息隐藏在类内部，不允许外部程序直接访问，而是通过该类提供的方法来实现对隐藏信息的操作和访问
   成员变量private，提供对应的getXxx()/setXxx()方法
3. 封装好处
   通过方法来控制成员变量的操作，提高了代码的安全性
   把代码用方法进行封装，提高了代码的复用性

## 11 构造方法

**11.1 构造方法概述【理解】**

构造方法是一种特殊的方法

* 作用：创建对象   Student stu = **new Student();**

* 格式：

  public class 类名{

  ​        修饰符 类名( 参数 ) {

  ​        }

  }

* 功能：主要是完成对象数据的初始化

* 示例代码：

```java
class Student {
    private String name;
    private int age;

    //构造方法
    public Student() {
        System.out.println("无参构造方法");
    }

    public void show() {
        System.out.println(name + "," + age);
    }
}
/*
    测试类
 */
public class StudentDemo {
    public static void main(String[] args) {
        //创建对象
        Student s = new Student();
        s.show();
    }
}
```

**11.2 构造方法的注意事项【理解】**

* 构造方法的创建

如果没有定义构造方法，系统将给出一个默认的无参数构造方法
如果定义了构造方法，系统将不再提供默认的构造方法

* 构造方法的重载

如果自定义了带参构造方法，还要使用无参数构造方法，就必须再写一个无参数构造方法

* 推荐的使用方式

无论是否使用，都手工书写无参数构造方法

* 重要功能！

可以使用带参构造，为成员变量进行初始化

* 示例代码

```java
/*
    学生类
 */
class Student {
    private String name;
    private int age;

    public Student() {}

    public Student(String name) {
        this.name = name;
    }

    public Student(int age) {
        this.age = age;
    }

    public Student(String name,int age) {
        this.name = name;
        this.age = age;
    }

    public void show() {
        System.out.println(name + "," + age);
    }
}
/*
    测试类
 */
public class StudentDemo {
    public static void main(String[] args) {
        //创建对象
        Student s1 = new Student();
        s1.show();

        //public Student(String name)
        Student s2 = new Student("林青霞");
        s2.show();

        //public Student(int age)
        Student s3 = new Student(30);
        s3.show();

        //public Student(String name,int age)
        Student s4 = new Student("林青霞",30);
        s4.show();
    }
}
```

**11.3 标准类制作【应用】**

* 需求：定义标准学生类，要求分别使用空参和有参构造方法创建对象，空参创建的对象通过setXxx赋值，有参创建的对象直接赋值，并通过show方法展示数据。 
* 示例代码：

```java
class Student {
    //成员变量
    private String name;
    private int age;

    //构造方法
    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    //成员方法
    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void show() {
        System.out.println(name + "," + age);
    }
}
/*
    创建对象并为其成员变量赋值的两种方式
        1:无参构造方法创建对象后使用setXxx()赋值
        2:使用带参构造方法直接创建带有属性值的对象
*/
public class StudentDemo {
    public static void main(String[] args) {
        //无参构造方法创建对象后使用setXxx()赋值
        Student s1 = new Student();
        s1.setName("林青霞");
        s1.setAge(30);
        s1.show();

        //使用带参构造方法直接创建带有属性值的对象
        Student s2 = new Student("林青霞",30);
        s2.show();
    }
}
```

## 12 API

**12.1API概述【理解】**

- 什么是API

  ​	API (Application Programming Interface) ：应用程序编程接口

- java中的API

  ​	指的就是 JDK 中提供的各种功能的 Java类，这些类将底层的实现封装了起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用即可，我们可以通过帮助文档来学习这些API如何使用。

**12.2 常用API**

**12.2.1 Math（应用）**

* 1、Math类概述

  * Math 包含执行基本数字运算的方法

* 2、Math中方法的调用方式

  * Math类中无构造方法，但内部的方法都是静态的，则可以通过   **类名.进行调用**

* 3、Math类的常用方法

  | 方法名    方法名                               | 说明                                           |
  | ---------------------------------------------- | ---------------------------------------------- |
  | public static int   abs(int a)                 | 返回参数的绝对值                               |
  | public static double ceil(double a)            | 返回大于或等于参数的最小double值，等于一个整数 |
  | public static double floor(double a)           | 返回小于或等于参数的最大double值，等于一个整数 |
  | public   static int round(float a)             | 按照四舍五入返回最接近参数的int                |
  | public static int   max(int a,int b)           | 返回两个int值中的较大值                        |
  | public   static int min(int a,int b)           | 返回两个int值中的较小值                        |
  | public   static double pow (double a,double b) | 返回a的b次幂的值                               |
  | public   static double random()                | 返回值为double的正值，[0.0,1.0)                |

**12.2.2 System（应用）**

* System类的常用方法 

| 方法名                                   | 说明                                             |
| ---------------------------------------- | ------------------------------------------------ |
| public   static void exit(int status)    | 终止当前运行的   Java   虚拟机，非零表示异常终止 |
| public   static long currentTimeMillis() | 返回当前时间(以毫秒为单位)                       |

* 示例代码

  * 需求：在控制台输出1-10000，计算这段代码执行了多少毫秒 

  ```java
  public class SystemDemo {
      public static void main(String[] args) {
          // 获取开始的时间节点
          long start = System.currentTimeMillis();
          for (int i = 1; i <= 10000; i++) {
              System.out.println(i);
          }
          // 获取代码运行结束后的时间节点
          long end = System.currentTimeMillis();
          System.out.println("共耗时：" + (end - start) + "毫秒");
      }
  }
  ```

**12.2.3 Object类的toString方法（应用）**

* Object类概述

  * Object 是类层次结构的根，每个类都可以将 Object 作为超类。所有类都直接或者间接的继承自该类，换句话说，该类所具备的方法，所有类都会有一份

* 查看方法源码的方式

  * 选中方法，按下Ctrl + B

* 重写toString方法的方式

  * 1. Alt + Insert 选择toString
  * 2. 在类的空白区域，右键 -> Generate -> 选择toString

* toString方法的作用：

  * 以良好的格式，更方便的展示对象中的属性值

* 示例代码：

  ```java
  class Student extends Object {
      private String name;
      private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      @Override
      public String toString() {
          return "Student{" +
                  "name='" + name + '\'' +
                  ", age=" + age +
                  '}';
      }
  }
  public class ObjectDemo {
      public static void main(String[] args) {
          Student s = new Student();
          s.setName("林青霞");
          s.setAge(30);
          System.out.println(s); 
          System.out.println(s.toString()); 
      }
  }
  ```

* 运行结果：

  ```java
  Student{name='林青霞', age=30}
  Student{name='林青霞', age=30}
  ```

**12.2.4 Object类的equals方法（应用）**

* equals方法的作用

  * 用于对象之间的比较，返回true和false的结果
  * 举例：s1.equals(s2);    s1和s2是两个对象

* 重写equals方法的场景

  * 不希望比较对象的地址值，想要结合对象属性进行比较的时候。

* 重写equals方法的方式

  * 1. alt + insert  选择equals() and hashCode()，IntelliJ Default，一路next，finish即可
  * 2. 在类的空白区域，右键 -> Generate -> 选择equals() and hashCode()，后面的同上。

* 示例代码：

  ```java
  class Student {
      private String name;
      private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      @Override
      public boolean equals(Object o) {
          //this -- s1
          //o -- s2
          if (this == o) return true;
          if (o == null || getClass() != o.getClass()) return false;
  
          Student student = (Student) o; //student -- s2
  
          if (age != student.age) return false;
          return name != null ? name.equals(student.name) : student.name == null;
      }
  }
  public class ObjectDemo {
      public static void main(String[] args) {
          Student s1 = new Student();
          s1.setName("林青霞");
          s1.setAge(30);
  
          Student s2 = new Student();
          s2.setName("林青霞");
          s2.setAge(30);
  
          //需求：比较两个对象的内容是否相同
          System.out.println(s1.equals(s2));
      }
  }
  
  ```

**12.2.5 冒泡排序原理（理解）**

* 冒泡排序概述
  * 一种排序的方式，对要进行排序的数据中相邻的数据进行两两比较，将较大的数据放在后面，依次对所有的数据进行操作，直至所有数据按要求完成排序
* 如果有n个数据进行排序，总共需要比较n-1次
* 每一次比较完毕，下一次的比较就会少一个数据参与

**12.2.6 冒泡排序代码实现（理解）**

* 代码实现

```java
/*
    冒泡排序：
        一种排序的方式，对要进行排序的数据中相邻的数据进行两两比较，将较大的数据放在后面，
        依次对所有的数据进行操作，直至所有数据按要求完成排序
 */
public class ArrayDemo {
    public static void main(String[] args) {
        //定义一个数组
        int[] arr = {24, 69, 80, 57, 13};
        System.out.println("排序前：" + arrayToString(arr));

        // 这里减1，是控制每轮比较的次数
        for (int x = 0; x < arr.length - 1; x++) {
            // -1是为了避免索引越界，-x是为了调高比较效率
            for (int i = 0; i < arr.length - 1 - x; i++) {
                if (arr[i] > arr[i + 1]) {
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                }
            }
        }
        System.out.println("排序后：" + arrayToString(arr));

    }

    //把数组中的元素按照指定的规则组成一个字符串：[元素1, 元素2, ...]
    public static String arrayToString(int[] arr) {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        for (int i = 0; i < arr.length; i++) {
            if (i == arr.length - 1) {
                sb.append(arr[i]);
            } else {
                sb.append(arr[i]).append(", ");
            }
        }
        sb.append("]");
        String s = sb.toString();
        return s;
    }
}
```

**12.2.7 Arrays（应用）**

* Arrays的常用方法

  | 方法名                                 | 说明                               |
  | -------------------------------------- | ---------------------------------- |
  | public static String toString(int[] a) | 返回指定数组的内容的字符串表示形式 |
  | public static void sort(int[] a)       | 按照数字顺序排列指定的数组         |

* 工具类设计思想

  1、构造方法用 private 修饰

  2、成员用 public static 修饰

## 13 常用类

### 13.1 String类

**13.1.1String类概述【理解】**

​	String 类代表字符串，Java 程序中的所有字符串文字（例如“abc”）都被实现为此类的实例。也就是说，Java 程序中所有的双引号字符串，都是 String 类的对象。String 类在 java.lang 包下，所以使用的时候不需要导包！

**13.1.2String类的特点【理解】**

- 字符串不可变，它们的值在创建后不能被更改
- 虽然 String 的值是不可变的，但是它们可以被共享
- 字符串效果上相当于字符数组( char[] )，但是底层原理是字节数组( byte[] )

**13.1.3String类的构造方法【记忆】**

- 常用的构造方法

  | 方法名                      | 说明                                      |
  | --------------------------- | ----------------------------------------- |
  | public   String()           | 创建一个空白字符串对象，不含有任何内容    |
  | public   String(char[] chs) | 根据字符数组的内容，来创建字符串对象      |
  | public   String(byte[] bys) | 根据字节数组的内容，来创建字符串对象      |
  | String s =   “abc”;         | 直接赋值的方式创建字符串对象，内容就是abc |

- 示例代码

  ```java
  public class StringDemo01 {
      public static void main(String[] args) {
          //public String()：创建一个空白字符串对象，不含有任何内容
          String s1 = new String();
          System.out.println("s1:" + s1);
  
          //public String(char[] chs)：根据字符数组的内容，来创建字符串对象
          char[] chs = {'a', 'b', 'c'};
          String s2 = new String(chs);
          System.out.println("s2:" + s2);
  
          //public String(byte[] bys)：根据字节数组的内容，来创建字符串对象
          byte[] bys = {97, 98, 99};
          String s3 = new String(bys);
          System.out.println("s3:" + s3);
  
          //String s = “abc”;	直接赋值的方式创建字符串对象，内容就是abc
          String s4 = "abc";
          System.out.println("s4:" + s4);
      }
  }
  ```

**13.1.4创建字符串对象两种方式的区别【理解】**

- 通过构造方法创建

  ​	通过 new 创建的字符串对象，每一次 new 都会申请一个内存空间，虽然内容相同，但是地址值不同

- 直接赋值方式创建

  ​	以“”方式给出的字符串，只要字符序列相同(顺序和大小写)，无论在程序代码中出现几次，JVM 都只会建立一个 String 对象，并在字符串池中维护

**13.1.5 字符串的比较【理解】**

**13.1.5.1==号的作用**

- 比较基本数据类型：比较的是具体的值
- 比较引用数据类型：比较的是对象地址值

**13.1.5.2equals方法的作用**

- 方法介绍

  ```java
  public boolean equals(String s)     比较两个字符串内容是否相同、区分大小写
  ```

- 示例代码

  ```java
  public class StringDemo02 {
      public static void main(String[] args) {
          //构造方法的方式得到对象
          char[] chs = {'a', 'b', 'c'};
          String s1 = new String(chs);
          String s2 = new String(chs);
  
          //直接赋值的方式得到对象
          String s3 = "abc";
          String s4 = "abc";
  
          //比较字符串对象地址是否相同
          System.out.println(s1 == s2);
          System.out.println(s1 == s3);
          System.out.println(s3 == s4);
          System.out.println("--------");
  
          //比较字符串内容是否相同
          System.out.println(s1.equals(s2));
          System.out.println(s1.equals(s3));
          System.out.println(s3.equals(s4));
      }
  }
  ```

**13.1.5.3 帮助文档查看String常用方法【记忆】**

| 方法名                                   | 说明                                           |
| ---------------------------------------- | ---------------------------------------------- |
| public boolean   equals(Object anObject) | 比较字符串的内容，严格区分大小写(用户名和密码) |
| public char charAt(int   index)          | 返回指定索引处的 char 值                       |
| public int   length()                    | 返回此字符串的长度                             |

### **13.2 StringBuilder类**

**13.2.1StringBuilder类概述【理解】**

​	StringBuilder 是一个可变的字符串类，我们可以把它看成是一个容器，这里的可变指的是 StringBuilder 对象中的内容是可变的

**13.2.2StringBuilder类和String类的区别【理解】**

- String类：内容是不可变的
- StringBuilder类：内容是可变的

**13.2.3StringBuilder类的构造方法【记忆】**

- 常用的构造方法

  | 方法名                             | 说明                                       |
  | ---------------------------------- | ------------------------------------------ |
  | public StringBuilder()             | 创建一个空白可变字符串对象，不含有任何内容 |
  | public StringBuilder(String   str) | 根据字符串的内容，来创建可变字符串对象     |

- 示例代码

```java
public class StringBuilderDemo01 {
    public static void main(String[] args) {
        //public StringBuilder()：创建一个空白可变字符串对象，不含有任何内容
        StringBuilder sb = new StringBuilder();
        System.out.println("sb:" + sb);
        System.out.println("sb.length():" + sb.length());

        //public StringBuilder(String str)：根据字符串的内容，来创建可变字符串对象
        StringBuilder sb2 = new StringBuilder("hello");
        System.out.println("sb2:" + sb2);
        System.out.println("sb2.length():" + sb2.length());
    }
}
```

**13.2.4StringBuilder类添加和反转方法【记忆】**

- 添加和反转方法

  | 方法名                                  | 说明                     |
  | --------------------------------------- | ------------------------ |
  | public StringBuilder   append(任意类型) | 添加数据，并返回对象本身 |
  | public StringBuilder   reverse()        | 返回相反的字符序列       |

- 示例代码

```java
public class StringBuilderDemo01 {
    public static void main(String[] args) {
        //创建对象
        StringBuilder sb = new StringBuilder();

        //public StringBuilder append(任意类型)：添加数据，并返回对象本身
//        StringBuilder sb2 = sb.append("hello");
//
//        System.out.println("sb:" + sb);
//        System.out.println("sb2:" + sb2);
//        System.out.println(sb == sb2);

//        sb.append("hello");
//        sb.append("world");
//        sb.append("java");
//        sb.append(100);

        //链式编程
        sb.append("hello").append("world").append("java").append(100);

        System.out.println("sb:" + sb);

        //public StringBuilder reverse()：返回相反的字符序列
        sb.reverse();
        System.out.println("sb:" + sb);
    }
}
```

**13.2.5StringBuilder和String相互转换【应用】**

- StringBuilder转换为String

  ​        public String toString()：通过 toString() 就可以实现把 StringBuilder 转换为 String

- String转换为StringBuilder

  ​        public StringBuilder(String s)：通过构造方法就可以实现把 String 转换为 StringBuilder

- 示例代码

```java
public class StringBuilderDemo02 {
    public static void main(String[] args) {
        /*
        //StringBuilder 转换为 String
        StringBuilder sb = new StringBuilder();
        sb.append("hello");

        //String s = sb; //这个是错误的做法

        //public String toString()：通过 toString() 就可以实现把 StringBuilder 转换为 String
        String s = sb.toString();
        System.out.println(s);
        */

        //String 转换为 StringBuilder
        String s = "hello";

        //StringBuilder sb = s; //这个是错误的做法

        //public StringBuilder(String s)：通过构造方法就可以实现把 String 转换为 StringBuilder
        StringBuilder sb = new StringBuilder(s);

        System.out.println(sb);
    }
}
```

**13.2.6 帮助文档查看StringBuilder常用方法【记忆】**

| 方法名                                   | 说明                                                |
| ---------------------------------------- | --------------------------------------------------- |
| public   StringBuilder append (任意类型) | 添加数据，并返回对象本身                            |
| public   StringBuilder reverse()         | 返回相反的字符序列                                  |
| public   int   length()                  | 返回长度，实际存储值                                |
| public   String toString()               | 通过toString()就可以实现把StringBuilder转换为String |

## 14 继承

**14.1 继承的实现（掌握）**

* 继承的概念

  * 继承是面向对象三大特征之一，可以使得子类具有父类的属性和方法，还可以在子类中重新定义，以及追加属性和方法

* 实现继承的格式

  * 继承通过extends实现
  * 格式：class 子类 extends 父类 { } 
    * 举例：class Dog extends Animal { }

* 继承带来的好处

  * 继承可以让类与类之间产生关系，子父类关系，产生子父类后，子类则可以使用父类中非私有的成员。

* 示例代码

  ```java
  public class Fu {
      public void show() {
          System.out.println("show方法被调用");
      }
  }
  public class Zi extends Fu {
      public void method() {
          System.out.println("method方法被调用");
      }
  }
  public class Demo {
      public static void main(String[] args) {
          //创建对象，调用方法
          Fu f = new Fu();
          f.show();
  
          Zi z = new Zi();
          z.method();
          z.show();
      }
  }
  ```

**14.2 继承的好处和弊端（理解）**

* 继承好处
  * 提高了代码的复用性(多个类相同的成员可以放到同一个类中)
  * 提高了代码的维护性(如果方法的代码需要修改，修改一处即可)
* 继承弊端
  * 继承让类与类之间产生了关系，类的耦合性增强了，当父类发生变化时子类实现也不得不跟着变化，削弱了子类的独立性
* 继承的应用场景：
  * 使用继承，需要考虑类与类之间是否存在is..a的关系，不能盲目使用继承
    *  is..a的关系：谁是谁的一种，例如：老师和学生是人的一种，那人就是父类，学生和老师就是子类

**14.3 继承中的成员访问特点**

**14.3.1 继承中变量的访问特点（掌握）**

在子类方法中访问一个变量，采用的是就近原则。

1. 子类局部范围找
2. 子类成员范围找
3. 父类成员范围找
4. 如果都没有就报错(不考虑父亲的父亲…)

* 示例代码

  ```java
  class Fu {
      int num = 10;
  }
  class Zi {
      int num = 20;
      public void show(){
          int num = 30;
          System.out.println(num);
      }
  }
  public class Demo1 {
      public static void main(String[] args) {
          Zi z = new Zi();
          z.show();	// 输出show方法中的局部变量30
      }
  }
  ```

**14.3.2 super（掌握）**

* this&super关键字：
  * this：代表本类对象的引用
  * super：代表父类存储空间的标识(可以理解为父类对象引用)
* this和super的使用分别
  * 成员变量：
    * this.成员变量    -   访问本类成员变量
    * super.成员变量 -   访问父类成员变量
  * 成员方法：
    * this.成员方法  - 访问本类成员方法
    * super.成员方法 - 访问父类成员方法
* 构造方法：
  * this(…)  -  访问本类构造方法
  * super(…)  -  访问父类构造方法

**14.3.3 继承中构造方法的访问特点（理解）**

**注意：子类中所有的构造方法默认都会访问父类中无参的构造方法**

​	子类会继承父类中的数据，可能还会使用父类的数据。所以，子类初始化之前，一定要先完成父类数据的初始化，原因在于，每一个子类构造方法的第一条语句默认都是：super()

**问题：如果父类中没有无参构造方法，只有带参构造方法，该怎么办呢？**

	1. 通过使用super关键字去显示的调用父类的带参构造方法
	2. 在父类中自己提供一个无参构造方法

**推荐方案：**

​	自己给出无参构造方法

**14.3.4 继承中成员方法的访问特点（掌握）**

通过子类对象访问一个方法

1. 子类成员范围找
2. 父类成员范围找
3. 如果都没有就报错(不考虑父亲的父亲…)

**14.3.5 super内存图（理解）**

* 对象在堆内存中，会单独存在一块super区域，用来存放父类的数据 

  ![图片1](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E5%9B%BE%E7%89%871-1677413514918.png)

**14.3.6 方法重写（掌握）**

* 1、方法重写概念
  * 子类出现了和父类中一模一样的方法声明（方法名一样，参数列表也必须一样）
* 2、方法重写的应用场景
  * 当子类需要父类的功能，而功能主体子类有自己特有内容时，可以重写父类中的方法，这样，即沿袭了父类的功能，又定义了子类特有的内容
* 3、Override注解
  * 用来检测当前的方法，是否是重写的方法，起到【校验】的作用

**14.3.7 方法重写的注意事项（掌握）**

* 方法重写的注意事项

1. 私有方法不能被重写(父类私有成员子类是不能继承的)
2. 子类方法访问权限不能更低(public > 默认 > 私有)

* 示例代码

```java
public class Fu {
    private void show() {
        System.out.println("Fu中show()方法被调用");
    }

    void method() {
        System.out.println("Fu中method()方法被调用");
    }
}

public class Zi extends Fu {

    /* 编译【出错】，子类不能重写父类私有的方法*/
    @Override
    private void show() {
        System.out.println("Zi中show()方法被调用");
    }
   
    /* 编译【出错】，子类重写父类方法的时候，访问权限需要大于等于父类 */
    @Override
    private void method() {
        System.out.println("Zi中method()方法被调用");
    }

    /* 编译【通过】，子类重写父类方法的时候，访问权限需要大于等于父类 */
    @Override
    public void method() {
        System.out.println("Zi中method()方法被调用");
    }
}
```

**14.3.8 Java中继承的注意事项（掌握）**

* Java中继承的注意事项

  1. Java中类只支持单继承，不支持多继承
     * 错误范例：class A extends B, C { }
  2. Java中类支持多层继承

* 多层继承示例代码：

  ```java
  public class Granddad {
  
      public void drink() {
          System.out.println("爷爷爱喝酒");
      }
  
  }
  
  public class Father extends Granddad {
  
      public void smoke() {
          System.out.println("爸爸爱抽烟");
      }
  
  }
  
  public class Mother {
  
      public void dance() {
          System.out.println("妈妈爱跳舞");
      }
  
  }
  public class Son extends Father {
  	// 此时，Son类中就同时拥有drink方法以及smoke方法
  }
  ```

**14.4 修饰符**

**14.4.1 package（了解）**

* 1、包的概念
  * 包就是文件夹，用来管理类文件的
* 2、包的定义格式
  * package 包名; (多级包用.分开)
  * 例如：package com.heima.demo;
* 3、带包编译&带包运行
  * 带包编译：javac –d . 类名.java
    * 例如：javac  -d  . com.heima.demo.HelloWorld.java
  * 带包运行：java 包名+类名
    * 例如：java com.heima.demo.HelloWorld

**14.4.2 import（理解）**

* 导包的意义

  使用不同包下的类时，使用的时候要写类的全路径，写起来太麻烦了

  为了简化带包的操作，Java就提供了导包的功能

* 导包的格式

  格式：import 包名;

  范例：import java.util.Scanner;

* 示例代码（没有使用导包，创建的Scanner对象）

```java
package com.heima;

public class Demo {
    public static void main(String[] args) {
        // 1. 没有导包，创建Scnaner对象
        java.util.Scanner sc = new java.util.Scanner(System.in);
    }
}
```

* 示例代码（使用导包后，创建的Scanner对象）

```java
package com.heima;

import java.util.Scanner;

public class Demo {
    public static void main(String[] args) {
        // 1. 没有导包，创建Scnaner对象
        Scanner sc = new Scanner(System.in);
    }
}
```

**14.4.3 权限修饰符（理解）**

![图片2(1)](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E5%9B%BE%E7%89%872(1).png)

**14.4.4 final（应用）**

* fianl关键字的作用
  * final代表最终的意思，可以修饰成员方法，成员变量，类
* final修饰类、方法、变量的效果  
  * fianl修饰类：该类不能被继承（不能有子类，但是可以有父类）
  * final修饰方法：该方法不能被重写
  * final修饰变量：表明该变量是一个常量，不能再次赋值

**14.4.5 final修饰局部变量（理解）**

* fianl修饰基本数据类型变量

  * final 修饰指的是基本类型的数据值不能发生改变

* final修饰引用数据类型变量  

  * final 修饰指的是引用类型的地址值不能发生改变，但是地址里面的内容是可以发生改变的

  * 举例：

    ```java
    public static void main(String[] args){
        final Student s = new Student(23);
      	s = new Student(24);  // 错误
     	s.setAge(24);  // 正确
    }
    ```

**14.4.6 static（应用）**

* static的概念
  * static关键字是静态的意思，可以修饰【成员方法】，【成员变量】
* static修饰的特点 
  1. 被类的所有对象共享，这也是我们判断是否使用静态关键字的条件
  2. 可以通过类名调用当然，也可以通过对象名调用**【推荐使用类名调用】**
* 示例代码：

```java
class Student {

    public String name; //姓名
    public int age; //年龄
    public static String university; //学校	共享数据！所以设计为静态！

    public void show() {
        System.out.println(name + "," + age + "," + university);
    }

}

public class StaticDemo {
    public static void main(String[] args) {
	    // 为对象的共享数据赋值
        Student.university = "传智大学";

        Student s1 = new Student();
        s1.name = "林青霞";
        s1.age = 30;
        s1.show();

        Student s2 = new Student();
        s2.name = "风清扬";
        s2.age = 33;
        s2.show();
    }
}
```

**14.4.7 static访问特点（掌握）**

* static的访问特点
  * 非静态的成员方法
    * 能访问静态的成员变量
    * 能访问非静态的成员变量
    * 能访问静态的成员方法
    * 能访问非静态的成员方法
  * 静态的成员方法
    * 能访问静态的成员变量
    * 能访问静态的成员方法
  * 总结成一句话就是：
    * **静态成员方法只能访问静态成员**

## 15 多态

**15.1 多态的概述（记忆）**

- 什么是多态

  ​	同一个对象，在不同时刻表现出来的不同形态

- 多态的前提

  - 要有继承或实现关系
  - 要有方法的重写
  - 要有父类引用指向子类对象

**15.2多态中的成员访问特点（记忆）**

- **成员访问特点**

  - 成员变量

    ​	编译看父类，运行看父类

  - 成员方法

    ​	编译看父类，运行看子类

- 代码演示

  - 动物类

    ```java
    public class Animal {
        public int age = 40;
    
        public void eat() {
            System.out.println("动物吃东西");
        }
    }
    ```

  - 猫类

    ```java
    public class Cat extends Animal {
        public int age = 20;
        public int weight = 10;
    
        @Override
        public void eat() {
            System.out.println("猫吃鱼");
        }
    
        public void playGame() {
            System.out.println("猫捉迷藏");
        }
    }
    ```

  - 测试类

    ```java
    public class AnimalDemo {
        public static void main(String[] args) {
            //有父类引用指向子类对象
            Animal a = new Cat();
    
            System.out.println(a.age);
    //        System.out.println(a.weight);
    
            a.eat();
    //        a.playGame();
        }
    }
    ```

**15.3多态的好处和弊端（记忆）**

- 好处

  ​	提高程序的扩展性。定义方法时候，使用父类型作为参数，在使用的时候，使用具体的子类型参与操作

- 弊端

  ​	不能使用子类的特有成员

**15.4多态中的转型（应用）**

- 向上转型

  ​	父类引用指向子类对象就是向上转型

- 向下转型

  ​	格式：子类型 对象名 = (子类型)父类引用;

- 代码演示

  - 动物类

  ```java
  public class Animal {
      public void eat() {
          System.out.println("动物吃东西");
      }
  }
  ```

  - 猫类

  ```java
  public class Cat extends Animal {
      @Override
      public void eat() {
          System.out.println("猫吃鱼");
      }
  
      public void playGame() {
          System.out.println("猫捉迷藏");
      }
  }
  ```

  - 测试类

  ```java
  public class AnimalDemo {
      public static void main(String[] args) {
          //多态
          //向上转型
          Animal a = new Cat();
          a.eat();
  //      a.playGame();
  
  
          //向下转型
          Cat c = (Cat)a;
          c.eat();
          c.playGame();
      }
  }
  ```

**15.5多态的案例（应用）**

- 案例需求

  ​	请采用多态的思想实现猫和狗的案例，并在测试类中进行测试

- 代码实现

  - 动物类

  ```java
  public class Animal {
      private String name;
      private int age;
  
      public Animal() {
      }
  
      public Animal(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public void eat() {
          System.out.println("动物吃东西");
      }
  }
  ```

  - 猫类

  ```java
  public class Cat extends Animal {
  
      public Cat() {
      }
  
      public Cat(String name, int age) {
          super(name, age);
      }
  
      @Override
      public void eat() {
          System.out.println("猫吃鱼");
      }
  }
  ```

  - 狗类

  ```java
  public class Dog extends Animal {
  
      public Dog() {
      }
  
      public Dog(String name, int age) {
          super(name, age);
      }
  
      @Override
      public void eat() {
          System.out.println("狗吃骨头");
      }
  }
  ```

  - 测试类

  ```java
  public class AnimalDemo {
      public static void main(String[] args) {
          //创建猫类对象进行测试
          Animal a = new Cat();
          a.setName("加菲");
          a.setAge(5);
          System.out.println(a.getName() + "," + a.getAge());
          a.eat();
  
          a = new Cat("加菲", 5);
          System.out.println(a.getName() + "," + a.getAge());
          a.eat();
      }
  }
  ```

## 16 抽象类

**16.1抽象类的概述（理解）**

​	当我们在做子类共性功能抽取时，有些方法在父类中并没有具体的体现，这个时候就需要抽象类了！

​	在Java中，一个没有方法体的方法应该定义为抽象方法，而类中如果有抽象方法，该类必须定义为抽象类！

**16.2抽象类的特点（记忆）**

- 抽象类和抽象方法必须使用 abstract 关键字修饰

  ```java
  //抽象类的定义
  public abstract class 类名 {}
  
  //抽象方法的定义
  public abstract void eat();
  ```

- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类

- 抽象类不能实例化

  ​	抽象类如何实例化呢？参照多态的方式，通过子类对象实例化，这叫抽象类多态

- 抽象类的子类

  ​	要么重写抽象类中的所有抽象方法

  ​	要么是抽象类

**16.3抽象类的成员特点（记忆）**

- 成员的特点

  - 成员变量
    - 既可以是变量
    - 也可以是常量
  - 构造方法
    - 空参构造
    - 有参构造
  - 成员方法
    - 抽象方法
    - 普通方法

- 代码演示

  - 动物类

  ```java
  public abstract class Animal {
  
      private int age = 20;
      private final String city = "北京";
  
      public Animal() {}
  
      public Animal(int age) {
          this.age = age;
      }
  
  
      public void show() {
          age = 40;
          System.out.println(age);
  //        city = "上海";
          System.out.println(city);
      }
  
      public abstract void eat();
  
  }
  ```

  - 猫类

  ```java
  public class Cat extends Animal {
      @Override
      public void eat() {
          System.out.println("猫吃鱼");
      }
  }
  ```

  - 测试类

  ```java
  public class AnimalDemo {
      public static void main(String[] args) {
          Animal a = new Cat();
          a.eat();
          a.show();
      }
  }
  ```

**16.4抽象类的案例（应用）**

- 案例需求

  ​	请采用抽象类的思想实现猫和狗的案例，并在测试类中进行测试

- 代码实现

  - 动物类

  ```java
  public abstract class Animal {
      private String name;
      private int age;
  
      public Animal() {
      }
  
      public Animal(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public abstract void eat();
  }
  ```

  - 猫类

  ```java
  public class Cat extends Animal {
  
      public Cat() {
      }
  
      public Cat(String name, int age) {
          super(name, age);
      }
  
      @Override
      public void eat() {
          System.out.println("猫吃鱼");
      }
  }
  ```

  - 狗类

  ```java
  public class Dog extends Animal {
  
      public Dog() {
      }
  
      public Dog(String name, int age) {
          super(name, age);
      }
  
      @Override
      public void eat() {
          System.out.println("狗吃骨头");
      }
  }
  ```

  - 测试类

  ```java
  public class AnimalDemo {
      public static void main(String[] args) {
          //创建对象，按照多态的方式
          Animal a = new Cat();
          a.setName("加菲");
          a.setAge(5);
          System.out.println(a.getName()+","+a.getAge());
          a.eat();
          System.out.println("--------");
  
          a = new Cat("加菲",5);
          System.out.println(a.getName()+","+a.getAge());
          a.eat();
      }
  }
  ```

## 17 接口

**17.1接口的概述（理解）**

​	接口就是一种公共的规范标准，只要符合规范标准，大家都可以通用。

​	Java中的接口更多的体现在对行为的抽象！

**17.2接口的特点（记忆）**

- 接口用关键字interface修饰

  ```java
  public interface 接口名 {} 
  ```

- 类实现接口用implements表示

  ```java
  public class 类名 implements 接口名 {}
  ```

- 接口不能实例化

  ​	接口如何实例化呢？参照多态的方式，通过实现类对象实例化，这叫接口多态。

  ​	多态的形式：具体类多态，抽象类多态，接口多态。 

- 接口的子类

  ​	要么重写接口中的所有抽象方法

  ​	要么子类也是抽象类

**17.3接口的成员特点（记忆）**

- 成员特点

  - 成员变量

    ​	 只能是常量
    ​	 默认修饰符：public static final

  - 构造方法

    ​	没有，因为接口主要是扩展功能的，而没有具体存在

  - 成员方法

    ​	只能是抽象方法

    ​	默认修饰符：public abstract

    ​	关于接口中的方法，JDK8和JDK9中有一些新特性，后面再讲解

- 代码演示

  - 接口

  ```java
  public interface Inter {
      public int num = 10;
      public final int num2 = 20;
  //    public static final int num3 = 30;
      int num3 = 30;
  
  //    public Inter() {}
  
  //    public void show() {}
  
      public abstract void method();
      void show();
  }
  ```

  - 实现类

  ```java
  public class InterImpl extends Object implements Inter {
      public InterImpl() {
          super();
      }
  
      @Override
      public void method() {
          System.out.println("method");
      }
  
      @Override
      public void show() {
          System.out.println("show");
      }
  }
  ```

  - 测试类

  ```java
  public class InterfaceDemo {
      public static void main(String[] args) {
          Inter i = new InterImpl();
  //        i.num = 20;
          System.out.println(i.num);
  //        i.num2 = 40;
          System.out.println(i.num2);
          System.out.println(Inter.num);
      }
  }
  ```

**17.4接口的案例（应用）**

- 案例需求

  ​	对猫和狗进行训练，他们就可以跳高了，这里加入跳高功能。

  ​	请采用抽象类和接口来实现猫狗案例，并在测试类中进行测试。

- 代码实现

  - 动物类

  ```java
  public abstract class Animal {
      private String name;
      private int age;
  
      public Animal() {
      }
  
      public Animal(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public abstract void eat();
  }
  ```

  - 跳高接口

  ```java
  public interface Jumpping {
      public abstract void jump();
  }
  ```

  - 猫类

  ```java
  public class Cat extends Animal implements Jumpping {
  
      public Cat() {
      }
  
      public Cat(String name, int age) {
          super(name, age);
      }
  
      @Override
      public void eat() {
          System.out.println("猫吃鱼");
      }
  
      @Override
      public void jump() {
          System.out.println("猫可以跳高了");
      }
  }
  ```

  - 测试类

  ```java
  public class AnimalDemo {
      public static void main(String[] args) {
          //创建对象，调用方法
          Jumpping j = new Cat();
          j.jump();
          System.out.println("--------");
  
          Animal a = new Cat();
          a.setName("加菲");
          a.setAge(5);
          System.out.println(a.getName()+","+a.getAge());
          a.eat();
  //        a.jump();
  
          a = new Cat("加菲",5);
          System.out.println(a.getName()+","+a.getAge());
          a.eat();
          System.out.println("--------");
  
          Cat c = new Cat();
          c.setName("加菲");
          c.setAge(5);
          System.out.println(c.getName()+","+c.getAge());
          c.eat();
          c.jump();
      }
  }
  ```

**17.5类和接口的关系（记忆）**

- 类与类的关系

  ​	继承关系，只能单继承，但是可以多层继承

- 类与接口的关系

  ​	实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口

- 接口与接口的关系

  ​	继承关系，可以单继承，也可以多继承

**17.6抽象类和接口的区别（记忆）**

- 成员区别

  - 抽象类

    ​	变量,常量；有构造方法；有抽象方法,也有非抽象方法

  - 接口

    ​	常量；抽象方法

- 关系区别

  - 类与类

    ​	继承，单继承

  - 类与接口

    ​	实现，可以单实现，也可以多实现

  - 接口与接口

    ​	继承，单继承，多继承

- 设计理念区别

  - 抽象类

    ​	对类抽象，包括属性、行为

  - 接口

    ​	对行为抽象，主要是行为

## 18 参数传递

**18.1 类名作为形参和返回值（应用）**

* 1、类名作为方法的形参

  方法的形参是类名，其实需要的是该类的对象

  实际传递的是该对象的【地址值】

* 2、类名作为方法的返回值

  方法的返回值是类名，其实返回的是该类的对象

  实际传递的，也是该对象的【地址值】

* 示例代码：

  ```java
  class Cat {
      public void eat() {
          System.out.println("猫吃鱼");
      }
  }
  class CatOperator {
      public void useCat(Cat c) { //Cat c = new Cat();
          c.eat();
      }
      public Cat getCat() {
          Cat c = new Cat();
          return c;
      }
  }
  public class CatDemo {
      public static void main(String[] args) {
          //创建操作类对象，并调用方法
          CatOperator co = new CatOperator();
          Cat c = new Cat();
          co.useCat(c);
  
          Cat c2 = co.getCat(); //new Cat()
          c2.eat();
      }
  }
  ```

**18.2 抽象类作为形参和返回值（理解）**

* 抽象类作为形参和返回值

  * 方法的形参是抽象类名，其实需要的是该抽象类的子类对象
  * 方法的返回值是抽象类名，其实返回的是该抽象类的子类对象

* 示例代码：

  ```java
  abstract class Animal {
      public abstract void eat();
  }
  class Cat extends Animal {
      @Override
      public void eat() {
          System.out.println("猫吃鱼");
      }
  }
  class AnimalOperator {
      public void useAnimal(Animal a) { //Animal a = new Cat();
          a.eat();
      }
      public Animal getAnimal() {
          Animal a = new Cat();
          return a;
      }
  }
  public class AnimalDemo {
      public static void main(String[] args) {
          //创建操作类对象，并调用方法
          AnimalOperator ao = new AnimalOperator();
          Animal a = new Cat();
          ao.useAnimal(a);
  
          Animal a2 = ao.getAnimal(); //new Cat()
          a2.eat();
      }
  }
  ```

**18.3 接口名作为形参和返回值（理解）**

* 接口作为形参和返回值

  * 方法的形参是接口名，其实需要的是该接口的实现类对象
  * 方法的返回值是接口名，其实返回的是该接口的实现类对象

* 示例代码：

  ```java
  interface Jumpping {
      void jump();
  }
  class JumppingOperator {
      public void useJumpping(Jumpping j) { //Jumpping j = new Cat();
          j.jump();
      }
      public Jumpping getJumpping() {
          Jumpping j = new Cat();
          return j;
      }
  }
  class Cat implements Jumpping {
      @Override
      public void jump() {
          System.out.println("猫可以跳高了");
      }
  }
  public class JumppingDemo {
      public static void main(String[] args) {
          //创建操作类对象，并调用方法
          JumppingOperator jo = new JumppingOperator();
          Jumpping j = new Cat();
          jo.useJumpping(j);
  
          Jumpping j2 = jo.getJumpping(); //new Cat()
          j2.jump();
      }
  }
  
  ```

## 19 内部类

**19.1 内部类的基本使用（理解）**

* 内部类概念

  * 在一个类中定义一个类。举例：在一个类A的内部定义一个类B，类B就被称为内部类

* 内部类定义格式

  * 格式&举例：

    ```java
    /*
    	格式：
        class 外部类名{
        	修饰符 class 内部类名{
        	
        	}
        }
    */
    
    class Outer {
        public class Inner {
            
        }
    }
    ```

* 内部类的访问特点 

  * 内部类可以直接访问外部类的成员，包括私有
  * 外部类要访问内部类的成员，必须创建对象

* 示例代码：

  ```java
  /*
      内部类访问特点：
          内部类可以直接访问外部类的成员，包括私有
          外部类要访问内部类的成员，必须创建对象
   */
  public class Outer {
      private int num = 10;
      public class Inner {
          public void show() {
              System.out.println(num);
          }
      }
      public void method() {
          Inner i = new Inner();
          i.show();
      }
  }
  ```

**19.2 成员内部类（理解）**

* 成员内部类的定义位置

  * 在类中方法，跟成员变量是一个位置

* 外界创建成员内部类格式

  * 格式：外部类名.内部类名 对象名 = 外部类对象.内部类对象;
  * 举例：Outer.Inner oi = new Outer().new Inner();

* 成员内部类的推荐使用方案

  * 将一个类，设计为内部类的目的，大多数都是不想让外界去访问，所以内部类的定义应该私有化，私有化之后，再提供一个可以让外界调用的方法，方法内部创建内部类对象并调用。

* 示例代码：

  ```java
  class Outer {
      private int num = 10;
      private class Inner {
          public void show() {
              System.out.println(num);
          }
      }
      public void method() {
          Inner i = new Inner();
          i.show();
      }
  }
  public class InnerDemo {
      public static void main(String[] args) {
  		//Outer.Inner oi = new Outer().new Inner();
  		//oi.show();
          Outer o = new Outer();
          o.method();
      }
  }
  ```

**19.3 局部内部类（理解）**

* 局部内部类定义位置

  * 局部内部类是在方法中定义的类

* 局部内部类方式方式

  * 局部内部类，外界是无法直接使用，需要在方法内部创建对象并使用
  * 该类可以直接访问外部类的成员，也可以访问方法内的局部变量

* 示例代码

  ```java
  class Outer {
      private int num = 10;
      public void method() {
          int num2 = 20;
          class Inner {
              public void show() {
                  System.out.println(num);
                  System.out.println(num2);
              }
          }
          Inner i = new Inner();
          i.show();
      }
  }
  public class OuterDemo {
      public static void main(String[] args) {
          Outer o = new Outer();
          o.method();
      }
  }
  
  ```

**19.4 匿名内部类（应用）**

* 匿名内部类的前提

  * 存在一个类或者接口，这里的类可以是具体类也可以是抽象类

* 匿名内部类的格式

  * 格式：new 类名 ( ) {  重写方法 }    new  接口名 ( ) { 重写方法 }

  * 举例： 

    ```java
    new Inter(){
        @Override
        public void method(){}
    } 
    ```

* 匿名内部类的本质

  * 本质：是一个继承了该类或者实现了该接口的子类匿名对象

* 匿名内部类的细节

  * 匿名内部类可以通过多态的形式接受

    ```java
    Inter i = new Inter(){
      @Override
        public void method(){
            
        }
    }
    ```

* 匿名内部类直接调用方法

  ```java
  interface Inter{
      void method();
  }
  
  class Test{
      public static void main(String[] args){
          new Inter(){
              @Override
              public void method(){
                  System.out.println("我是匿名内部类");
              }
          }.method();	// 直接调用方法
      }
  }
  ```

**19.5 匿名内部类在开发中的使用（应用）**

* 匿名内部类在开发中的使用

  * 当发现某个方法需要，接口或抽象类的子类对象，我们就可以传递一个匿名内部类过去，来简化传统的代码

* 示例代码：

  ```java
  interface Jumpping {
      void jump();
  }
  class Cat implements Jumpping {
      @Override
      public void jump() {
          System.out.println("猫可以跳高了");
      }
  }
  class Dog implements Jumpping {
      @Override
      public void jump() {
          System.out.println("狗可以跳高了");
      }
  }
  class JumppingOperator {
      public void method(Jumpping j) { //new Cat();   new Dog();
          j.jump();
      }
  }
  class JumppingDemo {
      public static void main(String[] args) {
          //需求：创建接口操作类的对象，调用method方法
          JumppingOperator jo = new JumppingOperator();
          Jumpping j = new Cat();
          jo.method(j);
  
          Jumpping j2 = new Dog();
          jo.method(j2);
          System.out.println("--------");
  
          // 匿名内部类的简化
          jo.method(new Jumpping() {
              @Override
              public void jump() {
                  System.out.println("猫可以跳高了");
              }
          });
  		// 匿名内部类的简化
          jo.method(new Jumpping() {
              @Override
              public void jump() {
                  System.out.println("狗可以跳高了");
              }
          });
      }
  }
  ```

## 20 泛型

**20.1泛型概述和好处【理解】**

- 泛型概述

  ​	是JDK5中引入的特性，它提供了编译时类型安全检测机制，该机制允许在编译时检测到非法的类型

  它的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？顾名思义，就是将类型由原来的具体的类型参数化，然后在使用/调用时传入具体的类型。这种参数类型可以用在类、方法和接口中，分别被称为泛型类、泛型方法、泛型接口

- 泛型定义格式

  - <类型>：指定一种类型的格式。这里的类型可以看成是形参
  - <类型1,类型2…>：指定多种类型的格式，多种类型之间用逗号隔开。这里的类型可以看成是形参
  - 将来具体调用时候给定的类型可以看成是实参，并且实参的类型只能是引用数据类型

- 泛型的好处

  - 把运行时期的问题提前到了编译期间
  - 避免了强制类型转换

**20.2泛型类【应用】**

- 定义格式

  ```java
  修饰符 class 类名<类型> {  }
  ```

- 示例代码

  - 泛型类

    ```java
    public class Generic<T> {
        private T t;
    
        public T getT() {
            return t;
        }
    
        public void setT(T t) {
            this.t = t;
        }
    }
    ```

  - 测试类

    ```java
    public class GenericDemo {
        public static void main(String[] args) {
            Generic<String> g1 = new Generic<String>();
            g1.setT("林青霞");
            System.out.println(g1.getT());
    
            Generic<Integer> g2 = new Generic<Integer>();
            g2.setT(30);
            System.out.println(g2.getT());
    
            Generic<Boolean> g3 = new Generic<Boolean>();
            g3.setT(true);
            System.out.println(g3.getT());
        }
    }
    ```

**20.3泛型方法【应用】**

- 定义格式

  ```java
  修饰符 <类型> 返回值类型 方法名(类型 变量名) {  }
  ```

- 示例代码

  - 带有泛型方法的类

    ```java
    public class Generic {
        public <T> void show(T t) {
            System.out.println(t);
        }
    }
    ```

  - 测试类

    ```java
    public class GenericDemo {
        public static void main(String[] args) {
    		Generic g = new Generic();
            g.show("林青霞");
            g.show(30);
            g.show(true);
            g.show(12.34);
        }
    }
    ```

**20.4泛型接口【应用】**

- 定义格式

  ```java
  修饰符 interface 接口名<类型> {  }
  ```

- 示例代码

  - 泛型接口

    ```java
    public interface Generic<T> {
        void show(T t);
    }
    ```

  - 泛型接口实现类

    ```java
    public class GenericImpl<T> implements Generic<T> {
        @Override
        public void show(T t) {
            System.out.println(t);
        }
    }
    ```

  - 测试类

    ```java
    public class GenericDemo {
        public static void main(String[] args) {
            Generic<String> g1 = new GenericImpl<String>();
            g1.show("林青霞");
    
            Generic<Integer> g2 = new GenericImpl<Integer>();
            g2.show(30);
        }
    }
    ```

**20.5类型通配符【应用】**

- 类型通配符的作用

  ​	为了表示各种泛型List的父类，可以使用类型通配符	

- 类型通配符的分类

  - 类型通配符：<?>
    - List<?>：表示元素类型未知的List，它的元素可以匹配任何的类型
    - 这种带通配符的List仅表示它是各种泛型List的父类，并不能把元素添加到其中
  - 类型通配符上限：<? extends 类型>
    - List<? extends Number>：它表示的类型是Number或者其子类型
  - 类型通配符下限：<? super 类型>
    - List<? super Number>：它表示的类型是Number或者其父类型

- 类型通配符的基本使用

  ```java
  public class GenericDemo {
      public static void main(String[] args) {
          //类型通配符：<?>
          List<?> list1 = new ArrayList<Object>();
          List<?> list2 = new ArrayList<Number>();
          List<?> list3 = new ArrayList<Integer>();
          System.out.println("--------");
  
          //类型通配符上限：<? extends 类型>
  //        List<? extends Number> list4 = new ArrayList<Object>();
          List<? extends Number> list5 = new ArrayList<Number>();
          List<? extends Number> list6 = new ArrayList<Integer>();
          System.out.println("--------");
  
          //类型通配符下限：<? super 类型>
          List<? super Number> list7 = new ArrayList<Object>();
          List<? super Number> list8 = new ArrayList<Number>();
  //        List<? super Number> list9 = new ArrayList<Integer>();
  
      }
  }
  ```

## 21 包装类

**21.1基本类型包装类（记忆）**

- 基本类型包装类的作用

  ​	将基本数据类型封装成对象的好处在于可以在对象中定义更多的功能方法操作该数据

  ​	常用的操作之一：用于基本数据类型与字符串之间的转换

- 基本类型对应的包装类

  | 基本数据类型 | 包装类    |
  | ------------ | --------- |
  | byte         | Byte      |
  | short        | Short     |
  | int          | Integer   |
  | long         | Long      |
  | float        | Float     |
  | double       | Double    |
  | char         | Character |
  | boolean      | Boolean   |

**21.2Integer类（应用）**

- Integer类概述

  ​	包装一个对象中的原始类型 int 的值

- Integer类构造方法

  | 方法名                                  | 说明                                     |
  | --------------------------------------- | ---------------------------------------- |
  | public Integer(int   value)             | 根据 int 值创建 Integer 对象(过时)       |
  | public Integer(String s)                | 根据 String 值创建 Integer 对象(过时)    |
  | public static Integer valueOf(int i)    | 返回表示指定的 int 值的 Integer   实例   |
  | public static Integer valueOf(String s) | 返回一个保存指定值的 Integer 对象 String |

- 示例代码

  ```java
  public class IntegerDemo {
      public static void main(String[] args) {
          //public Integer(int value)：根据 int 值创建 Integer 对象(过时)
          Integer i1 = new Integer(100);
          System.out.println(i1);
  
          //public Integer(String s)：根据 String 值创建 Integer 对象(过时)
          Integer i2 = new Integer("100");
  //        Integer i2 = new Integer("abc"); //NumberFormatException
          System.out.println(i2);
          System.out.println("--------");
  
          //public static Integer valueOf(int i)：返回表示指定的 int 值的 Integer 实例
          Integer i3 = Integer.valueOf(100);
          System.out.println(i3);
  
          //public static Integer valueOf(String s)：返回一个保存指定值的Integer对象 String
          Integer i4 = Integer.valueOf("100");
          System.out.println(i4);
      }
  }
  ```

**21.3 int和String类型的相互转换（记忆）**

- int转换为String

  - 转换方式

    - 方式一：直接在数字后加一个空字符串
    - 方式二：通过String类静态方法valueOf()

  - 示例代码

    ```java
    public class IntegerDemo {
        public static void main(String[] args) {
            //int --- String
            int number = 100;
            //方式1
            String s1 = number + "";
            System.out.println(s1);
            //方式2
            //public static String valueOf(int i)
            String s2 = String.valueOf(number);
            System.out.println(s2);
            System.out.println("--------");
        }
    }
    ```

- String转换为int

  - 转换方式

    - 方式一：先将字符串数字转成Integer，再调用valueOf()方法
    - 方式二：通过Integer静态方法parseInt()进行转换

  - 示例代码

    ```java
    public class IntegerDemo {
        public static void main(String[] args) {
            //String --- int
            String s = "100";
            //方式1：String --- Integer --- int
            Integer i = Integer.valueOf(s);
            //public int intValue()
            int x = i.intValue();
            System.out.println(x);
            //方式2
            //public static int parseInt(String s)
            int y = Integer.parseInt(s);
            System.out.println(y);
        }
    }
    ```

**21.4字符串数据排序案例（应用）**

- 案例需求

  ​	有一个字符串：“91 27 46 38 50”，请写程序实现最终输出结果是：“27 38 46 50 91”

- 代码实现

  ```java
  public class IntegerTest {
      public static void main(String[] args) {
          //定义一个字符串
          String s = "91 27 46 38 50";
  
          //把字符串中的数字数据存储到一个int类型的数组中
          String[] strArray = s.split(" ");
  //        for(int i=0; i<strArray.length; i++) {
  //            System.out.println(strArray[i]);
  //        }
  
          //定义一个int数组，把 String[] 数组中的每一个元素存储到 int 数组中
          int[] arr = new int[strArray.length];
          for(int i=0; i<arr.length; i++) {
              arr[i] = Integer.parseInt(strArray[i]);
          }
  
          //对 int 数组进行排序
          Arrays.sort(arr);
  
          //把排序后的int数组中的元素进行拼接得到一个字符串，这里拼接采用StringBuilder来实现
          StringBuilder sb = new StringBuilder();
          for(int i=0; i<arr.length; i++) {
              if(i == arr.length - 1) {
                  sb.append(arr[i]);
              } else {
                  sb.append(arr[i]).append(" ");
              }
          }
          String result = sb.toString();
  
          //输出结果
          System.out.println(result);
      }
  }
  ```

**21.5自动拆箱和自动装箱（理解）**

- 自动装箱

  ​	把基本数据类型转换为对应的包装类类型

- 自动拆箱

  ​	把包装类类型转换为对应的基本数据类型

- 示例代码

  ```java
  Integer i = 100;  // 自动装箱
  i += 200;         // i = i + 200;  i + 200 自动拆箱；i = i + 200; 是自动装箱
  ```

**21.6 时间日期类**

**21.6.1Date类（应用）**

- Date类概述

  ​	Date 代表了一个特定的时间，精确到毫秒

- Date类构造方法

  | 方法名                 | 说明                                                         |
  | ---------------------- | ------------------------------------------------------------ |
  | public Date()          | 分配一个 Date对象，并初始化，以便它代表它被分配的时间，精确到毫秒 |
  | public Date(long date) | 分配一个 Date对象，并将其初始化为表示从标准基准时间起指定的毫秒数 |

- 示例代码

  ```java
  public class DateDemo01 {
      public static void main(String[] args) {
          //public Date()：分配一个 Date对象，并初始化，以便它代表它被分配的时间，精确到毫秒
          Date d1 = new Date();
          System.out.println(d1);
  
          //public Date(long date)：分配一个 Date对象，并将其初始化为表示从标准基准时间起指定的毫秒数
          long date = 1000*60*60;
          Date d2 = new Date(date);
          System.out.println(d2);
      }
  }
  ```

**21.6.2Date类常用方法（应用）**

- 常用方法

  | 方法名                         | 说明                                                  |
  | ------------------------------ | ----------------------------------------------------- |
  | public long getTime()          | 获取的是日期对象从1970年1月1日 00:00:00到现在的毫秒值 |
  | public void setTime(long time) | 设置时间，给的是毫秒值                                |

- 示例代码

  ```java
  public class DateDemo02 {
      public static void main(String[] args) {
          //创建日期对象
          Date d = new Date();
  
          //public long getTime():获取的是日期对象从1970年1月1日 00:00:00到现在的毫秒值
  //        System.out.println(d.getTime());
  //        System.out.println(d.getTime() * 1.0 / 1000 / 60 / 60 / 24 / 365 + "年");
  
          //public void setTime(long time):设置时间，给的是毫秒值
  //        long time = 1000*60*60;
          long time = System.currentTimeMillis();
          d.setTime(time);
  
          System.out.println(d);
      }
  }
  ```

**21.6.3SimpleDateFormat类（应用）**

- SimpleDateFormat类概述

  ​	SimpleDateFormat是一个具体的类，用于以区域设置敏感的方式格式化和解析日期。

  ​	我们重点学习日期格式化和解析

- SimpleDateFormat类构造方法

  | 方法名                                  | 说明                                                   |
  | --------------------------------------- | ------------------------------------------------------ |
  | public   SimpleDateFormat()             | 构造一个SimpleDateFormat，使用默认模式和日期格式       |
  | public SimpleDateFormat(String pattern) | 构造一个SimpleDateFormat使用给定的模式和默认的日期格式 |

- SimpleDateFormat类的常用方法

  - 格式化(从Date到String)
    - public final String format(Date date)：将日期格式化成日期/时间字符串
  - 解析(从String到Date)
    - public Date parse(String source)：从给定字符串的开始解析文本以生成日期

- 示例代码

  ```java
  public class SimpleDateFormatDemo {
      public static void main(String[] args) throws ParseException {
          //格式化：从 Date 到 String
          Date d = new Date();
  //        SimpleDateFormat sdf = new SimpleDateFormat();
          SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
          String s = sdf.format(d);
          System.out.println(s);
          System.out.println("--------");
  
          //从 String 到 Date
          String ss = "2048-08-09 11:11:11";
          //ParseException
          SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
          Date dd = sdf2.parse(ss);
          System.out.println(dd);
      }
  }
  ```

**21.6.4 Calendar类（应用）**

- Calendar类概述

  ​	Calendar 为特定瞬间与一组日历字段之间的转换提供了一些方法，并为操作日历字段提供了一些方法

  ​	Calendar 提供了一个类方法 getInstance 用于获取这种类型的一般有用的对象。

  ​	该方法返回一个Calendar 对象。

  ​	其日历字段已使用当前日期和时间初始化：Calendar rightNow = Calendar.getInstance();

- Calendar类常用方法

  | 方法名                                             | 说明                                                   |
  | -------------------------------------------------- | ------------------------------------------------------ |
  | public int   get(int field)                        | 返回给定日历字段的值                                   |
  | public abstract void add(int   field, int amount)  | 根据日历的规则，将指定的时间量添加或减去给定的日历字段 |
  | public final void set(int year,int month,int date) | 设置当前日历的年月日                                   |

- 示例代码

  ```java
  public class CalendarDemo {
      public static void main(String[] args) {
          //获取日历类对象
          Calendar c = Calendar.getInstance();
  
          //public int get(int field):返回给定日历字段的值
          int year = c.get(Calendar.YEAR);
          int month = c.get(Calendar.MONTH) + 1;
          int date = c.get(Calendar.DATE);
          System.out.println(year + "年" + month + "月" + date + "日");
  
          //public abstract void add(int field, int amount):根据日历的规则，将指定的时间量添加或减去给定的日历字段
          //需求1:3年前的今天
  //        c.add(Calendar.YEAR,-3);
  //        year = c.get(Calendar.YEAR);
  //        month = c.get(Calendar.MONTH) + 1;
  //        date = c.get(Calendar.DATE);
  //        System.out.println(year + "年" + month + "月" + date + "日");
  
          //需求2:10年后的10天前
  //        c.add(Calendar.YEAR,10);
  //        c.add(Calendar.DATE,-10);
  //        year = c.get(Calendar.YEAR);
  //        month = c.get(Calendar.MONTH) + 1;
  //        date = c.get(Calendar.DATE);
  //        System.out.println(year + "年" + month + "月" + date + "日");
  
          //public final void set(int year,int month,int date):设置当前日历的年月日
          c.set(2050,10,10);
          year = c.get(Calendar.YEAR);
          month = c.get(Calendar.MONTH) + 1;
          date = c.get(Calendar.DATE);
          System.out.println(year + "年" + month + "月" + date + "日");
  
      }
  }
  ```

## 22 异常

**22.1异常（记忆）**

- 异常的概述

  ​	异常就是程序出现了不正常的情况

- 异常的体系结构

  ​	![异常的体系结构](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E5%BC%82%E5%B8%B8%E7%9A%84%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84.png)

**22.2JVM默认处理异常的方式（理解）**

- 如果程序出现了问题，我们没有做任何处理，最终JVM 会做默认的处理，处理方式有如下两个步骤：

- 把异常的名称，错误原因及异常出现的位置等信息输出在了控制台
- 程序停止执行

**22.3try-catch方式处理异常（应用）**

- 定义格式

  ```java
  try {
  	可能出现异常的代码;
  } catch(异常类名 变量名) {
  	异常的处理代码;
  }
  ```

- 执行流程

  - 程序从 try 里面的代码开始执行
  - 出现异常，就会跳转到对应的 catch 里面去执行
  - 执行完毕之后，程序还可以继续往下执行

- 示例代码

  ```java
  public class ExceptionDemo01 {
      public static void main(String[] args) {
          System.out.println("开始");
          method();
          System.out.println("结束");
      }
  
      public static void method() {
          try {
              int[] arr = {1, 2, 3};
              System.out.println(arr[3]);
              System.out.println("这里能够访问到吗");
          } catch (ArrayIndexOutOfBoundsException e) {
  //            System.out.println("你访问的数组索引不存在，请回去修改为正确的索引");
              e.printStackTrace();
          }
      }
  }
  ```

**22.4Throwable成员方法（应用）**

- 常用方法

  | 方法名                        | 说明                              |
  | ----------------------------- | --------------------------------- |
  | public String getMessage()    | 返回此 throwable 的详细消息字符串 |
  | public String toString()      | 返回此可抛出的简短描述            |
  | public void printStackTrace() | 把异常的错误信息输出在控制台      |

- 示例代码

  ```java
  public class ExceptionDemo02 {
      public static void main(String[] args) {
          System.out.println("开始");
          method();
          System.out.println("结束");
      }
  
      public static void method() {
          try {
              int[] arr = {1, 2, 3};
              System.out.println(arr[3]); //new ArrayIndexOutOfBoundsException();
              System.out.println("这里能够访问到吗");
          } catch (ArrayIndexOutOfBoundsException e) { //new ArrayIndexOutOfBoundsException();
  //            e.printStackTrace();
  
              //public String getMessage():返回此 throwable 的详细消息字符串
  //            System.out.println(e.getMessage());
              //Index 3 out of bounds for length 3
  
              //public String toString():返回此可抛出的简短描述
  //            System.out.println(e.toString());
              //java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
  
              //public void printStackTrace():把异常的错误信息输出在控制台
              e.printStackTrace();
  //            java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
  //            at com.itheima_02.ExceptionDemo02.method(ExceptionDemo02.java:18)
  //            at com.itheima_02.ExceptionDemo02.main(ExceptionDemo02.java:11)
  
          }
      }
  }
  ```

**22.5编译时异常和运行时异常的区别（记忆）**

- 编译时异常
  - 都是Exception类及其子类
  - 必须显示处理，否则程序就会发生错误，无法通过编译

- 运行时异常
  - 都是RuntimeException类及其子类
  - 无需显示处理，也可以和编译时异常一样处理

**22.6throws方式处理异常（应用）**

- 定义格式

  ```java
  public void 方法() throws 异常类名 {
      
  }
  ```

- 示例代码

  ```java
  public class ExceptionDemo {
      public static void main(String[] args) {
          System.out.println("开始");
  //        method();
          try {
              method2();
          }catch (ParseException e) {
              e.printStackTrace();
          }
          System.out.println("结束");
      }
  
      //编译时异常
      public static void method2() throws ParseException {
          String s = "2048-08-09";
          SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
          Date d = sdf.parse(s);
          System.out.println(d);
      }
  
      //运行时异常
      public static void method() throws ArrayIndexOutOfBoundsException {
          int[] arr = {1, 2, 3};
          System.out.println(arr[3]);
      }
  }
  ```

- 注意事项

  - 这个throws格式是跟在方法的括号后面的
  - 编译时异常必须要进行处理，两种处理方案：try...catch …或者 throws，如果采用 throws 这种方案，将来谁调用谁处理
  - 运行时异常可以不处理，出现问题后，需要我们回来修改代码

**22.7throws和throw的区别（记忆）**

![throws和throw的区别](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/throws%E5%92%8Cthrow%E7%9A%84%E5%8C%BA%E5%88%AB.png)

**22.8自定义异常（应用）**

- 自定义异常类

  ```java
  public class ScoreException extends Exception {
  
      public ScoreException() {}
  
      public ScoreException(String message) {
          super(message);
      }
  
  }
  ```

- 老师类

  ```java
  public class Teacher {
      public void checkScore(int score) throws ScoreException {
          if(score<0 || score>100) {
  //            throw new ScoreException();
              throw new ScoreException("你给的分数有误，分数应该在0-100之间");
          } else {
              System.out.println("成绩正常");
          }
      }
  }
  ```

- 测试类

  ```java
  public class Demo {
      public static void main(String[] args) {
          Scanner sc = new Scanner(System.in);
          System.out.println("请输入分数：");
  
          int score = sc.nextInt();
  
          Teacher t = new Teacher();
          try {
              t.checkScore(score);
          } catch (ScoreException e) {
              e.printStackTrace();
          }
      }
  }
  ```

## 23 集合

### 23.1 Collection集合

**23.1.1集合体系结构【记忆】**

- 集合类的特点

  ​	提供一种存储空间可变的存储模型，存储的数据容量可以随时发生改变

- 集合类的体系图

  ![集合类的体系图](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E9%9B%86%E5%90%88%E7%B1%BB%E7%9A%84%E4%BD%93%E7%B3%BB%E5%9B%BE-1677490032079.png)

**23.1.2Collection集合概述和基本使用【应用】**

- Collection集合概述

  - 是单例集合的顶层接口，它表示一组对象，这些对象也称为Collection的元素

  - JDK 不提供此接口的任何直接实现，它提供更具体的子接口（如Set和List）实现

- Collection集合基本使用

  ```java
  public class CollectionDemo01 {
      public static void main(String[] args) {
          //创建Collection集合的对象
          Collection<String> c = new ArrayList<String>();
  
          //添加元素：boolean add(E e)
          c.add("hello");
          c.add("world");
          c.add("java");
  
          //输出集合对象
          System.out.println(c);
      }
  }
  ```

**23.1.3Collection集合的常用方法【应用】**

| 方法名                     | 说明                               |
| -------------------------- | ---------------------------------- |
| boolean add(E e)           | 添加元素                           |
| boolean remove(Object o)   | 从集合中移除指定的元素             |
| void   clear()             | 清空集合中的元素                   |
| boolean contains(Object o) | 判断集合中是否存在指定的元素       |
| boolean isEmpty()          | 判断集合是否为空                   |
| int   size()               | 集合的长度，也就是集合中元素的个数 |

**23.1.4Collection集合的遍历【应用】**

- 迭代器的介绍
  - 迭代器，集合的专用遍历方式
  - Iterator<E> iterator()：返回此集合中元素的迭代器，通过集合的iterator()方法得到
  - 迭代器是通过集合的iterator()方法得到的，所以我们说它是依赖于集合而存在的
- Collection集合的遍历

```java
public class IteratorDemo {
    public static void main(String[] args) {
        //创建集合对象
        Collection<String> c = new ArrayList<>();

        //添加元素
        c.add("hello");
        c.add("world");
        c.add("java");
        c.add("javaee");

        //Iterator<E> iterator()：返回此集合中元素的迭代器，通过集合的iterator()方法得到
        Iterator<String> it = c.iterator();

        //用while循环改进元素的判断和获取
        while (it.hasNext()) {
            String s = it.next();
            System.out.println(s);
        }
    }
}
```

**23.1.5集合使用步骤图解【理解】**

- 使用步骤

![集合使用步骤](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E9%9B%86%E5%90%88%E4%BD%BF%E7%94%A8%E6%AD%A5%E9%AA%A4.png)

**23.1.6集合的案例-Collection集合存储学生对象并遍历【应用】**

- 案例需求

  ​	创建一个存储学生对象的集合，存储3个学生对象，使用程序实现在控制台遍历该集合

- 代码实现

  - 学生类

  ```java
  public class Student {
      private String name;
      private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  }
  ```

  - 测试类

  ```java
  public class CollectionDemo {
      public static void main(String[] args) {
          //创建Collection集合对象
          Collection<Student> c = new ArrayList<Student>();
  
          //创建学生对象
          Student s1 = new Student("林青霞", 30);
          Student s2 = new Student("张曼玉", 35);
          Student s3 = new Student("王祖贤", 33);
  
          //把学生添加到集合
          c.add(s1);
          c.add(s2);
          c.add(s3);
  
          //遍历集合(迭代器方式)
          Iterator<Student> it = c.iterator();
          while (it.hasNext()) {
              Student s = it.next();
              System.out.println(s.getName() + "," + s.getAge());
          }
      }
  }
  ```

### 23.2 List集合

**23.2.1List集合概述和特点【记忆】**

- List集合概述
  - 有序集合(也称为序列)，用户可以精确控制列表中每个元素的插入位置。用户可以通过整数索引访问元素，并搜索列表中的元素
  - 与Set集合不同，列表通常允许重复的元素
- List集合特点
  - 有索引
  - 可以存储重复元素
  - 元素存取有序

**23.2.2List集合的特有方法【应用】**

| 方法名                          | 描述                                   |
| ------------------------------- | -------------------------------------- |
| void add(int index,E   element) | 在此集合中的指定位置插入指定的元素     |
| E remove(int   index)           | 删除指定索引处的元素，返回被删除的元素 |
| E set(int index,E   element)    | 修改指定索引处的元素，返回被修改的元素 |
| E get(int   index)              | 返回指定索引处的元素                   |

**23.2.3集合的案例-List集合存储学生对象并遍历【应用】**

- 案例需求

  ​	创建一个存储学生对象的集合，存储3个学生对象，使用程序实现在控制台遍历该集合

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    ```

  - 测试类

    ```java
    public class ListDemo {
        public static void main(String[] args) {
            //创建List集合对象
            List<Student> list = new ArrayList<Student>();
    
            //创建学生对象
            Student s1 = new Student("林青霞", 30);
            Student s2 = new Student("张曼玉", 35);
            Student s3 = new Student("王祖贤", 33);
    
            //把学生添加到集合
            list.add(s1);
            list.add(s2);
            list.add(s3);
    
            //迭代器方式
            Iterator<Student> it = list.iterator();
            while (it.hasNext()) {
                Student s = it.next();
                System.out.println(s.getName() + "," + s.getAge());
            }
            
            System.out.println("--------");
    
            //for循环方式
            for(int i=0; i<list.size(); i++) {
                Student s = list.get(i);
                System.out.println(s.getName() + "," + s.getAge());
            }
    
        }
    }
    ```

**23.2.4并发修改异常【应用】**

- 出现的原因

  ​	迭代器遍历的过程中，通过集合对象修改了集合中的元素，造成了迭代器获取元素中判断预期修改值和实际修改值不一致，则会出现：ConcurrentModificationException

- 解决的方案

  ​	用for循环遍历，然后用集合对象做对应的操作即可

- 示例代码

  ```java
  public class ListDemo {
      public static void main(String[] args) {
          //创建集合对象
          List<String> list = new ArrayList<String>();
  
          //添加元素
          list.add("hello");
          list.add("world");
          list.add("java");
  
          //遍历集合，得到每一个元素，看有没有"world"这个元素，如果有，我就添加一个"javaee"元素，请写代码实现
  //        Iterator<String> it = list.iterator();
  //        while (it.hasNext()) {
  //            String s = it.next();
  //            if(s.equals("world")) {
  //                list.add("javaee");
  //            }
  //        }
  
          for(int i=0; i<list.size(); i++) {
              String s = list.get(i);
              if(s.equals("world")) {
                  list.add("javaee");
              }
          }
  
          //输出集合对象
          System.out.println(list);
      }
  }
  ```

**23.2.5列表迭代器【应用】**

- ListIterator介绍

  - 通过List集合的listIterator()方法得到，所以说它是List集合特有的迭代器
  - 用于允许程序员沿任一方向遍历的列表迭代器，在迭代期间修改列表，并获取列表中迭代器的当前位置

- 示例代码

  ```java
  public class ListIteratorDemo {
      public static void main(String[] args) {
          //创建集合对象
          List<String> list = new ArrayList<String>();
  
          //添加元素
          list.add("hello");
          list.add("world");
          list.add("java");
  
          //获取列表迭代器
          ListIterator<String> lit = list.listIterator();
          while (lit.hasNext()) {
              String s = lit.next();
              if(s.equals("world")) {
                  lit.add("javaee");
              }
          }
  
          System.out.println(list);
  
      }
  }
  ```

**23.2.6增强for循环【应用】**

- 定义格式

  ```java
  for(元素数据类型 变量名 : 数组/集合对象名) {
      循环体;
  }
  ```

- 示例代码

  ```java
  public class ForDemo {
      public static void main(String[] args) {
          int[] arr = {1,2,3,4,5};
          for(int i : arr) {
              System.out.println(i);
          }
          
          System.out.println("--------");
  
          String[] strArray = {"hello","world","java"};
          for(String s : strArray) {
              System.out.println(s);
          }
          
          System.out.println("--------");
  
          List<String> list = new ArrayList<String>();
          list.add("hello");
          list.add("world");
          list.add("java");
  
          for(String s : list) {
              System.out.println(s);
          }
          
          System.out.println("--------");
  
          //内部原理是一个Iterator迭代器
          /*
          for(String s : list) {
              if(s.equals("world")) {
                  list.add("javaee"); //ConcurrentModificationException
              }
          }
          */
      }
  }
  ```

**23.2.7集合的案例-List集合存储学生对象三种方式遍历【应用】**

- 案例需求

  ​	创建一个存储学生对象的集合，存储3个学生对象，使用程序实现在控制台遍历该集合

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    ```

  - 测试类

    ```java
    public class ListDemo {
        public static void main(String[] args) {
            //创建List集合对象
            List<Student> list = new ArrayList<Student>();
    
            //创建学生对象
            Student s1 = new Student("林青霞", 30);
            Student s2 = new Student("张曼玉", 35);
            Student s3 = new Student("王祖贤", 33);
    
            //把学生添加到集合
            list.add(s1);
            list.add(s2);
            list.add(s3);
    
            //迭代器：集合特有的遍历方式
            Iterator<Student> it = list.iterator();
            while (it.hasNext()) {
                Student s = it.next();
                System.out.println(s.getName()+","+s.getAge());
            }
            System.out.println("--------");
    
            //普通for：带有索引的遍历方式
            for(int i=0; i<list.size(); i++) {
                Student s = list.get(i);
                System.out.println(s.getName()+","+s.getAge());
            }
            System.out.println("--------");
    
            //增强for：最方便的遍历方式
            for(Student s : list) {
                System.out.println(s.getName()+","+s.getAge());
            }
        }
    }
    ```

**23.3 数据结构**

**23.3.1数据结构之栈和队列【记忆】**

- 栈结构

  ​	先进后出

- 队列结构

  ​	先进先出

**23.3.2数据结构之数组和链表【记忆】**

- 数组结构

  ​	查询快、增删慢

- 队列结构

  ​	查询慢、增删快

**23.4 List集合的实现类**

**23.4.1List集合子类的特点【记忆】**

- ArrayList集合

  ​	底层是数组结构实现，查询快、增删慢

- LinkedList集合

  ​	底层是链表结构实现，查询慢、增删快

**23.4.2集合的案例-ArrayList集合存储学生对象三种方式遍历【应用】**

- 案例需求

  ​	创建一个存储学生对象的集合，存储3个学生对象，使用程序实现在控制台遍历该集合

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    ```

  - 测试类

    ```java
    public class ArrayListDemo {
        public static void main(String[] args) {
            //创建ArrayList集合对象
            ArrayList<Student> array = new ArrayList<Student>();
    
            //创建学生对象
            Student s1 = new Student("林青霞", 30);
            Student s2 = new Student("张曼玉", 35);
            Student s3 = new Student("王祖贤", 33);
    
            //把学生添加到集合
            array.add(s1);
            array.add(s2);
            array.add(s3);
    
            //迭代器：集合特有的遍历方式
            Iterator<Student> it = array.iterator();
            while (it.hasNext()) {
                Student s = it.next();
                System.out.println(s.getName() + "," + s.getAge());
            }
            System.out.println("--------");
    
            //普通for：带有索引的遍历方式
            for(int i=0; i<array.size(); i++) {
                Student s = array.get(i);
                System.out.println(s.getName() + "," + s.getAge());
            }
            System.out.println("--------");
    
            //增强for：最方便的遍历方式
            for(Student s : array) {
                System.out.println(s.getName() + "," + s.getAge());
            }
        }
    }
    ```

**23.4.3LinkedList集合的特有功能【应用】**

- 特有方法

  | 方法名                    | 说明                             |
  | ------------------------- | -------------------------------- |
  | public void addFirst(E e) | 在该列表开头插入指定的元素       |
  | public void addLast(E e)  | 将指定的元素追加到此列表的末尾   |
  | public E getFirst()       | 返回此列表中的第一个元素         |
  | public   E getLast()      | 返回此列表中的最后一个元素       |
  | public E removeFirst()    | 从此列表中删除并返回第一个元素   |
  | public   E removeLast()   | 从此列表中删除并返回最后一个元素 |

### 23.3 Set集合

**23.3.1Set集合概述和特点【应用】**

- Set集合的特点
  - 元素存取无序
  - 没有索引、只能通过迭代器或增强for循环遍历
  - 不能存储重复元素
- Set集合的基本使用

```java
public class SetDemo {
    public static void main(String[] args) {
        //创建集合对象
        Set<String> set = new HashSet<String>();

        //添加元素
        set.add("hello");
        set.add("world");
        set.add("java");
        //不包含重复元素的集合
        set.add("world");

        //遍历
        for(String s : set) {
            System.out.println(s);
        }
    }
}
```

**23.3.2哈希值【理解】**

- 哈希值简介

  ​	是JDK根据对象的地址或者字符串或者数字算出来的int类型的数值

- 如何获取哈希值

  ​	Object类中的public int hashCode()：返回对象的哈希码值

- 哈希值的特点

  - 同一个对象多次调用hashCode()方法返回的哈希值是相同的
  - 默认情况下，不同对象的哈希值是不同的。而重写hashCode()方法，可以实现让不同对象的哈希值相同

- 获取哈希值的代码

  - 学生类

  ```java
  public class Student {
      private String name;
      private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      @Override
      public int hashCode() {
          return 0;
      }
  }
  ```

  - 测试类

  ```java
  public class HashDemo {
      public static void main(String[] args) {
          //创建学生对象
          Student s1 = new Student("林青霞",30);
  
          //同一个对象多次调用hashCode()方法返回的哈希值是相同的
          System.out.println(s1.hashCode()); //1060830840
          System.out.println(s1.hashCode()); //1060830840
          System.out.println("--------");
  
          Student s2 = new Student("林青霞",30);
  
          //默认情况下，不同对象的哈希值是不相同的
          //通过方法重写，可以实现不同对象的哈希值是相同的
          System.out.println(s2.hashCode()); //2137211482
          System.out.println("--------");
  
          System.out.println("hello".hashCode()); //99162322
          System.out.println("world".hashCode()); //113318802
          System.out.println("java".hashCode()); //3254818
  
          System.out.println("world".hashCode()); //113318802
          System.out.println("--------");
  
          System.out.println("重地".hashCode()); //1179395
          System.out.println("通话".hashCode()); //1179395
      }
  }
  ```

**23.3.3HashSet集合概述和特点【应用】**

- HashSet集合的特点

  - 底层数据结构是哈希表
  - 对集合的迭代顺序不作任何保证，也就是说不保证存储和取出的元素顺序一致
  - 没有带索引的方法，所以不能使用普通for循环遍历
  - 由于是Set集合，所以是不包含重复元素的集合

- HashSet集合的基本使用

  ```java
  public class HashSetDemo01 {
      public static void main(String[] args) {
          //创建集合对象
          HashSet<String> hs = new HashSet<String>();
  
          //添加元素
          hs.add("hello");
          hs.add("world");
          hs.add("java");
  
          hs.add("world");
  
          //遍历
          for(String s : hs) {
              System.out.println(s);
          }
      }
  }
  ```

**23.3.4HashSet集合保证元素唯一性源码分析【理解】**

- HashSet集合保证元素唯一性的原理

  ​	1.根据对象的哈希值计算存储位置

  ​            如果当前位置没有元素则直接存入

  ​            如果当前位置有元素存在，则进入第二步

  ​     2.当前元素的元素和已经存在的元素比较哈希值

  ​            如果哈希值不同，则将当前元素进行存储

  ​            如果哈希值相同，则进入第三步

  ​     3.通过equals()方法比较两个元素的内容

  ​            如果内容不相同，则将当前元素进行存储

  ​            如果内容相同，则不存储当前元素

- HashSet集合保证元素唯一性的图解!

  ![HashSet集合保证元素唯一性](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/HashSet%E9%9B%86%E5%90%88%E4%BF%9D%E8%AF%81%E5%85%83%E7%B4%A0%E5%94%AF%E4%B8%80%E6%80%A7.png)

**23.3.5常见数据结构之哈希表【理解】**

![常见数据结构之哈希表](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B9%8B%E5%93%88%E5%B8%8C%E8%A1%A8.png)

**23.3.6HashSet集合存储学生对象并遍历【应用】**

- 案例需求

  - 创建一个存储学生对象的集合，存储多个学生对象，使用程序实现在控制台遍历该集合
  - 要求：学生对象的成员变量值相同，我们就认为是同一个对象

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (o == null || getClass() != o.getClass()) return false;
    
            Student student = (Student) o;
    
            if (age != student.age) return false;
            return name != null ? name.equals(student.name) : student.name == null;
        }
    
        @Override
        public int hashCode() {
            int result = name != null ? name.hashCode() : 0;
            result = 31 * result + age;
            return result;
        }
    }
    ```

  - 测试类

    ```java
    public class HashSetDemo02 {
        public static void main(String[] args) {
            //创建HashSet集合对象
            HashSet<Student> hs = new HashSet<Student>();
    
            //创建学生对象
            Student s1 = new Student("林青霞", 30);
            Student s2 = new Student("张曼玉", 35);
            Student s3 = new Student("王祖贤", 33);
    
            Student s4 = new Student("王祖贤", 33);
    
            //把学生添加到集合
            hs.add(s1);
            hs.add(s2);
            hs.add(s3);
            hs.add(s4);
    
            //遍历集合(增强for)
            for (Student s : hs) {
                System.out.println(s.getName() + "," + s.getAge());
            }
        }
    }
    ```

**23.3.7LinkedHashSet集合概述和特点【应用】**

- LinkedHashSet集合特点

  - 哈希表和链表实现的Set接口，具有可预测的迭代次序
  - 由链表保证元素有序，也就是说元素的存储和取出顺序是一致的
  - 由哈希表保证元素唯一，也就是说没有重复的元素

- LinkedHashSet集合基本使用

  ```java
  public class LinkedHashSetDemo {
      public static void main(String[] args) {
          //创建集合对象
          LinkedHashSet<String> linkedHashSet = new LinkedHashSet<String>();
  
          //添加元素
          linkedHashSet.add("hello");
          linkedHashSet.add("world");
          linkedHashSet.add("java");
  
          linkedHashSet.add("world");
  
          //遍历集合
          for(String s : linkedHashSet) {
              System.out.println(s);
          }
      }
  }
  ```

**23.4 Set集合排序**

**23.4.1TreeSet集合概述和特点【应用】**

- TreeSet集合概述

  - 元素有序，可以按照一定的规则进行排序，具体排序方式取决于构造方法
    - TreeSet()：根据其元素的自然排序进行排序
    - TreeSet(Comparator comparator) ：根据指定的比较器进行排序
  - 没有带索引的方法，所以不能使用普通for循环遍历
  - 由于是Set集合，所以不包含重复元素的集合

- TreeSet集合基本使用

  ```java
  public class TreeSetDemo01 {
      public static void main(String[] args) {
          //创建集合对象
          TreeSet<Integer> ts = new TreeSet<Integer>();
  
          //添加元素
          ts.add(10);
          ts.add(40);
          ts.add(30);
          ts.add(50);
          ts.add(20);
  
          ts.add(30);
  
          //遍历集合
          for(Integer i : ts) {
              System.out.println(i);
          }
      }
  }
  ```

**23.4.2自然排序Comparable的使用【应用】**

- 案例需求

  - 存储学生对象并遍历，创建TreeSet集合使用无参构造方法
  - 要求：按照年龄从小到大排序，年龄相同时，按照姓名的字母顺序排序

- 实现步骤

  - 用TreeSet集合存储自定义对象，无参构造方法使用的是自然排序对元素进行排序的
  - 自然排序，就是让元素所属的类实现Comparable接口，重写compareTo(T o)方法
  - 重写方法时，一定要注意排序规则必须按照要求的主要条件和次要条件来写

- 代码实现

  - 学生类

    ```java
    public class Student implements Comparable<Student> {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
        @Override
        public int compareTo(Student s) {
    //        return 0;
    //        return 1;
    //        return -1;
            //按照年龄从小到大排序
           int num = this.age - s.age;
    //        int num = s.age - this.age;
            //年龄相同时，按照姓名的字母顺序排序
           int num2 = num==0?this.name.compareTo(s.name):num;
            return num2;
        }
    }
    ```

  - 测试类

    ```java
    public class TreeSetDemo02 {
        public static void main(String[] args) {
            //创建集合对象
            TreeSet<Student> ts = new TreeSet<Student>();
    
            //创建学生对象
            Student s1 = new Student("xishi", 29);
            Student s2 = new Student("wangzhaojun", 28);
            Student s3 = new Student("diaochan", 30);
            Student s4 = new Student("yangyuhuan", 33);
    
            Student s5 = new Student("linqingxia",33);
            Student s6 = new Student("linqingxia",33);
    
            //把学生添加到集合
            ts.add(s1);
            ts.add(s2);
            ts.add(s3);
            ts.add(s4);
            ts.add(s5);
            ts.add(s6);
    
            //遍历集合
            for (Student s : ts) {
                System.out.println(s.getName() + "," + s.getAge());
            }
        }
    }
    ```

**23.4.3比较器排序Comparator的使用【应用】**

- 案例需求

  - 存储学生对象并遍历，创建TreeSet集合使用带参构造方法
  - 要求：按照年龄从小到大排序，年龄相同时，按照姓名的字母顺序排序

- 实现步骤

  - 用TreeSet集合存储自定义对象，带参构造方法使用的是比较器排序对元素进行排序的
  - 比较器排序，就是让集合构造方法接收Comparator的实现类对象，重写compare(T o1,T o2)方法
  - 重写方法时，一定要注意排序规则必须按照要求的主要条件和次要条件来写

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    ```

  - 测试类

    ```java
    public class TreeSetDemo {
        public static void main(String[] args) {
            //创建集合对象
            TreeSet<Student> ts = new TreeSet<Student>(new Comparator<Student>() {
                @Override
                public int compare(Student s1, Student s2) {
                    //this.age - s.age
                    //s1,s2
                    int num = s1.getAge() - s2.getAge();
                    int num2 = num == 0 ? s1.getName().compareTo(s2.getName()) : num;
                    return num2;
                }
            });
    
            //创建学生对象
            Student s1 = new Student("xishi", 29);
            Student s2 = new Student("wangzhaojun", 28);
            Student s3 = new Student("diaochan", 30);
            Student s4 = new Student("yangyuhuan", 33);
    
            Student s5 = new Student("linqingxia",33);
            Student s6 = new Student("linqingxia",33);
    
            //把学生添加到集合
            ts.add(s1);
            ts.add(s2);
            ts.add(s3);
            ts.add(s4);
            ts.add(s5);
            ts.add(s6);
    
            //遍历集合
            for (Student s : ts) {
                System.out.println(s.getName() + "," + s.getAge());
            }
        }
    }
    ```

**23.4.4成绩排序案例【应用】**

- 案例需求

  - 用TreeSet集合存储多个学生信息(姓名，语文成绩，数学成绩)，并遍历该集合
  - 要求：按照总分从高到低出现

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int chinese;
        private int math;
    
        public Student() {
        }
    
        public Student(String name, int chinese, int math) {
            this.name = name;
            this.chinese = chinese;
            this.math = math;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getChinese() {
            return chinese;
        }
    
        public void setChinese(int chinese) {
            this.chinese = chinese;
        }
    
        public int getMath() {
            return math;
        }
    
        public void setMath(int math) {
            this.math = math;
        }
    
        public int getSum() {
            return this.chinese + this.math;
        }
    }
    ```

  - 测试类

    ```java
    public class TreeSetDemo {
        public static void main(String[] args) {
            //创建TreeSet集合对象，通过比较器排序进行排序
            TreeSet<Student> ts = new TreeSet<Student>(new Comparator<Student>() {
                @Override
                public int compare(Student s1, Student s2) {
    //                int num = (s2.getChinese()+s2.getMath())-(s1.getChinese()+s1.getMath());
                    //主要条件
                    int num = s2.getSum() - s1.getSum();
                    //次要条件
                    int num2 = num == 0 ? s1.getChinese() - s2.getChinese() : num;
                    int num3 = num2 == 0 ? s1.getName().compareTo(s2.getName()) : num2;
                    return num3;
                }
            });
    
            //创建学生对象
            Student s1 = new Student("林青霞", 98, 100);
            Student s2 = new Student("张曼玉", 95, 95);
            Student s3 = new Student("王祖贤", 100, 93);
            Student s4 = new Student("柳岩", 100, 97);
            Student s5 = new Student("风清扬", 98, 98);
    
            Student s6 = new Student("左冷禅", 97, 99);
    //        Student s7 = new Student("左冷禅", 97, 99);
            Student s7 = new Student("赵云", 97, 99);
    
            //把学生对象添加到集合
            ts.add(s1);
            ts.add(s2);
            ts.add(s3);
            ts.add(s4);
            ts.add(s5);
            ts.add(s6);
            ts.add(s7);
    
            //遍历集合
            for (Student s : ts) {
                System.out.println(s.getName() + "," + s.getChinese() + "," + s.getMath() + "," + s.getSum());
            }
        }
    }
    ```

**23.4.5不重复的随机数案例【应用】**

- 案例需求

  - 编写一个程序，获取10个1-20之间的随机数，要求随机数不能重复，并在控制台输出

- 代码实现

  ```java
  public class SetDemo {
      public static void main(String[] args) {
          //创建Set集合对象
  //        Set<Integer> set = new HashSet<Integer>();
          Set<Integer> set = new TreeSet<Integer>();
  
          //创建随机数对象
          Random r = new Random();
  
          //判断集合的长度是不是小于10
          while (set.size()<10) {
              //产生一个随机数，添加到集合
              int number = r.nextInt(20) + 1;
              set.add(number);
          }
  
          //遍历集合
          for(Integer i : set) {
              System.out.println(i);
          }
      }
  }
  ```

### 23.5 Map集合

**23.5.1Map集合概述和特点【理解】**

- Map集合概述

  ```java
  interface Map<K,V>  K：键的类型；V：值的类型
  ```

- Map集合的特点

  - 键值对映射关系
  - 一个键对应一个值
  - 键不能重复，值可以重复
  - 元素存取无序

- Map集合的基本使用

  ```java
  public class MapDemo01 {
      public static void main(String[] args) {
          //创建集合对象
          Map<String,String> map = new HashMap<String,String>();
  
          //V put(K key, V value) 将指定的值与该映射中的指定键相关联
          map.put("itheima001","林青霞");
          map.put("itheima002","张曼玉");
          map.put("itheima003","王祖贤");
          map.put("itheima003","柳岩");
  
          //输出集合对象
          System.out.println(map);
      }
  }
  ```

**23.5.2Map集合的基本功能【应用】**

- 方法介绍

  | 方法名                              | 说明                                 |
  | ----------------------------------- | ------------------------------------ |
  | V   put(K key,V   value)            | 添加元素                             |
  | V   remove(Object key)              | 根据键删除键值对元素                 |
  | void   clear()                      | 移除所有的键值对元素                 |
  | boolean containsKey(Object key)     | 判断集合是否包含指定的键             |
  | boolean containsValue(Object value) | 判断集合是否包含指定的值             |
  | boolean isEmpty()                   | 判断集合是否为空                     |
  | int size()                          | 集合的长度，也就是集合中键值对的个数 |

- 示例代码

  ```java
  public class MapDemo02 {
      public static void main(String[] args) {
          //创建集合对象
          Map<String,String> map = new HashMap<String,String>();
  
          //V put(K key,V value)：添加元素
          map.put("张无忌","赵敏");
          map.put("郭靖","黄蓉");
          map.put("杨过","小龙女");
  
          //V remove(Object key)：根据键删除键值对元素
  //        System.out.println(map.remove("郭靖"));
  //        System.out.println(map.remove("郭襄"));
  
          //void clear()：移除所有的键值对元素
  //        map.clear();
  
          //boolean containsKey(Object key)：判断集合是否包含指定的键
  //        System.out.println(map.containsKey("郭靖"));
  //        System.out.println(map.containsKey("郭襄"));
  
          //boolean isEmpty()：判断集合是否为空
  //        System.out.println(map.isEmpty());
  
          //int size()：集合的长度，也就是集合中键值对的个数
          System.out.println(map.size());
  
  
          //输出集合对象
          System.out.println(map);
      }
  }
  ```

**23.5.3Map集合的获取功能【应用】**

- 方法介绍

  | 方法名                           | 说明                     |
  | -------------------------------- | ------------------------ |
  | V   get(Object key)              | 根据键获取值             |
  | Set<K>   keySet()                | 获取所有键的集合         |
  | Collection<V>   values()         | 获取所有值的集合         |
  | Set<Map.Entry<K,V>>   entrySet() | 获取所有键值对对象的集合 |

- 示例代码

  ```java
  public class MapDemo03 {
      public static void main(String[] args) {
          //创建集合对象
          Map<String, String> map = new HashMap<String, String>();
  
          //添加元素
          map.put("张无忌", "赵敏");
          map.put("郭靖", "黄蓉");
          map.put("杨过", "小龙女");
  
          //V get(Object key):根据键获取值
  //        System.out.println(map.get("张无忌"));
  //        System.out.println(map.get("张三丰"));
  
          //Set<K> keySet():获取所有键的集合
  //        Set<String> keySet = map.keySet();
  //        for(String key : keySet) {
  //            System.out.println(key);
  //        }
  
          //Collection<V> values():获取所有值的集合
          Collection<String> values = map.values();
          for(String value : values) {
              System.out.println(value);
          }
      }
  }
  ```

**23.5.4Map集合的遍历(方式1)【应用】**

- 遍历思路

  - 我们刚才存储的元素都是成对出现的，所以我们把Map看成是一个夫妻对的集合
    - 把所有的丈夫给集中起来
    - 遍历丈夫的集合，获取到每一个丈夫
    - 根据丈夫去找对应的妻子

- 步骤分析

  - 获取所有键的集合。用keySet()方法实现
  - 遍历键的集合，获取到每一个键。用增强for实现  
  - 根据键去找值。用get(Object key)方法实现

- 代码实现

  ```java
  public class MapDemo01 {
      public static void main(String[] args) {
          //创建集合对象
          Map<String, String> map = new HashMap<String, String>();
  
          //添加元素
          map.put("张无忌", "赵敏");
          map.put("郭靖", "黄蓉");
          map.put("杨过", "小龙女");
  
          //获取所有键的集合。用keySet()方法实现
          Set<String> keySet = map.keySet();
          //遍历键的集合，获取到每一个键。用增强for实现
          for (String key : keySet) {
              //根据键去找值。用get(Object key)方法实现
              String value = map.get(key);
              System.out.println(key + "," + value);
          }
      }
  }
  ```

**23.5.5Map集合的遍历(方式2)【应用】**

- 遍历思路

  - 我们刚才存储的元素都是成对出现的，所以我们把Map看成是一个夫妻对的集合
    - 获取所有结婚证的集合
    - 遍历结婚证的集合，得到每一个结婚证
    - 根据结婚证获取丈夫和妻子

- 步骤分析

  - 获取所有键值对对象的集合
    - Set<Map.Entry<K,V>> entrySet()：获取所有键值对对象的集合
  - 遍历键值对对象的集合，得到每一个键值对对象
    - 用增强for实现，得到每一个Map.Entry
  - 根据键值对对象获取键和值
    - 用getKey()得到键
    - 用getValue()得到值

- 代码实现

  ```java
  public class MapDemo02 {
      public static void main(String[] args) {
          //创建集合对象
          Map<String, String> map = new HashMap<String, String>();
  
          //添加元素
          map.put("张无忌", "赵敏");
          map.put("郭靖", "黄蓉");
          map.put("杨过", "小龙女");
  
          //获取所有键值对对象的集合
          Set<Map.Entry<String, String>> entrySet = map.entrySet();
          //遍历键值对对象的集合，得到每一个键值对对象
          for (Map.Entry<String, String> me : entrySet) {
              //根据键值对对象获取键和值
              String key = me.getKey();
              String value = me.getValue();
              System.out.println(key + "," + value);
          }
      }
  }
  ```

**23.5.6Map集合的案例【应用】**

**23.5.6.1HashMap集合练习之键是String值是Student**

- 案例需求

  ​	创建一个HashMap集合，键是学号(String)，值是学生对象(Student)。存储三个键值对元素，并遍历

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    ```

  - 测试类

    ```java
    /*
        需求：
            创建一个HashMap集合，键是学号(String)，值是学生对象(Student)。存储三个键值对元素，并遍历
    
        思路：
            1:定义学生类
            2:创建HashMap集合对象
            3:创建学生对象
            4:把学生添加到集合
            5:遍历集合
                方式1：键找值
                方式2：键值对对象找键和值
     */
    public class HashMapDemo {
        public static void main(String[] args) {
            //创建HashMap集合对象
            HashMap<String, Student> hm = new HashMap<String, Student>();
    
            //创建学生对象
            Student s1 = new Student("林青霞", 30);
            Student s2 = new Student("张曼玉", 35);
            Student s3 = new Student("王祖贤", 33);
    
            //把学生添加到集合
            hm.put("itheima001", s1);
            hm.put("itheima002", s2);
            hm.put("itheima003", s3);
    
            //方式1：键找值
            Set<String> keySet = hm.keySet();
            for (String key : keySet) {
                Student value = hm.get(key);
                System.out.println(key + "," + value.getName() + "," + value.getAge());
            }
            System.out.println("--------");
    
            //方式2：键值对对象找键和值
            Set<Map.Entry<String, Student>> entrySet = hm.entrySet();
            for (Map.Entry<String, Student> me : entrySet) {
                String key = me.getKey();
                Student value = me.getValue();
                System.out.println(key + "," + value.getName() + "," + value.getAge());
            }
        }
    }
    ```

**23.5.6.2HashMap集合练习之键是Student值是String**

- 案例需求

  - 创建一个HashMap集合，键是学生对象(Student)，值是居住地 (String)。存储多个元素，并遍历。
  - 要求保证键的唯一性：如果学生对象的成员变量值相同，我们就认为是同一个对象

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (o == null || getClass() != o.getClass()) return false;
    
            Student student = (Student) o;
    
            if (age != student.age) return false;
            return name != null ? name.equals(student.name) : student.name == null;
        }
    
        @Override
        public int hashCode() {
            int result = name != null ? name.hashCode() : 0;
            result = 31 * result + age;
            return result;
        }
    }
    ```

  - 测试类

    ```java
    public class HashMapDemo {
        public static void main(String[] args) {
            //创建HashMap集合对象
            HashMap<Student, String> hm = new HashMap<Student, String>();
    
            //创建学生对象
            Student s1 = new Student("林青霞", 30);
            Student s2 = new Student("张曼玉", 35);
            Student s3 = new Student("王祖贤", 33);
            Student s4 = new Student("王祖贤", 33);
    
            //把学生添加到集合
            hm.put(s1, "西安");
            hm.put(s2, "武汉");
            hm.put(s3, "郑州");
            hm.put(s4, "北京");
    
            //遍历集合
            Set<Student> keySet = hm.keySet();
            for (Student key : keySet) {
                String value = hm.get(key);
                System.out.println(key.getName() + "," + key.getAge() + "," + value);
            }
        }
    }
    ```

**23.5.6.3集合嵌套之ArrayList嵌套HashMap**

- 案例需求

  - 创建一个ArrayList集合，存储三个元素，每一个元素都是HashMap
  - 每一个HashMap的键和值都是String，并遍历。

- 代码实现

  ```java
  public class ArrayListIncludeHashMapDemo {
      public static void main(String[] args) {
          //创建ArrayList集合
          ArrayList<HashMap<String, String>> array = new ArrayList<HashMap<String, String>>();
  
          //创建HashMap集合，并添加键值对元素
          HashMap<String, String> hm1 = new HashMap<String, String>();
          hm1.put("孙策", "大乔");
          hm1.put("周瑜", "小乔");
          //把HashMap作为元素添加到ArrayList集合
          array.add(hm1);
  
          HashMap<String, String> hm2 = new HashMap<String, String>();
          hm2.put("郭靖", "黄蓉");
          hm2.put("杨过", "小龙女");
          //把HashMap作为元素添加到ArrayList集合
          array.add(hm2);
  
          HashMap<String, String> hm3 = new HashMap<String, String>();
          hm3.put("令狐冲", "任盈盈");
          hm3.put("林平之", "岳灵珊");
          //把HashMap作为元素添加到ArrayList集合
          array.add(hm3);
  
          //遍历ArrayList集合
          for (HashMap<String, String> hm : array) {
              Set<String> keySet = hm.keySet();
              for (String key : keySet) {
                  String value = hm.get(key);
                  System.out.println(key + "," + value);
              }
          }
      }
  }
  ```

**23.5.6.4集合嵌套之HashMap嵌套ArrayList**

- 案例需求

  - 创建一个HashMap集合，存储三个键值对元素，每一个键值对元素的键是String，值是ArrayList
  - 每一个ArrayList的元素是String，并遍历。

- 代码实现

  ```java
  public class HashMapIncludeArrayListDemo {
      public static void main(String[] args) {
          //创建HashMap集合
          HashMap<String, ArrayList<String>> hm = new HashMap<String, ArrayList<String>>();
  
          //创建ArrayList集合，并添加元素
          ArrayList<String> sgyy = new ArrayList<String>();
          sgyy.add("诸葛亮");
          sgyy.add("赵云");
          //把ArrayList作为元素添加到HashMap集合
          hm.put("三国演义",sgyy);
  
          ArrayList<String> xyj = new ArrayList<String>();
          xyj.add("唐僧");
          xyj.add("孙悟空");
          //把ArrayList作为元素添加到HashMap集合
          hm.put("西游记",xyj);
  
          ArrayList<String> shz = new ArrayList<String>();
          shz.add("武松");
          shz.add("鲁智深");
          //把ArrayList作为元素添加到HashMap集合
          hm.put("水浒传",shz);
  
          //遍历HashMap集合
          Set<String> keySet = hm.keySet();
          for(String key : keySet) {
              System.out.println(key);
              ArrayList<String> value = hm.get(key);
              for(String s : value) {
                  System.out.println("\t" + s);
              }
          }
      }
  }
  ```

**23.5.6.5统计字符串中每个字符出现的次数**

- 案例需求

  - 键盘录入一个字符串，要求统计字符串中每个字符串出现的次数。
  - 举例：键盘录入“aababcabcdabcde”  在控制台输出：“a(5)b(4)c(3)d(2)e(1)”

- 代码实现

  ```java
  public class HashMapDemo {
      public static void main(String[] args) {
          //键盘录入一个字符串
          Scanner sc = new Scanner(System.in);
          System.out.println("请输入一个字符串：");
          String line = sc.nextLine();
  
          //创建HashMap集合，键是Character，值是Integer
  //        HashMap<Character, Integer> hm = new HashMap<Character, Integer>();
          TreeMap<Character, Integer> hm = new TreeMap<Character, Integer>();
  
          //遍历字符串，得到每一个字符
          for (int i = 0; i < line.length(); i++) {
              char key = line.charAt(i);
  
              //拿得到的每一个字符作为键到HashMap集合中去找对应的值，看其返回值
              Integer value = hm.get(key);
  
              if (value == null) {
                  //如果返回值是null：说明该字符在HashMap集合中不存在，就把该字符作为键，1作为值存储
                  hm.put(key,1);
              } else {
                  //如果返回值不是null：说明该字符在HashMap集合中存在，把该值加1，然后重新存储该字符和对应的值
                  value++;
                  hm.put(key,value);
              }
          }
  
          //遍历HashMap集合，得到键和值，按照要求进行拼接
          StringBuilder sb = new StringBuilder();
  
          Set<Character> keySet = hm.keySet();
          for(Character key : keySet) {
              Integer value = hm.get(key);
              sb.append(key).append("(").append(value).append(")");
          }
  
          String result = sb.toString();
  
          //输出结果
          System.out.println(result);
      }
  }
  ```

**23.6 Collections集合工具类**

**23.6.1Collections概述和使用【应用】**

- Collections类的作用

  ​	是针对集合操作的工具类

- Collections类常用方法

  | 方法名                                   | 说明                               |
  | ---------------------------------------- | ---------------------------------- |
  | public static void sort(List<T> list)    | 将指定的列表按升序排序             |
  | public static void reverse(List<?> list) | 反转指定列表中元素的顺序           |
  | public static void shuffle(List<?> list) | 使用默认的随机源随机排列指定的列表 |

- 示例代码

  ```java
  public class CollectionsDemo01 {
      public static void main(String[] args) {
          //创建集合对象
          List<Integer> list = new ArrayList<Integer>();
  
          //添加元素
          list.add(30);
          list.add(20);
          list.add(50);
          list.add(10);
          list.add(40);
  
          //public static <T extends Comparable<? super T>> void sort(List<T> list)：将指定的列表按升序排序
  //        Collections.sort(list);
  
          //public static void reverse(List<?> list)：反转指定列表中元素的顺序
  //        Collections.reverse(list);
  
          //public static void shuffle(List<?> list)：使用默认的随机源随机排列指定的列表
          Collections.shuffle(list);
  
          System.out.println(list);
      }
  }
  ```

**23.6.2ArrayList集合存储学生并排序【应用】**

- 案例需求

  - ArrayList存储学生对象，使用Collections对ArrayList进行排序
  - 要求：按照年龄从小到大排序，年龄相同时，按照姓名的字母顺序排序

- 代码实现

  - 学生类

    ```java
    public class Student {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    }
    ```

  - 测试类

    ```java
    public class CollectionsDemo02 {
        public static void main(String[] args) {
            //创建ArrayList集合对象
            ArrayList<Student> array = new ArrayList<Student>();
    
            //创建学生对象
            Student s1 = new Student("linqingxia", 30);
            Student s2 = new Student("zhangmanyu", 35);
            Student s3 = new Student("wangzuxian", 33);
            Student s4 = new Student("liuyan", 33);
    
            //把学生添加到集合
            array.add(s1);
            array.add(s2);
            array.add(s3);
            array.add(s4);
    
            //使用Collections对ArrayList集合排序
            //sort(List<T> list, Comparator<? super T> c)
            Collections.sort(array, new Comparator<Student>() {
                @Override
                public int compare(Student s1, Student s2) {
                    //按照年龄从小到大排序，年龄相同时，按照姓名的字母顺序排序
                    int num = s1.getAge() - s2.getAge();
                    int num2 = num == 0 ? s1.getName().compareTo(s2.getName()) : num;
                    return num2;
                }
            });
    
            //遍历集合
            for (Student s : array) {
                System.out.println(s.getName() + "," + s.getAge());
            }
        }
    }
    ```

**23.7 斗地主案例**

**23.7.1模拟斗地主案例-普通版本【应用】**

- 案例需求

  ​	通过程序实现斗地主过程中的洗牌，发牌和看牌

- 代码实现

  ```java
  public class PokerDemo {
      public static void main(String[] args) {
          //创建一个牌盒，也就是定义一个集合对象，用ArrayList集合实现
          ArrayList<String> array = new ArrayList<String>();
  
          //往牌盒里面装牌
          /*
              ♦2,♦3,♦4...♦K,♦A
              ♣2,...
              ♥2,...
              ♠2,...
              小王，大王
           */
          //定义花色数组
          String[] colors = {"♦", "♣", "♥", "♠"};
          //定义点数数组
          String[] numbers = {"2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"};
          for (String color : colors) {
              for (String number : numbers) {
                  array.add(color + number);
              }
          }
          array.add("小王");
          array.add("大王");
  
          //洗牌，也就是把牌打撒，用Collections的shuffle()方法实现
          Collections.shuffle(array);
  
  //        System.out.println(array);
  
          //发牌，也就是遍历集合，给三个玩家发牌
          ArrayList<String> lqxArray = new ArrayList<String>();
          ArrayList<String> lyArray = new ArrayList<String>();
          ArrayList<String> fqyArray = new ArrayList<String>();
          ArrayList<String> dpArray = new ArrayList<String>();
  
          for (int i = 0; i < array.size(); i++) {
              String poker = array.get(i);
              if (i >= array.size() - 3) {
                  dpArray.add(poker);
              } else if (i % 3 == 0) {
                  lqxArray.add(poker);
              } else if (i % 3 == 1) {
                  lyArray.add(poker);
              } else if (i % 3 == 2) {
                  fqyArray.add(poker);
              }
          }
  
          //看牌，也就是三个玩家分别遍历自己的牌
          lookPoker("林青霞", lqxArray);
          lookPoker("柳岩", lyArray);
          lookPoker("风清扬", fqyArray);
          lookPoker("底牌", dpArray);
      }
  
      //看牌的方法
      public static void lookPoker(String name, ArrayList<String> array) {
          System.out.print(name + "的牌是：");
          for (String poker : array) {
              System.out.print(poker + " ");
          }
          System.out.println();
      }
  }
  ```

**23.7.2模拟斗地主案例-升级版本【应用】**

- 案例需求

  ​	通过程序实现斗地主过程中的洗牌，发牌和看牌。要求：对牌进行排序

- 代码实现

  ```java
  public class PokerDemo {
      public static void main(String[] args) {
          //创建HashMap，键是编号，值是牌
          HashMap<Integer, String> hm = new HashMap<Integer, String>();
  
          //创建ArrayList，存储编号
          ArrayList<Integer> array = new ArrayList<Integer>();
  
          //创建花色数组和点数数组
          String[] colors = {"♦", "♣", "♥", "♠"};
          String[] numbers = {"3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"};
  
          //从0开始往HashMap里面存储编号，并存储对应的牌。同时往ArrayList里面存储编号
          int index = 0;
  
          for (String number : numbers) {
              for (String color : colors) {
                  hm.put(index, color + number);
                  array.add(index);
                  index++;
              }
          }
          hm.put(index, "小王");
          array.add(index);
          index++;
          hm.put(index, "大王");
          array.add(index);
  
          //洗牌(洗的是编号)，用Collections的shuffle()方法实现
          Collections.shuffle(array);
  
          //发牌(发的也是编号，为了保证编号是排序的，创建TreeSet集合接收)
          TreeSet<Integer> lqxSet = new TreeSet<Integer>();
          TreeSet<Integer> lySet = new TreeSet<Integer>();
          TreeSet<Integer> fqySet = new TreeSet<Integer>();
          TreeSet<Integer> dpSet = new TreeSet<Integer>();
  
          for (int i = 0; i < array.size(); i++) {
              int x = array.get(i);
              if (i >= array.size() - 3) {
                  dpSet.add(x);
              } else if (i % 3 == 0) {
                  lqxSet.add(x);
              } else if (i % 3 == 1) {
                  lySet.add(x);
              } else if (i % 3 == 2) {
                  fqySet.add(x);
              }
          }
  
          //调用看牌方法
          lookPoker("林青霞", lqxSet, hm);
          lookPoker("柳岩", lySet, hm);
          lookPoker("风清扬", fqySet, hm);
          lookPoker("底牌", dpSet, hm);
      }
  
      //定义方法看牌(遍历TreeSet集合，获取编号，到HashMap集合找对应的牌)
      public static void lookPoker(String name, TreeSet<Integer> ts, HashMap<Integer, String> hm) {
          System.out.print(name + "的牌是：");
          for (Integer key : ts) {
              String poker = hm.get(key);
              System.out.print(poker + " ");
          }
          System.out.println();
      }
  }
  ```

## 24 可变参数

**24.1可变参数【应用】**

- 可变参数介绍

  ​	可变参数又称参数个数可变，用作方法的形参出现，那么方法参数个数就是可变的了

- 可变参数定义格式

  ```java
  修饰符 返回值类型 方法名(数据类型… 变量名) {  }
  ```

- 可变参数的注意事项

  - 这里的变量其实是一个数组
  - 如果一个方法有多个参数，包含可变参数，可变参数要放在最后

- 可变参数的基本使用

  ```java
  public class ArgsDemo01 {
      public static void main(String[] args) {
          System.out.println(sum(10, 20));
          System.out.println(sum(10, 20, 30));
          System.out.println(sum(10, 20, 30, 40));
  
          System.out.println(sum(10,20,30,40,50));
          System.out.println(sum(10,20,30,40,50,60));
          System.out.println(sum(10,20,30,40,50,60,70));
          System.out.println(sum(10,20,30,40,50,60,70,80,90,100));
      }
  
  //    public static int sum(int b,int... a) {
  //        return 0;
  //    }
  
      public static int sum(int... a) {
          int sum = 0;
          for(int i : a) {
              sum += i;
          }
          return sum;
      }
  }
  ```

**24.2可变参数的使用【应用】**

- Arrays工具类中有一个静态方法：

  - public static <T> List<T> asList(T... a)：返回由指定数组支持的固定大小的列表
  - 返回的集合不能做增删操作，可以做修改操作

- List接口中有一个静态方法：

  - public static <E> List<E> of(E... elements)：返回包含任意数量元素的不可变列表
  - 返回的集合不能做增删改操作

- Set接口中有一个静态方法：

  - public static <E> Set<E> of(E... elements) ：返回一个包含任意数量元素的不可变集合
  - 在给元素的时候，不能给重复的元素
  - 返回的集合不能做增删操作，没有修改的方法

- 示例代码

  ```java
  public class ArgsDemo02 {
      public static void main(String[] args) {
          //public static <T> List<T> asList(T... a)：返回由指定数组支持的固定大小的列表
  //        List<String> list = Arrays.asList("hello", "world", "java");
  //
  ////        list.add("javaee"); //UnsupportedOperationException
  ////        list.remove("world"); //UnsupportedOperationException
  //        list.set(1,"javaee");
  //
  //        System.out.println(list);
  
          //public static <E> List<E> of(E... elements)：返回包含任意数量元素的不可变列表
  //        List<String> list = List.of("hello", "world", "java", "world");
  //
  ////        list.add("javaee");//UnsupportedOperationException
  ////        list.remove("java");//UnsupportedOperationException
  ////        list.set(1,"javaee");//UnsupportedOperationException
  //
  //        System.out.println(list);
  
          //public static <E> Set<E> of(E... elements) ：返回一个包含任意数量元素的不可变集合
  //        Set<String> set = Set.of("hello", "world", "java","world"); //IllegalArgumentException
          //Set<String> set = Set.of("hello", "world", "java");
  
  //        set.add("javaee");//UnsupportedOperationException
  //        set.remove("world");//UnsupportedOperationException
  
          //System.out.println(set);
      }
  }
  ```

## 25 File类

**25.1File类概述和构造方法【应用】**

- File类介绍

  - 它是文件和目录路径名的抽象表示
  - 文件和目录是可以通过File封装成对象的
  - 对于File而言，其封装的并不是一个真正存在的文件，仅仅是一个路径名而已。它可以是存在的，也可以是不存在的。将来是要通过具体的操作把这个路径的内容转换为具体存在的

- File类的构造方法

  | 方法名                              | 说明                                                        |
  | ----------------------------------- | ----------------------------------------------------------- |
  | File(String   pathname)             | 通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例 |
  | File(String   parent, String child) | 从父路径名字符串和子路径名字符串创建新的   File实例         |
  | File(File   parent, String child)   | 从父抽象路径名和子路径名字符串创建新的   File实例           |

- 示例代码

  ```java
  public class FileDemo01 {
      public static void main(String[] args) {
          //File(String pathname)：通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例。
          File f1 = new File("E:\\itcast\\java.txt");
          System.out.println(f1);
  
          //File(String parent, String child)：从父路径名字符串和子路径名字符串创建新的 File实例。
          File f2 = new File("E:\\itcast","java.txt");
          System.out.println(f2);
  
          //File(File parent, String child)：从父抽象路径名和子路径名字符串创建新的 File实例。
          File f3 = new File("E:\\itcast");
          File f4 = new File(f3,"java.txt");
          System.out.println(f4);
      }
  }
  ```

**25.2File类创建功能【应用】**

- 方法分类

  | 方法名                         | 说明                                                         |
  | ------------------------------ | ------------------------------------------------------------ |
  | public boolean createNewFile() | 当具有该名称的文件不存在时，创建一个由该抽象路径名命名的新空文件 |
  | public boolean mkdir()         | 创建由此抽象路径名命名的目录                                 |
  | public boolean mkdirs()        | 创建由此抽象路径名命名的目录，包括任何必需但不存在的父目录   |

- 示例代码

  ```java
  public class FileDemo02 {
      public static void main(String[] args) throws IOException {
          //需求1：我要在E:\\itcast目录下创建一个文件java.txt
          File f1 = new File("E:\\itcast\\java.txt");
          System.out.println(f1.createNewFile());
          System.out.println("--------");
  
          //需求2：我要在E:\\itcast目录下创建一个目录JavaSE
          File f2 = new File("E:\\itcast\\JavaSE");
          System.out.println(f2.mkdir());
          System.out.println("--------");
  
          //需求3：我要在E:\\itcast目录下创建一个多级目录JavaWEB\\HTML
          File f3 = new File("E:\\itcast\\JavaWEB\\HTML");
  //        System.out.println(f3.mkdir());
          System.out.println(f3.mkdirs());
          System.out.println("--------");
  
          //需求4：我要在E:\\itcast目录下创建一个文件javase.txt
          File f4 = new File("E:\\itcast\\javase.txt");
  //        System.out.println(f4.mkdir());
          System.out.println(f4.createNewFile());
      }
  }
  ```

**25.3File类判断和获取功能【应用】**

- 判断功能

  | 方法名                         | 说明                                 |
  | ------------------------------ | ------------------------------------ |
  | public   boolean isDirectory() | 测试此抽象路径名表示的File是否为目录 |
  | public   boolean isFile()      | 测试此抽象路径名表示的File是否为文件 |
  | public   boolean   exists()    | 测试此抽象路径名表示的File是否存在   |

- 获取功能

  | 方法名                            | 说明                                                     |
  | --------------------------------- | -------------------------------------------------------- |
  | public   String getAbsolutePath() | 返回此抽象路径名的绝对路径名字符串                       |
  | public   String getPath()         | 将此抽象路径名转换为路径名字符串                         |
  | public   String getName()         | 返回由此抽象路径名表示的文件或目录的名称                 |
  | public   String[] list()          | 返回此抽象路径名表示的目录中的文件和目录的名称字符串数组 |
  | public   File[] listFiles()       | 返回此抽象路径名表示的目录中的文件和目录的File对象数组   |

- 示例代码

  ```java
  public class FileDemo04 {
      public static void main(String[] args) {
          //创建一个File对象
          File f = new File("myFile\\java.txt");
  
  //        public boolean isDirectory()：测试此抽象路径名表示的File是否为目录
  //        public boolean isFile()：测试此抽象路径名表示的File是否为文件
  //        public boolean exists()：测试此抽象路径名表示的File是否存在
          System.out.println(f.isDirectory());
          System.out.println(f.isFile());
          System.out.println(f.exists());
  
  //        public String getAbsolutePath()：返回此抽象路径名的绝对路径名字符串
  //        public String getPath()：将此抽象路径名转换为路径名字符串
  //        public String getName()：返回由此抽象路径名表示的文件或目录的名称
          System.out.println(f.getAbsolutePath());
          System.out.println(f.getPath());
          System.out.println(f.getName());
          System.out.println("--------");
  
  //        public String[] list()：返回此抽象路径名表示的目录中的文件和目录的名称字符串数组
  //        public File[] listFiles()：返回此抽象路径名表示的目录中的文件和目录的File对象数组
          File f2 = new File("E:\\itcast");
  
          String[] strArray = f2.list();
          for(String str : strArray) {
              System.out.println(str);
          }
          System.out.println("--------");
  
          File[] fileArray = f2.listFiles();
          for(File file : fileArray) {
  //            System.out.println(file);
  //            System.out.println(file.getName());
              if(file.isFile()) {
                  System.out.println(file.getName());
              }
          }
      }
  }
  ```

**25.4 File类删除功能【应用】**

- 方法分类

  | 方法名                    | 说明                               |
  | ------------------------- | ---------------------------------- |
  | public boolean   delete() | 删除由此抽象路径名表示的文件或目录 |

- 示例代码

  ```java
  public class FileDemo03 {
      public static void main(String[] args) throws IOException {
  //        File f1 = new File("E:\\itcast\\java.txt");
          //需求1：在当前模块目录下创建java.txt文件
          File f1 = new File("myFile\\java.txt");
  //        System.out.println(f1.createNewFile());
  
          //需求2：删除当前模块目录下的java.txt文件
          System.out.println(f1.delete());
          System.out.println("--------");
  
          //需求3：在当前模块目录下创建itcast目录
          File f2 = new File("myFile\\itcast");
  //        System.out.println(f2.mkdir());
  
          //需求4：删除当前模块目录下的itcast目录
          System.out.println(f2.delete());
          System.out.println("--------");
  
          //需求5：在当前模块下创建一个目录itcast,然后在该目录下创建一个文件java.txt
          File f3 = new File("myFile\\itcast");
  //        System.out.println(f3.mkdir());
          File f4 = new File("myFile\\itcast\\java.txt");
  //        System.out.println(f4.createNewFile());
  
          //需求6：删除当前模块下的目录itcast
          System.out.println(f4.delete());
          System.out.println(f3.delete());
      }
  }
  ```

- 绝对路径和相对路径的区别

  - 绝对路径：完整的路径名，不需要任何其他信息就可以定位它所表示的文件。例如：E:\itcast\java.txt
  - 相对路径：必须使用取自其他路径名的信息进行解释。例如：myFile\\java.txt

## 26 递归

**26.1递归【应用】**

- 递归的介绍

  - 以编程的角度来看，递归指的是方法定义中调用方法本身的现象
  - 把一个复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解
  - 递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算

- 递归的基本使用

  ```java
  public class DiGuiDemo {
      public static void main(String[] args) {
          //回顾不死神兔问题，求第20个月兔子的对数
          //每个月的兔子对数：1,1,2,3,5,8，...
          int[] arr = new int[20];
  
          arr[0] = 1;
          arr[1] = 1;
  
          for (int i = 2; i < arr.length; i++) {
              arr[i] = arr[i - 1] + arr[i - 2];
          }
          System.out.println(arr[19]);
          System.out.println(f(20));
      }
  
      /*
          递归解决问题，首先就是要定义一个方法：
              定义一个方法f(n)：表示第n个月的兔子对数
              那么，第n-1个月的兔子对数该如何表示呢？f(n-1)
              同理，第n-2个月的兔子对数该如何表示呢？f(n-2)
  
          StackOverflowError:当堆栈溢出发生时抛出一个应用程序递归太深
       */
      public static int f(int n) {
          if(n==1 || n==2) {
              return 1;
          } else {
              return f(n - 1) + f(n - 2);
          }
      }
  }
  ```

- 递归的注意事项

  - 递归一定要有出口。否则内存溢出
  - 递归虽然有出口，但是递归的次数也不宜过多。否则内存溢出

**26.2递归求阶乘【应用】**

- 案例需求

  ​	用递归求5的阶乘，并把结果在控制台输出

- 代码实现

  ```java
  public class DiGuiDemo01 {
      public static void main(String[] args) {
          //调用方法
          int result = jc(5);
          //输出结果
          System.out.println("5的阶乘是：" + result);
      }
  
      //定义一个方法，用于递归求阶乘，参数为一个int类型的变量
      public static int jc(int n) {
          //在方法内部判断该变量的值是否是1
          if(n == 1) {
              //是：返回1
              return 1;
          } else {
              //不是：返回n*(n-1)!
              return n*jc(n-1);
          }
      }
  }
  ```

**26.3递归遍历目录【应用】**

- 案例需求

  ​	给定一个路径(E:\\itcast)，通过递归完成遍历该目录下所有内容，并把所有文件的绝对路径输出在控制台

- 代码实现

  ```java
  public class DiGuiDemo02 {
      public static void main(String[] args) {
          //根据给定的路径创建一个File对象
  //        File srcFile = new File("E:\\itcast");
          File srcFile = new File("E:\\itheima");
  
          //调用方法
          getAllFilePath(srcFile);
      }
  
      //定义一个方法，用于获取给定目录下的所有内容，参数为第1步创建的File对象
      public static void getAllFilePath(File srcFile) {
          //获取给定的File目录下所有的文件或者目录的File数组
          File[] fileArray = srcFile.listFiles();
          //遍历该File数组，得到每一个File对象
          if(fileArray != null) {
              for(File file : fileArray) {
                  //判断该File对象是否是目录
                  if(file.isDirectory()) {
                      //是：递归调用
                      getAllFilePath(file);
                  } else {
                      //不是：获取绝对路径输出在控制台
                      System.out.println(file.getAbsolutePath());
                  }
              }
          }
      }
  }
  ```

## 27 IO流

**27.1 IO流概述和分类【理解】**

- IO流介绍
  - IO：输入/输出(Input/Output)
  - 流：是一种抽象概念，是对数据传输的总称。也就是说数据在设备间的传输称为流，流的本质是数据传输
  - IO流就是用来处理设备间数据传输问题的。常见的应用：文件复制；文件上传；文件下载
- IO流的分类
  - 按照数据的流向
    - 输入流：读数据
    - 输出流：写数据
  - 按照数据类型来分
    - 字节流
      - 字节输入流
      - 字节输出流
    - 字符流
      - 字符输入流
      - 字符输出流
- IO流的使用场景
  - 如果操作的是纯文本文件，优先使用字符流
  - 如果操作的是图片、视频、音频等二进制文件。优先使用字节流
  - 如果不确定文件类型，优先使用字节流。字节流是万能的流

**27.2字节流写数据【应用】**

- 字节流抽象基类

  - InputStream：这个抽象类是表示字节输入流的所有类的超类
  - OutputStream：这个抽象类是表示字节输出流的所有类的超类
  - 子类名特点：子类名称都是以其父类名作为子类名的后缀

- 字节输出流

  - FileOutputStream(String name)：创建文件输出流以指定的名称写入文件

- 使用字节输出流写数据的步骤

  - 创建字节输出流对象(调用系统功能创建了文件，创建字节输出流对象，让字节输出流对象指向文件)
  - 调用字节输出流对象的写数据方法
  - 释放资源(关闭此文件输出流并释放与此流相关联的任何系统资源)

- 示例代码

  ```java
  public class FileOutputStreamDemo01 {
      public static void main(String[] args) throws IOException {
          //创建字节输出流对象
          //FileOutputStream(String name)：创建文件输出流以指定的名称写入文件
          FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
          /*
              做了三件事情：
                  A:调用系统功能创建了文件
                  B:创建了字节输出流对象
                  C:让字节输出流对象指向创建好的文件
           */
  
          //void write(int b)：将指定的字节写入此文件输出流
          fos.write(97);
  //        fos.write(57);
  //        fos.write(55);
  
          //最后都要释放资源
          //void close()：关闭此文件输出流并释放与此流相关联的任何系统资源。
          fos.close();
      }
  }
  ```

**27.3字节流写数据的三种方式【应用】**

- 写数据的方法分类

  | 方法名                                   | 说明                                                         |
  | ---------------------------------------- | ------------------------------------------------------------ |
  | void   write(int b)                      | 将指定的字节写入此文件输出流   一次写一个字节数据            |
  | void   write(byte[] b)                   | 将 b.length字节从指定的字节数组写入此文件输出流   一次写一个字节数组数据 |
  | void   write(byte[] b, int off, int len) | 将 len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流   一次写一个字节数组的部分数据 |

- 示例代码

  ```java
  public class FileOutputStreamDemo02 {
      public static void main(String[] args) throws IOException {
          //FileOutputStream(String name)：创建文件输出流以指定的名称写入文件
          FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
          //new File(name)
  //        FileOutputStream fos = new FileOutputStream(new File("myByteStream\\fos.txt"));
  
          //FileOutputStream(File file)：创建文件输出流以写入由指定的 File对象表示的文件
  //        File file = new File("myByteStream\\fos.txt");
  //        FileOutputStream fos2 = new FileOutputStream(file);
  //        FileOutputStream fos2 = new FileOutputStream(new File("myByteStream\\fos.txt"));
  
          //void write(int b)：将指定的字节写入此文件输出流
  //        fos.write(97);
  //        fos.write(98);
  //        fos.write(99);
  //        fos.write(100);
  //        fos.write(101);
  
  //        void write(byte[] b)：将 b.length字节从指定的字节数组写入此文件输出流
  //        byte[] bys = {97, 98, 99, 100, 101};
          //byte[] getBytes()：返回字符串对应的字节数组
          byte[] bys = "abcde".getBytes();
  //        fos.write(bys);
  
          //void write(byte[] b, int off, int len)：将 len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流
  //        fos.write(bys,0,bys.length);
          fos.write(bys,1,3);
  
          //释放资源
          fos.close();
      }
  }
  ```

**27.4字节流写数据的两个小问题【应用】**

- 字节流写数据如何实现换行

  - windows:\r\n
  - linux:\n
  - mac:\r

- 字节流写数据如何实现追加写入

  - public FileOutputStream(String name,boolean append)
  - 创建文件输出流以指定的名称写入文件。如果第二个参数为true ，则字节将写入文件的末尾而不是开头

- 示例代码

  ```java
  public class FileOutputStreamDemo03 {
      public static void main(String[] args) throws IOException {
          //创建字节输出流对象
  //        FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
          FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt",true);
  
          //写数据
          for (int i = 0; i < 10; i++) {
              fos.write("hello".getBytes());
              fos.write("\r\n".getBytes());
          }
  
          //释放资源
          fos.close();
      }
  }
  ```

**27.5字节流写数据加异常处理【应用】**

- 异常处理格式

  - try-catch-finally

    ```java
    try{
    	可能出现异常的代码;
    }catch(异常类名 变量名){
    	异常的处理代码;
    }finally{
    	执行所有清除操作;
    }
    ```

  - finally特点

    - 被finally控制的语句一定会执行，除非JVM退出

- 示例代码

  ```java
  public class FileOutputStreamDemo04 {
      public static void main(String[] args) {
          //加入finally来实现释放资源
          FileOutputStream fos = null;
          try {
              fos = new FileOutputStream("myByteStream\\fos.txt");
              fos.write("hello".getBytes());
          } catch (IOException e) {
              e.printStackTrace();
          } finally {
              if(fos != null) {
                  try {
                      fos.close();
                  } catch (IOException e) {
                      e.printStackTrace();
                  }
              }
          }
      }
  }
  ```

**27.6字节流读数据(一次读一个字节数据)【应用】**

- 字节输入流

  - FileInputStream(String name)：通过打开与实际文件的连接来创建一个FileInputStream ，该文件由文件系统中的路径名name命名

- 字节输入流读取数据的步骤

  - 创建字节输入流对象
  - 调用字节输入流对象的读数据方法
  - 释放资源

- 示例代码

  ```java
  public class FileInputStreamDemo01 {
      public static void main(String[] args) throws IOException {
          //创建字节输入流对象
          //FileInputStream(String name)
          FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");
  
          int by;
          /*
              fis.read()：读数据
              by=fis.read()：把读取到的数据赋值给by
              by != -1：判断读取到的数据是否是-1
           */
          while ((by=fis.read())!=-1) {
              System.out.print((char)by);
          }
  
          //释放资源
          fis.close();
      }
  }
  ```

**27.7字节流复制文本文件【应用】**

- 案例需求

  ​	把“E:\\itcast\\窗里窗外.txt”复制到模块目录下的“窗里窗外.txt”

- 实现步骤

  - 复制文本文件，其实就把文本文件的内容从一个文件中读取出来(数据源)，然后写入到另一个文件中(目的地)

  - 数据源：

    ​	E:\\itcast\\窗里窗外.txt --- 读数据 --- InputStream --- FileInputStream 

  - 目的地：

    ​	myByteStream\\窗里窗外.txt --- 写数据 --- OutputStream --- FileOutputStream

- 代码实现

  ```java
  public class CopyTxtDemo {
      public static void main(String[] args) throws IOException {
          //根据数据源创建字节输入流对象
          FileInputStream fis = new FileInputStream("E:\\itcast\\窗里窗外.txt");
          //根据目的地创建字节输出流对象
          FileOutputStream fos = new FileOutputStream("myByteStream\\窗里窗外.txt");
  
          //读写数据，复制文本文件(一次读取一个字节，一次写入一个字节)
          int by;
          while ((by=fis.read())!=-1) {
              fos.write(by);
          }
  
          //释放资源
          fos.close();
          fis.close();
      }
  }
  ```

**27.8字节流读数据(一次读一个字节数组数据)【应用】**

- 一次读一个字节数组的方法

  - public int read(byte[] b)：从输入流读取最多b.length个字节的数据
  - 返回的是读入缓冲区的总字节数,也就是实际的读取字节个数

- 示例代码

  ```java
  public class FileInputStreamDemo02 {
      public static void main(String[] args) throws IOException {
          //创建字节输入流对象
          FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");
  
          /*
              hello\r\n
              world\r\n
  
              第一次：hello
              第二次：\r\nwor
              第三次：ld\r\nr
  
           */
  
          byte[] bys = new byte[1024]; //1024及其整数倍
          int len;
          while ((len=fis.read(bys))!=-1) {
              System.out.print(new String(bys,0,len));
          }
  
          //释放资源
          fis.close();
      }
  }
  ```

**27.9字节流复制图片【应用】**

- 案例需求

  ​	把“E:\\itcast\\mn.jpg”复制到模块目录下的“mn.jpg”

- 实现步骤

  - 根据数据源创建字节输入流对象
  - 根据目的地创建字节输出流对象
  - 读写数据，复制图片(一次读取一个字节数组，一次写入一个字节数组)
  - 释放资源

- 代码实现

  ```java
  public class CopyJpgDemo {
      public static void main(String[] args) throws IOException {
          //根据数据源创建字节输入流对象
          FileInputStream fis = new FileInputStream("E:\\itcast\\mn.jpg");
          //根据目的地创建字节输出流对象
          FileOutputStream fos = new FileOutputStream("myByteStream\\mn.jpg");
  
          //读写数据，复制图片(一次读取一个字节数组，一次写入一个字节数组)
          byte[] bys = new byte[1024];
          int len;
          while ((len=fis.read(bys))!=-1) {
              fos.write(bys,0,len);
          }
  
          //释放资源
          fos.close();
          fis.close();
      }
  }
  ```

### 27.10 字节缓冲流

**27.10.1字节缓冲流构造方法【应用】**

- 字节缓冲流介绍

  - lBufferOutputStream：该类实现缓冲输出流。 通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用

  - lBufferedInputStream：创建BufferedInputStream将创建一个内部缓冲区数组。 当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次很多字节

- 构造方法：

  | 方法名                                 | 说明                   |
  | -------------------------------------- | ---------------------- |
  | BufferedOutputStream(OutputStream out) | 创建字节缓冲输出流对象 |
  | BufferedInputStream(InputStream in)    | 创建字节缓冲输入流对象 |

- 示例代码

  ```java
  public class BufferStreamDemo {
      public static void main(String[] args) throws IOException {
          //字节缓冲输出流：BufferedOutputStream(OutputStream out)
   
          BufferedOutputStream bos = new BufferedOutputStream(new 				                                       FileOutputStream("myByteStream\\bos.txt"));
          //写数据
          bos.write("hello\r\n".getBytes());
          bos.write("world\r\n".getBytes());
          //释放资源
          bos.close();
      
  
          //字节缓冲输入流：BufferedInputStream(InputStream in)
          BufferedInputStream bis = new BufferedInputStream(new                                                          FileInputStream("myByteStream\\bos.txt"));
  
          //一次读取一个字节数据
  //        int by;
  //        while ((by=bis.read())!=-1) {
  //            System.out.print((char)by);
  //        }
  
          //一次读取一个字节数组数据
          byte[] bys = new byte[1024];
          int len;
          while ((len=bis.read(bys))!=-1) {
              System.out.print(new String(bys,0,len));
          }
  
          //释放资源
          bis.close();
      }
  }
  ```

**27.10.2字节流复制视频【应用】**

- 案例需求

  把“E:\\itcast\\字节流复制图片.avi”复制到模块目录下的“字节流复制图片.avi”

- 实现步骤

  - 根据数据源创建字节输入流对象

  - 根据目的地创建字节输出流对象
  - 读写数据，复制视频
  - 释放资源

- 代码实现

  ```java
  public class CopyAviDemo {
      public static void main(String[] args) throws IOException {
          //记录开始时间
          long startTime = System.currentTimeMillis();
  
          //复制视频
  //        method1();
  //        method2();
  //        method3();
          method4();
  
          //记录结束时间
          long endTime = System.currentTimeMillis();
          System.out.println("共耗时：" + (endTime - startTime) + "毫秒");
      }
  
      //字节缓冲流一次读写一个字节数组
      public static void method4() throws IOException {
          BufferedInputStream bis = new BufferedInputStream(new FileInputStream("E:\\itcast\\字节流复制图片.avi"));
          BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myByteStream\\字节流复制图片.avi"));
  
          byte[] bys = new byte[1024];
          int len;
          while ((len=bis.read(bys))!=-1) {
              bos.write(bys,0,len);
          }
  
          bos.close();
          bis.close();
      }
  
      //字节缓冲流一次读写一个字节
      public static void method3() throws IOException {
          BufferedInputStream bis = new BufferedInputStream(new FileInputStream("E:\\itcast\\字节流复制图片.avi"));
          BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myByteStream\\字节流复制图片.avi"));
  
          int by;
          while ((by=bis.read())!=-1) {
              bos.write(by);
          }
  
          bos.close();
          bis.close();
      }
  
  
      //基本字节流一次读写一个字节数组
      public static void method2() throws IOException {
          //E:\\itcast\\字节流复制图片.avi
          //模块目录下的 字节流复制图片.avi
          FileInputStream fis = new FileInputStream("E:\\itcast\\字节流复制图片.avi");
          FileOutputStream fos = new FileOutputStream("myByteStream\\字节流复制图片.avi");
  
          byte[] bys = new byte[1024];
          int len;
          while ((len=fis.read(bys))!=-1) {
              fos.write(bys,0,len);
          }
  
          fos.close();
          fis.close();
      }
  
      //基本字节流一次读写一个字节
      public static void method1() throws IOException {
          //E:\\itcast\\字节流复制图片.avi
          //模块目录下的 字节流复制图片.avi
          FileInputStream fis = new FileInputStream("E:\\itcast\\字节流复制图片.avi");
          FileOutputStream fos = new FileOutputStream("myByteStream\\字节流复制图片.avi");
  
          int by;
          while ((by=fis.read())!=-1) {
              fos.write(by);
          }
  
          fos.close();
          fis.close();
      }
  }
  ```

### 27.11 字符流

**27.11.1为什么会出现字符流【理解】**

- 字符流的介绍

  由于字节流操作中文不是特别的方便，所以Java就提供字符流

  字符流 = 字节流 + 编码表

- 中文的字节存储方式

  用字节流复制文本文件时，文本文件也会有中文，但是没有问题，原因是最终底层操作会自动进行字节拼接成中文，如何识别是中文的呢？

  汉字在存储的时候，无论选择哪种编码存储，第一个字节都是负数

**27.11.2编码表【理解】**

- 什么是字符集

  是一个系统支持的所有字符的集合，包括各国家文字、标点符号、图形符号、数字等

  l计算机要准确的存储和识别各种字符集符号，就需要进行字符编码，一套字符集必然至少有一套字符编码。常见字符集有ASCII字符集、GBXXX字符集、Unicode字符集等

- 常见的字符集

  - ASCII字符集：

    lASCII：是基于拉丁字母的一套电脑编码系统，用于显示现代英语，主要包括控制字符(回车键、退格、换行键等)和可显示字符(英文大小写字符、阿拉伯数字和西文符号) 

    基本的ASCII字符集，使用7位表示一个字符，共128字符。ASCII的扩展字符集使用8位表示一个字符，共256字符，方便支持欧洲常用字符。是一个系统支持的所有字符的集合，包括各国家文字、标点符号、图形符号、数字等

  - GBXXX字符集：

    GBK：最常用的中文码表。是在GB2312标准基础上的扩展规范，使用了双字节编码方案，共收录了21003个汉字，完全兼容GB2312标准，同时支持繁体汉字以及日韩汉字等

  - Unicode字符集：

    UTF-8编码：可以用来表示Unicode标准中任意字符，它是电子邮件、网页及其他存储或传送文字的应用 中，优先采用的编码。互联网工程工作小组（IETF）要求所有互联网协议都必须支持UTF-8编码。它使用一至四个字节为每个字符编码

    编码规则： 

      128个US-ASCII字符，只需一个字节编码

      拉丁文等字符，需要二个字节编码

      大部分常用字（含中文），使用三个字节编码

      其他极少使用的Unicode辅助字符，使用四字节编码

**27.11.3字符串中的编码解码问题【应用】**

- 相关方法

  | 方法名                                   | 说明                                               |
  | ---------------------------------------- | -------------------------------------------------- |
  | byte[] getBytes()                        | 使用平台的默认字符集将该 String编码为一系列字节    |
  | byte[] getBytes(String charsetName)      | 使用指定的字符集将该 String编码为一系列字节        |
  | String(byte[] bytes)                     | 使用平台的默认字符集解码指定的字节数组来创建字符串 |
  | String(byte[] bytes, String charsetName) | 通过指定的字符集解码指定的字节数组来创建字符串     |

- 代码演示

  ```java
  public class StringDemo {
      public static void main(String[] args) throws UnsupportedEncodingException {
          //定义一个字符串
          String s = "中国";
  
          //byte[] bys = s.getBytes(); //[-28, -72, -83, -27, -101, -67]
          //byte[] bys = s.getBytes("UTF-8"); //[-28, -72, -83, -27, -101, -67]
          byte[] bys = s.getBytes("GBK"); //[-42, -48, -71, -6]
          System.out.println(Arrays.toString(bys));
  
          //String ss = new String(bys);
          //String ss = new String(bys,"UTF-8");
          String ss = new String(bys,"GBK");
          System.out.println(ss);
      }
  }
  ```

**27.11.4字符流中的编码解码问题【应用】**

- 字符流中和编码解码问题相关的两个类

  - InputStreamReader：是从字节流到字符流的桥梁

    ​	它读取字节，并使用指定的编码将其解码为字符

    ​	它使用的字符集可以由名称指定，也可以被明确指定，或者可以接受平台的默认字符集

  - OutputStreamWriter：是从字符流到字节流的桥梁

    ​	是从字符流到字节流的桥梁，使用指定的编码将写入的字符编码为字节

    ​	它使用的字符集可以由名称指定，也可以被明确指定，或者可以接受平台的默认字符集

- 构造方法

  | 方法名                                              | 说明                                         |
  | --------------------------------------------------- | -------------------------------------------- |
  | InputStreamReader(InputStream in)                   | 使用默认字符编码创建InputStreamReader对象    |
  | InputStreamReader(InputStream in,String chatset)    | 使用指定的字符编码创建InputStreamReader对象  |
  | OutputStreamWriter(OutputStream out)                | 使用默认字符编码创建OutputStreamWriter对象   |
  | OutputStreamWriter(OutputStream out,String charset) | 使用指定的字符编码创建OutputStreamWriter对象 |

- 代码演示

  ```java
  public class ConversionStreamDemo {
      public static void main(String[] args) throws IOException {
          //OutputStreamWriter osw = new OutputStreamWriter(new                                             FileOutputStream("myCharStream\\osw.txt"));
          OutputStreamWriter osw = new OutputStreamWriter(new                                              FileOutputStream("myCharStream\\osw.txt"),"GBK");
          osw.write("中国");
          osw.close();
  
          //InputStreamReader isr = new InputStreamReader(new 	                                         FileInputStream("myCharStream\\osw.txt"));
          InputStreamReader isr = new InputStreamReader(new                                                 FileInputStream("myCharStream\\osw.txt"),"GBK");
          //一次读取一个字符数据
          int ch;
          while ((ch=isr.read())!=-1) {
              System.out.print((char)ch);
          }
          isr.close();
      }
  }
  ```

**27.11.5字符流写数据的5种方式【应用】**

- 方法介绍

  | 方法名                                    | 说明                 |
  | ----------------------------------------- | -------------------- |
  | void   write(int c)                       | 写一个字符           |
  | void   write(char[] cbuf)                 | 写入一个字符数组     |
  | void write(char[] cbuf, int off, int len) | 写入字符数组的一部分 |
  | void write(String str)                    | 写一个字符串         |
  | void write(String str, int off, int len)  | 写一个字符串的一部分 |

- 刷新和关闭的方法

  | 方法名  | 说明                                                         |
  | ------- | ------------------------------------------------------------ |
  | flush() | 刷新流，之后还可以继续写数据                                 |
  | close() | 关闭流，释放资源，但是在关闭之前会先刷新流。一旦关闭，就不能再写数据 |

- 代码演示

  ```java
  public class OutputStreamWriterDemo {
      public static void main(String[] args) throws IOException {
          OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("myCharStream\\osw.txt"));
  
          //void write(int c)：写一个字符
  //        osw.write(97);
  //        osw.write(98);
  //        osw.write(99);
  
          //void writ(char[] cbuf)：写入一个字符数组
          char[] chs = {'a', 'b', 'c', 'd', 'e'};
  //        osw.write(chs);
  
          //void write(char[] cbuf, int off, int len)：写入字符数组的一部分
  //        osw.write(chs, 0, chs.length);
  //        osw.write(chs, 1, 3);
  
          //void write(String str)：写一个字符串
  //        osw.write("abcde");
  
          //void write(String str, int off, int len)：写一个字符串的一部分
  //        osw.write("abcde", 0, "abcde".length());
          osw.write("abcde", 1, 3);
  
          //释放资源
          osw.close();
      }
  }
  ```

**27.11.6字符流读数据的2种方式【应用】**

- 方法介绍

  | 方法名                | 说明                   |
  | --------------------- | ---------------------- |
  | int read()            | 一次读一个字符数据     |
  | int read(char[] cbuf) | 一次读一个字符数组数据 |

- 代码演示

  ```java
  public class InputStreamReaderDemo {
      public static void main(String[] args) throws IOException {
     
          InputStreamReader isr = new InputStreamReader(new FileInputStream("myCharStream\\ConversionStreamDemo.java"));
  
          //int read()：一次读一个字符数据
  //        int ch;
  //        while ((ch=isr.read())!=-1) {
  //            System.out.print((char)ch);
  //        }
  
          //int read(char[] cbuf)：一次读一个字符数组数据
          char[] chs = new char[1024];
          int len;
          while ((len = isr.read(chs)) != -1) {
              System.out.print(new String(chs, 0, len));
          }
  
          //释放资源
          isr.close();
      }
  }
  ```

**27.11.7字符流复制Java文件【应用】**

- 案例需求

  把模块目录下的“ConversionStreamDemo.java” 复制到模块目录下的“Copy.java”

- 实现步骤

  - 根据数据源创建字符输入流对象
  - 根据目的地创建字符输出流对象
  - 读写数据，复制文件
  - 释放资源

- 代码实现

  ```java
  public class CopyJavaDemo01 {
      public static void main(String[] args) throws IOException {
          //根据数据源创建字符输入流对象
          InputStreamReader isr = new InputStreamReader(new FileInputStream("myCharStream\\ConversionStreamDemo.java"));
          //根据目的地创建字符输出流对象
          OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("myCharStream\\Copy.java"));
  
          //读写数据，复制文件
          //一次读写一个字符数据
  //        int ch;
  //        while ((ch=isr.read())!=-1) {
  //            osw.write(ch);
  //        }
  
          //一次读写一个字符数组数据
          char[] chs = new char[1024];
          int len;
          while ((len=isr.read(chs))!=-1) {
              osw.write(chs,0,len);
          }
  
          //释放资源
          osw.close();
          isr.close();
      }
  }
  ```

**27.11.8字符流复制Java文件改进版【应用】**

- 案例需求

  使用便捷流对象，把模块目录下的“ConversionStreamDemo.java” 复制到模块目录下的“Copy.java”

- 实现步骤

  - 根据数据源创建字符输入流对象

  - 根据目的地创建字符输出流对象
  - 读写数据，复制文件
  - 释放资源

- 代码实现

  ```java
  public class CopyJavaDemo02 {
      public static void main(String[] args) throws IOException {
          //根据数据源创建字符输入流对象
          FileReader fr = new FileReader("myCharStream\\ConversionStreamDemo.java");
          //根据目的地创建字符输出流对象
          FileWriter fw = new FileWriter("myCharStream\\Copy.java");
  
          //读写数据，复制文件
  //        int ch;
  //        while ((ch=fr.read())!=-1) {
  //            fw.write(ch);
  //        }
  
          char[] chs = new char[1024];
          int len;
          while ((len=fr.read(chs))!=-1) {
              fw.write(chs,0,len);
          }
  
          //释放资源
          fw.close();
          fr.close();
      }
  }
  ```

**27.11.9字符缓冲流【应用】**

- 字符缓冲流介绍

  - BufferedWriter：将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入，可以指定缓冲区大小，或者可以接受默认大小。默认值足够大，可用于大多数用途

  - BufferedReader：从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取，可以指定缓冲区大小，或者可以使用默认大小。 默认值足够大，可用于大多数用途

- 构造方法

  | 方法名                     | 说明                   |
  | -------------------------- | ---------------------- |
  | BufferedWriter(Writer out) | 创建字符缓冲输出流对象 |
  | BufferedReader(Reader in)  | 创建字符缓冲输入流对象 |

- 代码演示

  ```java
  public class BufferedStreamDemo01 {
      public static void main(String[] args) throws IOException {
          //BufferedWriter(Writer out)
          BufferedWriter bw = new BufferedWriter(new                                                            FileWriter("myCharStream\\bw.txt"));
          bw.write("hello\r\n");
          bw.write("world\r\n");
          bw.close();
  
          //BufferedReader(Reader in)
          BufferedReader br = new BufferedReader(new                                                           FileReader("myCharStream\\bw.txt"));
  
          //一次读取一个字符数据
  //        int ch;
  //        while ((ch=br.read())!=-1) {
  //            System.out.print((char)ch);
  //        }
  
          //一次读取一个字符数组数据
          char[] chs = new char[1024];
          int len;
          while ((len=br.read(chs))!=-1) {
              System.out.print(new String(chs,0,len));
          }
  
          br.close();
      }
  }
  ```

**27.11.10字符缓冲流复制Java文件【应用】**

- 案例需求

  把模块目录下的ConversionStreamDemo.java 复制到模块目录下的 Copy.java

- 实现步骤

  - 根据数据源创建字符缓冲输入流对象
  - 根据目的地创建字符缓冲输出流对象
  - 读写数据，复制文件，使用字符缓冲流特有功能实现
  - 释放资源

- 代码实现

  ```java
  public class CopyJavaDemo01 {
      public static void main(String[] args) throws IOException {
          //根据数据源创建字符缓冲输入流对象
          BufferedReader br = new BufferedReader(new FileReader("myCharStream\\ConversionStreamDemo.java"));
          //根据目的地创建字符缓冲输出流对象
          BufferedWriter bw = new BufferedWriter(new FileWriter("myCharStream\\Copy.java"));
  
          //读写数据，复制文件
          //一次读写一个字符数据
  //        int ch;
  //        while ((ch=br.read())!=-1) {
  //            bw.write(ch);
  //        }
  
          //一次读写一个字符数组数据
          char[] chs = new char[1024];
          int len;
          while ((len=br.read(chs))!=-1) {
              bw.write(chs,0,len);
          }
  
          //释放资源
          bw.close();
          br.close();
      }
  }
  ```

**27.11.11字符缓冲流特有功能【应用】**

- 方法介绍

  BufferedWriter：

  | 方法名         | 说明                                         |
  | -------------- | -------------------------------------------- |
  | void newLine() | 写一行行分隔符，行分隔符字符串由系统属性定义 |

  BufferedReader:

  | 方法名            | 说明                                                         |
  | ----------------- | ------------------------------------------------------------ |
  | String readLine() | 读一行文字。 结果包含行的内容的字符串，不包括任何行终止字符如果流的结尾已经到达，则为null |

- 代码演示

  ```java
  public class BufferedStreamDemo02 {
      public static void main(String[] args) throws IOException {
  
          //创建字符缓冲输出流
          BufferedWriter bw = new BufferedWriter(new                                                          FileWriter("myCharStream\\bw.txt"));
  
          //写数据
          for (int i = 0; i < 10; i++) {
              bw.write("hello" + i);
              //bw.write("\r\n");
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          bw.close();
  
          //创建字符缓冲输入流
          BufferedReader br = new BufferedReader(new                                                          FileReader("myCharStream\\bw.txt"));
  
          String line;
          while ((line=br.readLine())!=null) {
              System.out.println(line);
          }
  
          br.close();
      }
  }
  ```

**27.11.12字符缓冲流特有功能复制Java文件【应用】**

- 案例需求

  使用特有功能把模块目录下的ConversionStreamDemo.java 复制到模块目录下的 Copy.java

- 实现步骤

  - 根据数据源创建字符缓冲输入流对象
  - 根据目的地创建字符缓冲输出流对象
  - 读写数据，复制文件，使用字符缓冲流特有功能实现
  - 释放资源

- 代码实现

  ```java
  public class CopyJavaDemo02 {
      public static void main(String[] args) throws IOException {
          //根据数据源创建字符缓冲输入流对象
          BufferedReader br = new BufferedReader(new FileReader("myCharStream\\ConversionStreamDemo.java"));
          //根据目的地创建字符缓冲输出流对象
          BufferedWriter bw = new BufferedWriter(new FileWriter("myCharStream\\Copy.java"));
  
          //读写数据，复制文件
          //使用字符缓冲流特有功能实现
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          bw.close();
          br.close();
      }
  }
  ```

**27.11.13IO流小结【理解】**

- 字节流

  ![IO小结字节流](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/IO%E5%B0%8F%E7%BB%93%E5%AD%97%E8%8A%82%E6%B5%81-1677566604429.jpg)

- 字符流

  ![IO小结字符流](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/IO%E5%B0%8F%E7%BB%93%E5%AD%97%E7%AC%A6%E6%B5%81.jpg)

**27.12 IO特殊操作流**

**27.12.1标准输入流【应用】**

- System类中有两个静态的成员变量

  - public static final InputStream in：标准输入流。通常该流对应于键盘输入或由主机环境或用户指定的另一个输入源
  - public static final PrintStream out：标准输出流。通常该流对应于显示输出或由主机环境或用户指定的另一个输出目标

- 自己实现键盘录入数据

  ```java
  public class SystemInDemo {
      public static void main(String[] args) throws IOException {
          //public static final InputStream in：标准输入流
  //        InputStream is = System.in;
  
  //        int by;
  //        while ((by=is.read())!=-1) {
  //            System.out.print((char)by);
  //        }
  
          //如何把字节流转换为字符流？用转换流
  //        InputStreamReader isr = new InputStreamReader(is);
  //        //使用字符流能不能够实现一次读取一行数据呢？可以
  //        //但是，一次读取一行数据的方法是字符缓冲输入流的特有方法
  //        BufferedReader br = new BufferedReader(isr);
  
          BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  
          System.out.println("请输入一个字符串：");
          String line = br.readLine();
          System.out.println("你输入的字符串是：" + line);
  
          System.out.println("请输入一个整数：");
          int i = Integer.parseInt(br.readLine());
          System.out.println("你输入的整数是：" + i);
  
          //自己实现键盘录入数据太麻烦了，所以Java就提供了一个类供我们使用
          Scanner sc = new Scanner(System.in);
      }
  }
  ```

**27.12.2标准输出流【应用】**

- System类中有两个静态的成员变量

  - public static final InputStream in：标准输入流。通常该流对应于键盘输入或由主机环境或用户指定的另一个输入源
  - public static final PrintStream out：标准输出流。通常该流对应于显示输出或由主机环境或用户指定的另一个输出目标

- 输出语句的本质：是一个标准的输出流

  - PrintStream ps = System.out;
  - PrintStream类有的方法，System.out都可以使用

- 示例代码

  ```java
  public class SystemOutDemo {
      public static void main(String[] args) {
          //public static final PrintStream out：标准输出流
          PrintStream ps = System.out;
  
          //能够方便地打印各种数据值
  //        ps.print("hello");
  //        ps.print(100);
  
  //        ps.println("hello");
  //        ps.println(100);
  
          //System.out的本质是一个字节输出流
          System.out.println("hello");
          System.out.println(100);
  
          System.out.println();
  //        System.out.print();
      }
  }
  ```

**27.12.3字节打印流【应用】**

- 打印流分类

  - 字节打印流：PrintStream
  - 字符打印流：PrintWriter

- 打印流的特点

  - 只负责输出数据，不负责读取数据
  - 永远不会抛出IOException
  - 有自己的特有方法

- 字节打印流

  - PrintStream(String fileName)：使用指定的文件名创建新的打印流

  - 使用继承父类的方法写数据，查看的时候会转码；使用自己的特有方法写数据，查看的数据原样输出

  - 可以改变输出语句的目的地

    ​	public static void setOut(PrintStream out)：重新分配“标准”输出流

- 示例代码

  ```java
  public class PrintStreamDemo {
      public static void main(String[] args) throws IOException {
          //PrintStream(String fileName)：使用指定的文件名创建新的打印流
          PrintStream ps = new PrintStream("myOtherStream\\ps.txt");
  
          //写数据
          //字节输出流有的方法
  //        ps.write(97);
  
          //使用特有方法写数据
  //        ps.print(97);
  //        ps.println();
  //        ps.print(98);
          ps.println(97);
          ps.println(98);
          
          //释放资源
          ps.close();
      }
  }
  ```

**27.12.4字符打印流【应用】**

- 字符打印流构造房方法

  | 方法名                                       | 说明                                                         |
  | -------------------------------------------- | ------------------------------------------------------------ |
  | PrintWriter(String   fileName)               | 使用指定的文件名创建一个新的PrintWriter，而不需要自动执行刷新 |
  | PrintWriter(Writer   out, boolean autoFlush) | 创建一个新的PrintWriter    out：字符输出流    autoFlush： 一个布尔值，如果为真，则println ， printf ，或format方法将刷新输出缓冲区 |

- 示例代码

  ```java
  public class PrintWriterDemo {
      public static void main(String[] args) throws IOException {
          //PrintWriter(String fileName) ：使用指定的文件名创建一个新的PrintWriter，而不需要自动执行行刷新
  //        PrintWriter pw = new PrintWriter("myOtherStream\\pw.txt");
  
  //        pw.write("hello");
  //        pw.write("\r\n");
  //        pw.flush();
  //        pw.write("world");
  //        pw.write("\r\n");
  //        pw.flush();
  
  //        pw.println("hello");
          /*
              pw.write("hello");
              pw.write("\r\n");
           */
  //        pw.flush();
  //        pw.println("world");
  //        pw.flush();
  
          //PrintWriter(Writer out, boolean autoFlush)：创建一个新的PrintWriter
          PrintWriter pw = new PrintWriter(new FileWriter("myOtherStream\\pw.txt"),true);
  //        PrintWriter pw = new PrintWriter(new FileWriter("myOtherStream\\pw.txt"),false);
  
          pw.println("hello");
          /*
              pw.write("hello");
              pw.write("\r\n");
              pw.flush();
           */
          pw.println("world");
  
          pw.close();
      }
  }
  ```

**27.12.5复制Java文件打印流改进版【应用】**

- 案例需求

  - 把模块目录下的PrintStreamDemo.java 复制到模块目录下的 Copy.java

- 分析步骤

  - 根据数据源创建字符输入流对象
  - 根据目的地创建字符输出流对象
  - 读写数据，复制文件
  - 释放资源

- 代码实现

  ```java
  public class CopyJavaDemo {
      public static void main(String[] args) throws IOException {
          /*
          //根据数据源创建字符输入流对象
          BufferedReader br = new BufferedReader(new FileReader("myOtherStream\\PrintStreamDemo.java"));
          //根据目的地创建字符输出流对象
          BufferedWriter bw = new BufferedWriter(new FileWriter("myOtherStream\\Copy.java"));
  
          //读写数据，复制文件
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          bw.close();
          br.close();
          */
  
          //根据数据源创建字符输入流对象
          BufferedReader br = new BufferedReader(new FileReader("myOtherStream\\PrintStreamDemo.java"));
          //根据目的地创建字符输出流对象
          PrintWriter pw = new PrintWriter(new FileWriter("myOtherStream\\Copy.java"),true);
  
          //读写数据，复制文件
          String line;
          while ((line=br.readLine())!=null) {
              pw.println(line);
          }
  
          //释放资源
          pw.close();
          br.close();
      }
  }
  ```

**27.12.6对象序列化流【应用】**

- 对象序列化介绍

  - 对象序列化：就是将对象保存到磁盘中，或者在网络中传输对象
  - 这种机制就是使用一个字节序列表示一个对象，该字节序列包含：对象的类型、对象的数据和对象中存储的属性等信息
  - 字节序列写到文件之后，相当于文件中持久保存了一个对象的信息
  - 反之，该字节序列还可以从文件中读取回来，重构对象，对它进行反序列化

- 对象序列化流： ObjectOutputStream

  - 将Java对象的原始数据类型和图形写入OutputStream。 可以使用ObjectInputStream读取（重构）对象。 可以通过使用流的文件来实现对象的持久存储。 如果流是网络套接字流，则可以在另一个主机上或另一个进程中重构对象 

- 构造方法

  | 方法名                               | 说明                                               |
  | ------------------------------------ | -------------------------------------------------- |
  | ObjectOutputStream(OutputStream out) | 创建一个写入指定的OutputStream的ObjectOutputStream |

- 序列化对象的方法

  | 方法名                       | 说明                               |
  | ---------------------------- | ---------------------------------- |
  | void writeObject(Object obj) | 将指定的对象写入ObjectOutputStream |

- 示例代码

  - 学生类

    ```java
    public class Student implements Serializable {
        private String name;
        private int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
        @Override
        public String toString() {
            return "Student{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    '}';
        }
    }
    ```

  - 测试类

    ```java
    public class ObjectOutputStreamDemo {
        public static void main(String[] args) throws IOException {
            //ObjectOutputStream(OutputStream out)：创建一个写入指定的OutputStream的ObjectOutputStream
            ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("myOtherStream\\oos.txt"));
    
            //创建对象
            Student s = new Student("林青霞",30);
    
            //void writeObject(Object obj)：将指定的对象写入ObjectOutputStream
            oos.writeObject(s);
    
            //释放资源
            oos.close();
        }
    }
    ```

- 注意事项

  - 一个对象要想被序列化，该对象所属的类必须必须实现Serializable 接口
  - Serializable是一个标记接口，实现该接口，不需要重写任何方法

**27.12.7对象反序列化流【应用】**

- 对象反序列化流： ObjectInputStream

  - ObjectInputStream反序列化先前使用ObjectOutputStream编写的原始数据和对象

- 构造方法

  | 方法名                            | 说明                                           |
  | --------------------------------- | ---------------------------------------------- |
  | ObjectInputStream(InputStream in) | 创建从指定的InputStream读取的ObjectInputStream |

- 反序列化对象的方法

  | 方法名              | 说明                            |
  | ------------------- | ------------------------------- |
  | Object readObject() | 从ObjectInputStream读取一个对象 |

- 示例代码

  ```java
  public class ObjectInputStreamDemo {
      public static void main(String[] args) throws IOException, ClassNotFoundException {
          //ObjectInputStream(InputStream in)：创建从指定的InputStream读取的ObjectInputStream
          ObjectInputStream ois = new ObjectInputStream(new FileInputStream("myOtherStream\\oos.txt"));
  
          //Object readObject()：从ObjectInputStream读取一个对象
          Object obj = ois.readObject();
  
          Student s = (Student) obj;
          System.out.println(s.getName() + "," + s.getAge());
  
          ois.close();
      }
  }
  ```

**27.12.8serialVersionUID&transient【应用】**

- serialVersionUID

  - 用对象序列化流序列化了一个对象后，假如我们修改了对象所属的类文件，读取数据会不会出问题呢？
    - 会出问题，会抛出InvalidClassException异常
  - 如果出问题了，如何解决呢？
    - 重新序列化
    - 给对象所属的类加一个serialVersionUID 
      - private static final long serialVersionUID = 42L;

- transient

  - 如果一个对象中的某个成员变量的值不想被序列化，又该如何实现呢？
    - 给该成员变量加transient关键字修饰，该关键字标记的成员变量不参与序列化过程

- 示例代码

  - 学生类

    ```java
    public class Student implements Serializable {
        private static final long serialVersionUID = 42L;
        private String name;
    //    private int age;
        private transient int age;
    
        public Student() {
        }
    
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
    //    @Override
    //    public String toString() {
    //        return "Student{" +
    //                "name='" + name + '\'' +
    //                ", age=" + age +
    //                '}';
    //    }
    }
    ```

  - 测试类

    ```java
    public class ObjectStreamDemo {
        public static void main(String[] args) throws IOException, ClassNotFoundException {
    //        write();
            read();
        }
    
        //反序列化
        private static void read() throws IOException, ClassNotFoundException {
            ObjectInputStream ois = new ObjectInputStream(new FileInputStream("myOtherStream\\oos.txt"));
            Object obj = ois.readObject();
            Student s = (Student) obj;
            System.out.println(s.getName() + "," + s.getAge());
            ois.close();
        }
    
        //序列化
        private static void write() throws IOException {
            ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("myOtherStream\\oos.txt"));
            Student s = new Student("林青霞", 30);
            oos.writeObject(s);
            oos.close();
        }
    }
    ```

## 28 Properties集合

**28.1Properties作为Map集合的使用【应用】**

- Properties介绍

  - 是一个Map体系的集合类
  - Properties可以保存到流中或从流中加载
  - 属性列表中的每个键及其对应的值都是一个字符串

- Properties基本使用

  ```java
  public class PropertiesDemo01 {
      public static void main(String[] args) {
          //创建集合对象
  //        Properties<String,String> prop = new Properties<String,String>(); //错误
          Properties prop = new Properties();
  
          //存储元素
          prop.put("itheima001", "林青霞");
          prop.put("itheima002", "张曼玉");
          prop.put("itheima003", "王祖贤");
  
          //遍历集合
          Set<Object> keySet = prop.keySet();
          for (Object key : keySet) {
              Object value = prop.get(key);
              System.out.println(key + "," + value);
          }
      }
  }
  ```

**28.2Properties作为Map集合的特有方法【应用】**

- 特有方法

  | 方法名                                         | 说明                                                         |
  | ---------------------------------------------- | ------------------------------------------------------------ |
  | Object   setProperty(String key, String value) | 设置集合的键和值，都是String类型，底层调用   Hashtable方法 put |
  | String   getProperty(String key)               | 使用此属性列表中指定的键搜索属性                             |
  | Set<String>   stringPropertyNames()            | 从该属性列表中返回一个不可修改的键集，其中键及其对应的值是字符串 |

- 示例代码

  ```java
  public class PropertiesDemo02 {
      public static void main(String[] args) {
          //创建集合对象
          Properties prop = new Properties();
  
          //Object setProperty(String key, String value)：设置集合的键和值，都是String类型，底层调用Hashtable方法put
          prop.setProperty("itheima001", "林青霞");
          /*
              Object setProperty(String key, String value) {
                  return put(key, value);
              }
  
              Object put(Object key, Object value) {
                  return map.put(key, value);
              }
           */
          prop.setProperty("itheima002", "张曼玉");
          prop.setProperty("itheima003", "王祖贤");
  
          //String getProperty(String key)：使用此属性列表中指定的键搜索属性
  //        System.out.println(prop.getProperty("itheima001"));
  //        System.out.println(prop.getProperty("itheima0011"));
  
  //        System.out.println(prop);
  
          //Set<String> stringPropertyNames()：从该属性列表中返回一个不可修改的键集，其中键及其对应的值是字符串
          Set<String> names = prop.stringPropertyNames();
          for (String key : names) {
  //            System.out.println(key);
              String value = prop.getProperty(key);
              System.out.println(key + "," + value);
          }
      }
  }
  ```

**28.3Properties和IO流相结合的方法【应用】**

- 和IO流结合的方法

  | 方法名                                          | 说明                                                         |
  | ----------------------------------------------- | ------------------------------------------------------------ |
  | void   load(InputStream inStream)               | 从输入字节流读取属性列表（键和元素对）                       |
  | void   load(Reader reader)                      | 从输入字符流读取属性列表（键和元素对）                       |
  | void   store(OutputStream out, String comments) | 将此属性列表（键和元素对）写入此   Properties表中，以适合于使用   load(InputStream)方法的格式写入输出字节流 |
  | void   store(Writer writer, String comments)    | 将此属性列表（键和元素对）写入此   Properties表中，以适合使用   load(Reader)方法的格式写入输出字符流 |

- 示例代码

  ```java
  public class PropertiesDemo03 {
      public static void main(String[] args) throws IOException {
          //把集合中的数据保存到文件
  //        myStore();
  
          //把文件中的数据加载到集合
          myLoad();
  
      }
  
      private static void myLoad() throws IOException {
          Properties prop = new Properties();
  
          //void load(Reader reader)：
          FileReader fr = new FileReader("myOtherStream\\fw.txt");
          prop.load(fr);
          fr.close();
  
          System.out.println(prop);
      }
  
      private static void myStore() throws IOException {
          Properties prop = new Properties();
  
          prop.setProperty("itheima001","林青霞");
          prop.setProperty("itheima002","张曼玉");
          prop.setProperty("itheima003","王祖贤");
  
          //void store(Writer writer, String comments)：
          FileWriter fw = new FileWriter("myOtherStream\\fw.txt");
          prop.store(fw,null);
          fw.close();
      }
  }
  ```

**28.4游戏次数案例【应用】**

- 案例需求

  - 实现猜数字小游戏只能试玩3次，如果还想玩，提示：游戏试玩已结束，想玩请充值(www.itcast.cn)

- 分析步骤

  1. 写一个游戏类，里面有一个猜数字的小游戏

  2. 写一个测试类，测试类中有main()方法，main()方法中写如下代码：

     ​	从文件中读取数据到Properties集合，用load()方法实现

       		文件已经存在：game.txt

       		里面有一个数据值：count=0

     ​	通过Properties集合获取到玩游戏的次数

     ​	判断次数是否到到3次了

       		如果到了，给出提示：游戏试玩已结束，想玩请充值(www.itcast.cn)

       		如果不到3次：

       			次数+1，重新写回文件，用Properties的store()方法实现玩游戏

- 代码实现

  ```java
  public class PropertiesTest {
      public static void main(String[] args) throws IOException {
          //从文件中读取数据到Properties集合，用load()方法实现
          Properties prop = new Properties();
  
          FileReader fr = new FileReader("myOtherStream\\game.txt");
          prop.load(fr);
          fr.close();
  
          //通过Properties集合获取到玩游戏的次数
          String count = prop.getProperty("count");
          int number = Integer.parseInt(count);
  
          //判断次数是否到到3次了
          if(number >= 3) {
              //如果到了，给出提示：游戏试玩已结束，想玩请充值(www.itcast.cn)
              System.out.println("游戏试玩已结束，想玩请充值(www.itcast.cn)");
          } else {
              //玩游戏
              GuessNumber.start();
  
              //次数+1，重新写回文件，用Properties的store()方法实现
              number++;
              prop.setProperty("count",String.valueOf(number));
              FileWriter fw = new FileWriter("myOtherStream\\game.txt");
              prop.store(fw,null);
              fw.close();
          }
      }
  }
  ```

## 29 多线程

**29.1 实现多线程**

**29.1.1进程和线程【理解】**

- 进程：是正在运行的程序

  ​	是系统进行资源分配和调用的独立单位

  ​	每一个进程都有它自己的内存空间和系统资源

- 线程：是进程中的单个顺序控制流，是一条执行路径

  ​	单线程：一个进程如果只有一条执行路径，则称为单线程程序

  ​	多线程：一个进程如果有多条执行路径，则称为多线程程序

**29.1.2实现多线程方式一：继承Thread类【应用】**

- 方法介绍

  | 方法名       | 说明                                        |
  | ------------ | ------------------------------------------- |
  | void run()   | 在线程开启后，此方法将被调用执行            |
  | void start() | 使此线程开始执行，Java虚拟机会调用run方法() |

- 实现步骤

  - 定义一个类MyThread继承Thread类
  - 在MyThread类中重写run()方法
  - 创建MyThread类的对象
  - 启动线程

- 代码演示

  ```java
  public class MyThread extends Thread {
      @Override
      public void run() {
          for(int i=0; i<100; i++) {
              System.out.println(i);
          }
      }
  }
  public class MyThreadDemo {
      public static void main(String[] args) {
          MyThread my1 = new MyThread();
          MyThread my2 = new MyThread();
  
  //        my1.run();
  //        my2.run();
  
          //void start() 导致此线程开始执行; Java虚拟机调用此线程的run方法
          my1.start();
          my2.start();
      }
  }
  ```

- 两个小问题

  - 为什么要重写run()方法？

    因为run()是用来封装被线程执行的代码

  - run()方法和start()方法的区别？

    run()：封装线程执行的代码，直接调用，相当于普通方法的调用

    start()：启动线程；然后由JVM调用此线程的run()方法

**29.1.3设置和获取线程名称【应用】**

- 方法介绍

  | 方法名                     | 说明                               |
  | -------------------------- | ---------------------------------- |
  | void  setName(String name) | 将此线程的名称更改为等于参数name   |
  | String  getName()          | 返回此线程的名称                   |
  | Thread  currentThread()    | 返回对当前正在执行的线程对象的引用 |

- 代码演示

  ```java
  public class MyThread extends Thread {
      public MyThread() {}
      public MyThread(String name) {
          super(name);
      }
  
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
              System.out.println(getName()+":"+i);
          }
      }
  }
  public class MyThreadDemo {
      public static void main(String[] args) {
          MyThread my1 = new MyThread();
          MyThread my2 = new MyThread();
  
          //void setName(String name)：将此线程的名称更改为等于参数 name
          my1.setName("高铁");
          my2.setName("飞机");
  
          //Thread(String name)
          MyThread my1 = new MyThread("高铁");
          MyThread my2 = new MyThread("飞机");
  
          my1.start();
          my2.start();
  
          //static Thread currentThread() 返回对当前正在执行的线程对象的引用
          System.out.println(Thread.currentThread().getName());
      }
  }
  ```

**29.1.4线程优先级【应用】**

- 线程调度

  - 两种调度方式

    - 分时调度模型：所有线程轮流使用 CPU 的使用权，平均分配每个线程占用 CPU 的时间片
    - 抢占式调度模型：优先让优先级高的线程使用 CPU，如果线程的优先级相同，那么会随机选择一个，优先级高的线程获取的 CPU 时间片相对多一些

  - Java使用的是抢占式调度模型

  - 随机性

    假如计算机只有一个 CPU，那么 CPU 在某一个时刻只能执行一条指令，线程只有得到CPU时间片，也就是使用权，才可以执行指令。所以说多线程程序的执行是有随机性，因为谁抢到CPU的使用权是不一定的

- 优先级相关方法

  | 方法名                                  | 说明                                                         |
  | --------------------------------------- | ------------------------------------------------------------ |
  | final int getPriority()                 | 返回此线程的优先级                                           |
  | final void setPriority(int newPriority) | 更改此线程的优先级                                                                                         线程默认优先级是5；线程优先级的范围是：1-10 |

- 代码演示

  ```java
  public class ThreadPriority extends Thread {
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
              System.out.println(getName() + ":" + i);
          }
      }
  }
  public class ThreadPriorityDemo {
      public static void main(String[] args) {
          ThreadPriority tp1 = new ThreadPriority();
          ThreadPriority tp2 = new ThreadPriority();
          ThreadPriority tp3 = new ThreadPriority();
  
          tp1.setName("高铁");
          tp2.setName("飞机");
          tp3.setName("汽车");
  
          //public final int getPriority()：返回此线程的优先级
          System.out.println(tp1.getPriority()); //5
          System.out.println(tp2.getPriority()); //5
          System.out.println(tp3.getPriority()); //5
  
          //public final void setPriority(int newPriority)：更改此线程的优先级
  //        tp1.setPriority(10000); //IllegalArgumentException
          System.out.println(Thread.MAX_PRIORITY); //10
          System.out.println(Thread.MIN_PRIORITY); //1
          System.out.println(Thread.NORM_PRIORITY); //5
  
          //设置正确的优先级
          tp1.setPriority(5);
          tp2.setPriority(10);
          tp3.setPriority(1);
  
          tp1.start();
          tp2.start();
          tp3.start();
      }
  }
  ```

**29.1.5线程控制【应用】**

- 相关方法

  | 方法名                         | 说明                                                         |
  | ------------------------------ | ------------------------------------------------------------ |
  | static void sleep(long millis) | 使当前正在执行的线程停留（暂停执行）指定的毫秒数             |
  | void join()                    | 等待这个线程死亡                                             |
  | void setDaemon(boolean on)     | 将此线程标记为守护线程，当运行的线程都是守护线程时，Java虚拟机将退出 |

- 代码演示

  ```java
  sleep演示：
  public class ThreadSleep extends Thread {
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
              System.out.println(getName() + ":" + i);
              try {
                  Thread.sleep(1000);
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
          }
      }
  }
  public class ThreadSleepDemo {
      public static void main(String[] args) {
          ThreadSleep ts1 = new ThreadSleep();
          ThreadSleep ts2 = new ThreadSleep();
          ThreadSleep ts3 = new ThreadSleep();
  
          ts1.setName("曹操");
          ts2.setName("刘备");
          ts3.setName("孙权");
  
          ts1.start();
          ts2.start();
          ts3.start();
      }
  }
  
  Join演示：
  public class ThreadJoin extends Thread {
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
              System.out.println(getName() + ":" + i);
          }
      }
  }
  public class ThreadJoinDemo {
      public static void main(String[] args) {
          ThreadJoin tj1 = new ThreadJoin();
          ThreadJoin tj2 = new ThreadJoin();
          ThreadJoin tj3 = new ThreadJoin();
  
          tj1.setName("康熙");
          tj2.setName("四阿哥");
          tj3.setName("八阿哥");
  
          tj1.start();
          try {
              tj1.join();
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
          tj2.start();
          tj3.start();
      }
  }
  
  Daemon演示：
  public class ThreadDaemon extends Thread {
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
              System.out.println(getName() + ":" + i);
          }
      }
  }
  public class ThreadDaemonDemo {
      public static void main(String[] args) {
          ThreadDaemon td1 = new ThreadDaemon();
          ThreadDaemon td2 = new ThreadDaemon();
  
          td1.setName("关羽");
          td2.setName("张飞");
  
          //设置主线程为刘备
          Thread.currentThread().setName("刘备");
  
          //设置守护线程
          td1.setDaemon(true);
          td2.setDaemon(true);
  
          td1.start();
          td2.start();
  
          for(int i=0; i<10; i++) {
              System.out.println(Thread.currentThread().getName()+":"+i);
          }
      }
  }
  ```

**29.1.6线程的生命周期【理解】**

​	线程一共有五种状态，线程在各种状态之间转换。

![线程生命周期](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E7%BA%BF%E7%A8%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.jpg)

**29.1.7实现多线程方式二：实现Runnable接口【应用】**

- Thread构造方法

  | 方法名                               | 说明                   |
  | ------------------------------------ | ---------------------- |
  | Thread(Runnable target)              | 分配一个新的Thread对象 |
  | Thread(Runnable target, String name) | 分配一个新的Thread对象 |

- 实现步骤

  - 定义一个类MyRunnable实现Runnable接口
  - 在MyRunnable类中重写run()方法
  - 创建MyRunnable类的对象
  - 创建Thread类的对象，把MyRunnable对象作为构造方法的参数
  - 启动线程

- 代码演示

  ```java
  public class MyRunnable implements Runnable {
      @Override
      public void run() {
          for(int i=0; i<100; i++) {
              System.out.println(Thread.currentThread().getName()+":"+i);
          }
      }
  }
  public class MyRunnableDemo {
      public static void main(String[] args) {
          //创建MyRunnable类的对象
          MyRunnable my = new MyRunnable();
  
          //创建Thread类的对象，把MyRunnable对象作为构造方法的参数
          //Thread(Runnable target)
  //        Thread t1 = new Thread(my);
  //        Thread t2 = new Thread(my);
          //Thread(Runnable target, String name)
          Thread t1 = new Thread(my,"高铁");
          Thread t2 = new Thread(my,"飞机");
  
          //启动线程
          t1.start();
          t2.start();
      }
  }
  ```

- 多线程的实现方案有两种

  - 继承Thread类
  - 实现Runnable接口

- 相比继承Thread类，实现Runnable接口的好处

  - 避免了Java单继承的局限性

  - 适合多个相同程序的代码去处理同一个资源的情况，把线程和程序的代码、数据有效分离，较好的体现了面向对象的设计思想

**29.2 线程同步**

**29.2.1卖票【应用】**

- 案例需求

  某电影院目前正在上映国产大片，共有100张票，而它有3个窗口卖票，请设计一个程序模拟该电影院卖票

- 实现步骤

  - 定义一个类SellTicket实现Runnable接口，里面定义一个成员变量：private int tickets = 100;

  - 在SellTicket类中重写run()方法实现卖票，代码步骤如下

  - 判断票数大于0，就卖票，并告知是哪个窗口卖的
  - 卖了票之后，总票数要减1
  - 票没有了，也可能有人来问，所以这里用死循环让卖票的动作一直执行
  - 定义一个测试类SellTicketDemo，里面有main方法，代码步骤如下
  - 创建SellTicket类的对象
  - 创建三个Thread类的对象，把SellTicket对象作为构造方法的参数，并给出对应的窗口名称
  - 启动线程

- 代码实现

  ```java
  public class SellTicket implements Runnable {
      private int tickets = 100;
      //在SellTicket类中重写run()方法实现卖票，代码步骤如下
      @Override
      public void run() {
          while (true) {
              if (tickets > 0) {
                  System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
                  tickets--;
              }
          }
      }
  }
  public class SellTicketDemo {
      public static void main(String[] args) {
          //创建SellTicket类的对象
          SellTicket st = new SellTicket();
  
          //创建三个Thread类的对象，把SellTicket对象作为构造方法的参数，并给出对应的窗口名称
          Thread t1 = new Thread(st,"窗口1");
          Thread t2 = new Thread(st,"窗口2");
          Thread t3 = new Thread(st,"窗口3");
  
          //启动线程
          t1.start();
          t2.start();
          t3.start();
      }
  }
  ```

- 执行结果

  ![卖票1(1)](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E5%8D%96%E7%A5%A81(1).jpg)

**29.2.2卖票案例的问题【理解】**

- 卖票出现了问题

  - 相同的票出现了多次

  - 出现了负数的票

- 问题产生原因

  线程执行的随机性导致的

  ```java
  public class SellTicket implements Runnable {
      private int tickets = 100;
  
      @Override
      public void run() {
          //相同的票出现了多次
  //        while (true) {
  //            //tickets = 100;
  //            //t1,t2,t3
  //            //假设t1线程抢到CPU的执行权
  //            if (tickets > 0) {
  //                //通过sleep()方法来模拟出票时间
  //                try {
  //                    Thread.sleep(100);
  //                    //t1线程休息100毫秒
  //                    //t2线程抢到了CPU的执行权，t2线程就开始执行，执行到这里的时候，t2线程休息100毫秒
  //                    //t3线程抢到了CPU的执行权，t3线程就开始执行，执行到这里的时候，t3线程休息100毫秒
  //                } catch (InterruptedException e) {
  //                    e.printStackTrace();
  //                }
  //                //假设线程按照顺序醒过来
  //                //t1抢到CPU的执行权，在控制台输出：窗口1正在出售第100张票
  //                System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
  //                //t2抢到CPU的执行权，在控制台输出：窗口2正在出售第100张票
  //                //t3抢到CPU的执行权，在控制台输出：窗口3正在出售第100张票
  //                tickets--;
  //                //如果这三个线程还是按照顺序来，这里就执行了3次--的操作，最终票就变成了97
  //            }
  //        }
  
          //出现了负数的票
          while (true) {
              //tickets = 1;
              //t1,t2,t3
              //假设t1线程抢到CPU的执行权
              if (tickets > 0) {
                  //通过sleep()方法来模拟出票时间
                  try {
                      Thread.sleep(100);
                      //t1线程休息100毫秒
                      //t2线程抢到了CPU的执行权，t2线程就开始执行，执行到这里的时候，t2线程休息100毫秒
                      //t3线程抢到了CPU的执行权，t3线程就开始执行，执行到这里的时候，t3线程休息100毫秒
                  } catch (InterruptedException e) {
                      e.printStackTrace();
                  }
                  //假设线程按照顺序醒过来
                  //t1抢到了CPU的执行权，在控制台输出：窗口1正在出售第1张票
                  //假设t1继续拥有CPU的执行权，就会执行tickets--;操作，tickets = 0;
                  //t2抢到了CPU的执行权，在控制台输出：窗口1正在出售第0张票
                  //假设t2继续拥有CPU的执行权，就会执行tickets--;操作，tickets = -1;
                  //t3抢到了CPU的执行权，在控制台输出：窗口3正在出售第-1张票
                  //假设t2继续拥有CPU的执行权，就会执行tickets--;操作，tickets = -2;
                  System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
                  tickets--;
              }
          }
      }
  }
  ```

**29.2.3同步代码块解决数据安全问题【应用】**

- 安全问题出现的条件

  - 是多线程环境

  - 有共享数据

  - 有多条语句操作共享数据

- 如何解决多线程安全问题呢?

  - 基本思想：让程序没有安全问题的环境

- 怎么实现呢?

  - 把多条语句操作共享数据的代码给锁起来，让任意时刻只能有一个线程执行即可

  - Java提供了同步代码块的方式来解决

- 同步代码块格式：

  ```java
  synchronized(任意对象) { 
  	多条语句操作共享数据的代码 
  }
  ```

  synchronized(任意对象)：就相当于给代码加锁了，任意对象就可以看成是一把锁

- 同步的好处和弊端  

  - 好处：解决了多线程的数据安全问题

  - 弊端：当线程很多时，因为每个线程都会去判断同步上的锁，这是很耗费资源的，无形中会降低程序的运行效率

- 代码演示

  ```java
  public class SellTicket implements Runnable {
      private int tickets = 100;
      private Object obj = new Object();
  
      @Override
      public void run() {
          while (true) {
              //tickets = 100;
              //t1,t2,t3
              //假设t1抢到了CPU的执行权
              //假设t2抢到了CPU的执行权
              synchronized (obj) {
                  //t1进来后，就会把这段代码给锁起来
                  if (tickets > 0) {
                      try {
                          Thread.sleep(100);
                          //t1休息100毫秒
                      } catch (InterruptedException e) {
                          e.printStackTrace();
                      }
                      //窗口1正在出售第100张票
                      System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
                      tickets--; //tickets = 99;
                  }
              }
              //t1出来了，这段代码的锁就被释放了
          }
      }
  }
  
  public class SellTicketDemo {
      public static void main(String[] args) {
          SellTicket st = new SellTicket();
  
          Thread t1 = new Thread(st, "窗口1");
          Thread t2 = new Thread(st, "窗口2");
          Thread t3 = new Thread(st, "窗口3");
  
          t1.start();
          t2.start();
          t3.start();
      }
  }
  ```

**29.2.4同步方法解决数据安全问题【应用】**

- 同步方法的格式

  同步方法：就是把synchronized关键字加到方法上

  ```java
  修饰符 synchronized 返回值类型 方法名(方法参数) { 
  	方法体；
  }
  ```

  同步方法的锁对象是什么呢?

  ​	this

- 静态同步方法

  同步静态方法：就是把synchronized关键字加到静态方法上

  ```java
  修饰符 static synchronized 返回值类型 方法名(方法参数) { 
  	方法体；
  }
  ```

  同步静态方法的锁对象是什么呢?

  ​	类名.class

- 代码演示

  ```java
  public class SellTicket implements Runnable {
      private static int tickets = 100;
      private int x = 0;
  
      @Override
      public void run() {
          while (true) {
  			sellTicket()；
      	}
      }
  //    同步方法
  //    private synchronized void sellTicket() {
  //        if (tickets > 0) {
  //            try {
  //                Thread.sleep(100);
  //            } catch (InterruptedException e) {
  //                e.printStackTrace();
  //            }
  //            System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
  //            tickets--;
  //        }
  //    }
      
  //  静态同步方法
      private static synchronized void sellTicket() {
          if (tickets > 0) {
              try {
                  Thread.sleep(100);
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
              System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
              tickets--;
          }
      }
  }
  
  public class SellTicketDemo {
      public static void main(String[] args) {
          SellTicket st = new SellTicket();
  
          Thread t1 = new Thread(st, "窗口1");
          Thread t2 = new Thread(st, "窗口2");
          Thread t3 = new Thread(st, "窗口3");
  
          t1.start();
          t2.start();
          t3.start();
      }
  }
  ```

**29.2.5线程安全的类【理解】**

- StringBuffer

  - 线程安全，可变的字符序列

  - 从版本JDK 5开始，被StringBuilder 替代。 通常应该使用StringBuilder类，因为它支持所有相同的操作，但它更快，因为它不执行同步

- Vector
  - 从Java 2平台v1.2开始，该类改进了List接口，使其成为Java Collections Framework的成员。 与新的集合实现不同， Vector被同步。 如果不需要线程安全的实现，建议使用ArrayList代替Vector

- Hashtable
  - 该类实现了一个哈希表，它将键映射到值。 任何非null对象都可以用作键或者值
  - 从Java 2平台v1.2开始，该类进行了改进，实现了Map接口，使其成为Java Collections Framework的成员。 与新的集合实现不同， Hashtable被同步。 如果不需要线程安全的实现，建议使用HashMap代替Hashtable

**29.2.6Lock锁【应用】**

虽然我们可以理解同步代码块和同步方法的锁对象问题，但是我们并没有直接看到在哪里加上了锁，在哪里释放了锁，为了更清晰的表达如何加锁和释放锁，JDK5以后提供了一个新的锁对象Lock

Lock是接口不能直接实例化，这里采用它的实现类ReentrantLock来实例化

- ReentrantLock构造方法

  | 方法名          | 说明                        |
  | --------------- | --------------------------- |
  | ReentrantLock() | 创建一个ReentrantLock的实例 |

- 加锁解锁方法

  | 方法名        | 说明   |
  | ------------- | ------ |
  | void lock()   | 获得锁 |
  | void unlock() | 释放锁 |

- 代码演示

  ```java
  public class SellTicket implements Runnable {
      private int tickets = 100;
      private Lock lock = new ReentrantLock();
  
      @Override
      public void run() {
          while (true) {
              try {
                  lock.lock();
                  if (tickets > 0) {
                      try {
                          Thread.sleep(100);
                      } catch (InterruptedException e) {
                          e.printStackTrace();
                      }
                      System.out.println(Thread.currentThread().getName() + "正在出售第" + tickets + "张票");
                      tickets--;
                  }
              } finally {
                  lock.unlock();
              }
          }
      }
  }
  public class SellTicketDemo {
      public static void main(String[] args) {
          SellTicket st = new SellTicket();
  
          Thread t1 = new Thread(st, "窗口1");
          Thread t2 = new Thread(st, "窗口2");
          Thread t3 = new Thread(st, "窗口3");
  
          t1.start();
          t2.start();
          t3.start();
      }
  }
  ```

**29.3 生产者消费者**

**29.3.1生产者和消费者模式概述【应用】**

- 概述

  生产者消费者模式是一个十分经典的多线程协作的模式，弄懂生产者消费者问题能够让我们对多线程编程的理解更加深刻。

  所谓生产者消费者问题，实际上主要是包含了两类线程：

  ​	一类是生产者线程用于生产数据

  ​	一类是消费者线程用于消费数据

  为了解耦生产者和消费者的关系，通常会采用共享的数据区域，就像是一个仓库

  生产者生产数据之后直接放置在共享数据区中，并不需要关心消费者的行为

  消费者只需要从共享数据区中去获取数据，并不需要关心生产者的行为

  ![生产消费](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/%E7%94%9F%E4%BA%A7%E6%B6%88%E8%B4%B9.jpg)

- Object类的等待和唤醒方法

  | 方法名           | 说明                                                         |
  | ---------------- | ------------------------------------------------------------ |
  | void wait()      | 导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法 |
  | void notify()    | 唤醒正在等待对象监视器的单个线程                             |
  | void notifyAll() | 唤醒正在等待对象监视器的所有线程                             |

**29.3.2生产者和消费者案例【应用】**

- 案例需求

  生产者消费者案例中包含的类：

  奶箱类(Box)：定义一个成员变量，表示第x瓶奶，提供存储牛奶和获取牛奶的操作

  生产者类(Producer)：实现Runnable接口，重写run()方法，调用存储牛奶的操作

  消费者类(Customer)：实现Runnable接口，重写run()方法，调用获取牛奶的操作

  测试类(BoxDemo)：里面有main方法，main方法中的代码步骤如下

  ①创建奶箱对象，这是共享数据区域

  ②创建消费者创建生产者对象，把奶箱对象作为构造方法参数传递，因为在这个类中要调用存储牛奶的操作

  ③对象，把奶箱对象作为构造方法参数传递，因为在这个类中要调用获取牛奶的操作

  ④创建2个线程对象，分别把生产者对象和消费者对象作为构造方法参数传递

  ⑤启动线程

- 代码实现

  ```java
  public class Box {
      //定义一个成员变量，表示第x瓶奶
      private int milk;
      //定义一个成员变量，表示奶箱的状态
      private boolean state = false;
  
      //提供存储牛奶和获取牛奶的操作
      public synchronized void put(int milk) {
          //如果有牛奶，等待消费
          if(state) {
              try {
                  wait();
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
          }
  
          //如果没有牛奶，就生产牛奶
          this.milk = milk;
          System.out.println("送奶工将第" + this.milk + "瓶奶放入奶箱");
  
          //生产完毕之后，修改奶箱状态
          state = true;
  
          //唤醒其他等待的线程
          notifyAll();
      }
  
      public synchronized void get() {
          //如果没有牛奶，等待生产
          if(!state) {
              try {
                  wait();
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
          }
  
          //如果有牛奶，就消费牛奶
          System.out.println("用户拿到第" + this.milk + "瓶奶");
  
          //消费完毕之后，修改奶箱状态
          state = false;
  
          //唤醒其他等待的线程
          notifyAll();
      }
  }
  
  public class Producer implements Runnable {
      private Box b;
  
      public Producer(Box b) {
          this.b = b;
      }
  
      @Override
      public void run() {
          for(int i=1; i<=30; i++) {
              b.put(i);
          }
      }
  }
  
  public class Customer implements Runnable {
      private Box b;
  
      public Customer(Box b) {
          this.b = b;
      }
  
      @Override
      public void run() {
          while (true) {
              b.get();
          }
      }
  }
  
  public class BoxDemo {
      public static void main(String[] args) {
          //创建奶箱对象，这是共享数据区域
          Box b = new Box();
  
          //创建生产者对象，把奶箱对象作为构造方法参数传递，因为在这个类中要调用存储牛奶的操作
          Producer p = new Producer(b);
          //创建消费者对象，把奶箱对象作为构造方法参数传递，因为在这个类中要调用获取牛奶的操作
          Customer c = new Customer(b);
  
          //创建2个线程对象，分别把生产者对象和消费者对象作为构造方法参数传递
          Thread t1 = new Thread(p);
          Thread t2 = new Thread(c);
  
          //启动线程
          t1.start();
          t2.start();
      }
  }
  ```

## 30 网络编程

**30.1 网络编程入门**

**30.1.1 网络编程概述【理解】**

- 计算机网络

  是指将地理位置不同的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，在网络操作系统，网络管理软件及网络通信协议的管理和协调下，实现资源共享和信息传递的计算机系统

- 网络编程

  在网络通信协议下，实现网络互连的不同计算机上运行的程序间可以进行数据交换

**30.1.2 网络编程三要素【理解】**

- IP地址

  要想让网络中的计算机能够互相通信，必须为每台计算机指定一个标识号，通过这个标识号来指定要接收数据的计算机和识别发送的计算机，而IP地址就是这个标识号。也就是设备的标识

- 端口

  网络的通信，本质上是两个应用程序的通信。每台计算机都有很多的应用程序，那么在网络通信时，如何区分这些应用程序呢？如果说IP地址可以唯一标识网络中的设备，那么端口号就可以唯一标识设备中的应用程序了。也就是应用程序的标识

- 协议

  通过计算机网络可以使多台计算机实现连接，位于同一个网络中的计算机在进行连接和通信时需要遵守一定的规则，这就好比在道路中行驶的汽车一定要遵守交通规则一样。在计算机网络中，这些连接和通信的规则被称为网络通信协议，它对数据的传输格式、传输速率、传输步骤等做了统一规定，通信双方必须同时遵守才能完成数据交换。常见的协议有UDP协议和TCP协议

**30.1.3 IP地址【理解】**

IP地址：是网络中设备的唯一标识

- IP地址分为两大类

  - IPv4：是给每个连接在网络上的主机分配一个32bit地址。按照TCP/IP规定，IP地址用二进制来表示，每个IP地址长32bit，也就是4个字节。例如一个采用二进制形式的IP地址是“11000000 10101000 00000001 01000010”，这么长的地址，处理起来也太费劲了。为了方便使用，IP地址经常被写成十进制的形式，中间使用符号“.”分隔不同的字节。于是，上面的IP地址可以表示为“192.168.1.66”。IP地址的这种表示法叫做“点分十进制表示法”，这显然比1和0容易记忆得多

  - IPv6：由于互联网的蓬勃发展，IP地址的需求量愈来愈大，但是网络地址资源有限，使得IP的分配越发紧张。为了扩大地址空间，通过IPv6重新定义地址空间，采用128位地址长度，每16个字节一组，分成8组十六进制数，这样就解决了网络地址资源数量不够的问题

- DOS常用命令：

  - ipconfig：查看本机IP地址

  - ping IP地址：检查网络是否连通

- 特殊IP地址：
  - 127.0.0.1：是回送地址，可以代表本机地址，一般用来测试使用

**30.1.4InetAddress【应用】**

InetAddress：此类表示Internet协议（IP）地址

- 相关方法

  | 方法名                                    | 说明                                                         |
  | ----------------------------------------- | ------------------------------------------------------------ |
  | static InetAddress getByName(String host) | 确定主机名称的IP地址。主机名称可以是机器名称，也可以是IP地址 |
  | String getHostName()                      | 获取此IP地址的主机名                                         |
  | String getHostAddress()                   | 返回文本显示中的IP地址字符串                                 |

- 代码演示

  ```java
  public class InetAddressDemo {
      public static void main(String[] args) throws UnknownHostException {
  		//InetAddress address = InetAddress.getByName("itheima");
          InetAddress address = InetAddress.getByName("192.168.1.66");
  
          //public String getHostName()：获取此IP地址的主机名
          String name = address.getHostName();
          //public String getHostAddress()：返回文本显示中的IP地址字符串
          String ip = address.getHostAddress();
  
          System.out.println("主机名：" + name);
          System.out.println("IP地址：" + ip);
      }
  }
  ```

**30.1.5端口和协议【理解】**

- 端口

  - 设备上应用程序的唯一标识

- 端口号

  - 用两个字节表示的整数，它的取值范围是0~65535。其中，0~1023之间的端口号用于一些知名的网络服务和应用，普通的应用程序需要使用1024以上的端口号。如果端口号被另外一个服务或应用所占用，会导致当前程序启动失败

- 协议

  - 计算机网络中，连接和通信的规则被称为网络通信协议

- UDP协议

  - 用户数据报协议(User Datagram Protocol)
  - UDP是无连接通信协议，即在数据传输时，数据的发送端和接收端不建立逻辑连接。简单来说，当一台计算机向另外一台计算机发送数据时，发送端不会确认接收端是否存在，就会发出数据，同样接收端在收到数据时，也不会向发送端反馈是否收到数据。
  - 由于使用UDP协议消耗资源小，通信效率高，所以通常都会用于音频、视频和普通数据的传输
  - 例如视频会议通常采用UDP协议，因为这种情况即使偶尔丢失一两个数据包，也不会对接收结果产生太大影响。但是在使用UDP协议传送数据时，由于UDP的面向无连接性，不能保证数据的完整性，因此在传输重要数据时不建议使用UDP协议

- TCP协议

  - 传输控制协议 (Transmission Control Protocol)

  - TCP协议是面向连接的通信协议，即传输数据之前，在发送端和接收端建立逻辑连接，然后再传输数据，它提供了两台计算机之间可靠无差错的数据传输。在TCP连接中必须要明确客户端与服务器端，由客户端向服务端发出连接请求，每次连接的创建都需要经过“三次握手”

  - 三次握手：TCP协议中，在发送数据的准备阶段，客户端与服务器之间的三次交互，以保证连接的可靠

    第一次握手，客户端向服务器端发出连接请求，等待服务器确认

    第二次握手，服务器端向客户端回送一个响应，通知客户端收到了连接请求

    第三次握手，客户端再次向服务器端发送确认信息，确认连接

  - 完成三次握手，连接建立后，客户端和服务器就可以开始进行数据传输了。由于这种面向连接的特性，TCP协议可以保证传输数据的安全，所以应用十分广泛。例如上传文件、下载文件、浏览网页等

### 30.2 UDP通信程序

**30.2.1 UDP发送数据【应用】**

- Java中的UDP通信

  - UDP协议是一种不可靠的网络协议，它在通信的两端各建立一个Socket对象，但是这两个Socket只是发送，接收数据的对象，因此对于基于UDP协议的通信双方而言，没有所谓的客户端和服务器的概念
  - Java提供了DatagramSocket类作为基于UDP协议的Socket

- 构造方法

  | 方法名                                                      | 说明                                                 |
  | ----------------------------------------------------------- | ---------------------------------------------------- |
  | DatagramSocket()                                            | 创建数据报套接字并将其绑定到本机地址上的任何可用端口 |
  | DatagramPacket(byte[] buf,int len,InetAddress add,int port) | 创建数据包,发送长度为len的数据包到指定主机的指定端口 |

- 相关方法

  | 方法名                         | 说明                   |
  | ------------------------------ | ---------------------- |
  | void send(DatagramPacket p)    | 发送数据报包           |
  | void close()                   | 关闭数据报套接字       |
  | void receive(DatagramPacket p) | 从此套接字接受数据报包 |

- 发送数据的步骤

  - 创建发送端的Socket对象(DatagramSocket)
  - 创建数据，并把数据打包
  - 调用DatagramSocket对象的方法发送数据
  - 关闭发送端

- 代码演示

  ```java
  public class SendDemo {
      public static void main(String[] args) throws IOException {
          //创建发送端的Socket对象(DatagramSocket)
          // DatagramSocket() 构造数据报套接字并将其绑定到本地主机上的任何可用端口
          DatagramSocket ds = new DatagramSocket();
  
          //创建数据，并把数据打包
          //DatagramPacket(byte[] buf, int length, InetAddress address, int port)
          //构造一个数据包，发送长度为 length的数据包到指定主机上的指定端口号。
          byte[] bys = "hello,udp,我来了".getBytes();
  
          DatagramPacket dp = new DatagramPacket(bys,bys.length,InetAddress.getByName("192.168.1.66"),10086);
  
          //调用DatagramSocket对象的方法发送数据
          //void send(DatagramPacket p) 从此套接字发送数据报包
          ds.send(dp);
  
          //关闭发送端
          //void close() 关闭此数据报套接字
          ds.close();
      }
  }
  ```

**30.2.2UDP接收数据【应用】**

- 接收数据的步骤

  - 创建接收端的Socket对象(DatagramSocket)
  - 创建一个数据包，用于接收数据
  - 调用DatagramSocket对象的方法接收数据
  - 解析数据包，并把数据在控制台显示
  - 关闭接收端

- 构造方法

  | 方法名                              | 说明                                            |
  | ----------------------------------- | ----------------------------------------------- |
  | DatagramPacket(byte[] buf, int len) | 创建一个DatagramPacket用于接收长度为len的数据包 |

- 相关方法

  | 方法名            | 说明                                     |
  | ----------------- | ---------------------------------------- |
  | byte[]  getData() | 返回数据缓冲区                           |
  | int  getLength()  | 返回要发送的数据的长度或接收的数据的长度 |

- 示例代码

  ```java
  public class ReceiveDemo {
      public static void main(String[] args) throws IOException {
          //创建接收端的Socket对象(DatagramSocket)
          DatagramSocket ds = new DatagramSocket(12345);
  
          while (true) {
              //创建一个数据包，用于接收数据
              byte[] bys = new byte[1024];
              DatagramPacket dp = new DatagramPacket(bys, bys.length);
  
              //调用DatagramSocket对象的方法接收数据
              ds.receive(dp);
  
              //解析数据包，并把数据在控制台显示
              System.out.println("数据是：" + new String(dp.getData(), 0,                                             dp.getLength()));
          }
      }
  }
  ```

**30.2.3UDP通信程序练习【应用】**

- 案例需求

  UDP发送数据：数据来自于键盘录入，直到输入的数据是886，发送数据结束

  UDP接收数据：因为接收端不知道发送端什么时候停止发送，故采用死循环接收

- 代码实现

  ```java
  /*
      UDP发送数据：
          数据来自于键盘录入，直到输入的数据是886，发送数据结束
   */
  public class SendDemo {
      public static void main(String[] args) throws IOException {
          //创建发送端的Socket对象(DatagramSocket)
          DatagramSocket ds = new DatagramSocket();
          //自己封装键盘录入数据
          BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
          String line;
          while ((line = br.readLine()) != null) {
              //输入的数据是886，发送数据结束
              if ("886".equals(line)) {
                  break;
              }
              //创建数据，并把数据打包
              byte[] bys = line.getBytes();
              DatagramPacket dp = new DatagramPacket(bys, bys.length, InetAddress.getByName("192.168.1.66"), 12345);
  
              //调用DatagramSocket对象的方法发送数据
              ds.send(dp);
          }
          //关闭发送端
          ds.close();
      }
  }
  
  /*
      UDP接收数据：
          因为接收端不知道发送端什么时候停止发送，故采用死循环接收
   */
  public class ReceiveDemo {
      public static void main(String[] args) throws IOException {
          //创建接收端的Socket对象(DatagramSocket)
          DatagramSocket ds = new DatagramSocket(12345);
          while (true) {
              //创建一个数据包，用于接收数据
              byte[] bys = new byte[1024];
              DatagramPacket dp = new DatagramPacket(bys, bys.length);
              //调用DatagramSocket对象的方法接收数据
              ds.receive(dp);
              //解析数据包，并把数据在控制台显示
              System.out.println("数据是：" + new String(dp.getData(), 0, dp.getLength()));
          }
          //关闭接收端
  //        ds.close();
      }
  }
  ```

### 30.3 TCP通信程序

**30.3.1TCP发送数据【应用】**

- Java中的TCP通信

  - Java对基于TCP协议的的网络提供了良好的封装，使用Socket对象来代表两端的通信端口，并通过Socket产生IO流来进行网络通信。
  - Java为客户端提供了Socket类，为服务器端提供了ServerSocket类

- 构造方法

  | 方法名                               | 说明                                           |
  | ------------------------------------ | ---------------------------------------------- |
  | Socket(InetAddress address,int port) | 创建流套接字并将其连接到指定IP指定端口号       |
  | Socket(String host, int port)        | 创建流套接字并将其连接到指定主机上的指定端口号 |

- 相关方法

  | 方法名                         | 说明                 |
  | ------------------------------ | -------------------- |
  | InputStream  getInputStream()  | 返回此套接字的输入流 |
  | OutputStream getOutputStream() | 返回此套接字的输出流 |

- 示例代码

  ```java
  public class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端的Socket对象(Socket)
          //Socket(String host, int port) 创建流套接字并将其连接到指定主机上的指定端口号
          Socket s = new Socket("192.168.1.66",10000);
  
          //获取输出流，写数据
          //OutputStream getOutputStream() 返回此套接字的输出流
          OutputStream os = s.getOutputStream();
          os.write("hello,tcp,我来了".getBytes());
  
          //释放资源
          s.close();
      }
  }
  ```

**30.3.2TCP接收数据【应用】**

- 构造方法

  | 方法名                  | 说明                             |
  | ----------------------- | -------------------------------- |
  | ServletSocket(int port) | 创建绑定到指定端口的服务器套接字 |

- 相关方法

  | 方法名          | 说明                           |
  | --------------- | ------------------------------ |
  | Socket accept() | 监听要连接到此的套接字并接受它 |

- 示例代码

  ```java
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器端的Socket对象(ServerSocket)
          //ServerSocket(int port) 创建绑定到指定端口的服务器套接字
          ServerSocket ss = new ServerSocket(10000);
  
          //Socket accept() 侦听要连接到此套接字并接受它
          Socket s = ss.accept();
  
          //获取输入流，读数据，并把数据显示在控制台
          InputStream is = s.getInputStream();
          byte[] bys = new byte[1024];
          int len = is.read(bys);
          String data = new String(bys,0,len);
          System.out.println("数据是：" + data);
  
          //释放资源
          s.close();
          ss.close();
      }
  }
  ```

**30.3.3TCP通信程序练习【应用】**

- 案例需求

  客户端：发送数据，接受服务器反馈

  服务器：收到消息后给出反馈

- 案例分析

  - 客户端创建对象，使用输出流输出数据
  - 服务端创建对象，使用输入流接受数据
  - 服务端使用输出流给出反馈数据
  - 客户端使用输入流接受反馈数据

- 代码实现

  ```java
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器端的Socket对象(ServerSocket)
          ServerSocket ss = new ServerSocket(10000);
  
          //监听客户端连接，返回一个Socket对象
          Socket s = ss.accept();
  
          //获取输入流，读数据，并把数据显示在控制台
          InputStream is = s.getInputStream();
          byte[] bys = new byte[1024];
          int len = is.read(bys);
          String data = new String(bys, 0, len);
          System.out.println("服务器：" + data);
  
          //给出反馈
          OutputStream os = s.getOutputStream();
          os.write("数据已经收到".getBytes());
  
          //释放资源
  //        s.close();
          ss.close();
      }
  }
  
  public class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端的Socket对象(Socket)
          Socket s = new Socket("192.168.1.66", 10000);
  
          //获取输出流，写数据
          OutputStream os = s.getOutputStream();
          os.write("hello,tcp,我来了".getBytes());
  
          //接收服务器反馈
          InputStream is = s.getInputStream();
          byte[] bys = new byte[1024];
          int len = is.read(bys);
          String data = new String(bys, 0, len);
          System.out.println("客户端：" + data);
  
          //释放资源
  //        is.close();
  //        os.close();
          s.close();
      }
  }
  ```

**30.3.4TCP通信程序练习【应用】**

- 案例需求

  客户端：数据来自于键盘录入, 直到输入的数据是886，发送数据结束

  服务端：接收到数据在控制台输出

- 案例分析

  - 客户端创建对象，使用键盘录入循环接受数据，接受一行发送一行，直到键盘录入886为止
  - 服务端创建对象，使用输入流按行循环接受数据，直到接受到null为止

- 代码实现

  ```java
  public class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端Socket对象
          Socket s = new Socket("192.168.1.66",10000);
  
          //数据来自于键盘录入，直到输入的数据是886，发送数据结束
          BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
          //封装输出流对象
          BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
          String line;
          while ((line=br.readLine())!=null) {
              if("886".equals(line)) {
                  break;
              }
  
              //获取输出流对象
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          s.close();
      }
  }
  
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器Socket对象
          ServerSocket ss = new ServerSocket(10000);
  
          //监听客户端的连接，返回一个对应的Socket对象
          Socket s = ss.accept();
  
          //获取输入流
          BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
          String line;
          while ((line = br.readLine()) != null) {
              System.out.println(line);
          }
  
          //释放资源
          ss.close();
      }
  }
  ```

**30.3.5TCP通信程序练习【应用】**

- 案例需求

  客户端：数据来自于键盘录入，直到输入的数据是886,发送数据结束

  服务端：接受到的数据写入文本文件中

- 案例分析

  - 客户端创建对象，使用键盘录入循环接受数据，接受一行发送一行，直到键盘录入886为止
  - 服务端创建对象，创建输出流对象指向文件，每接受一行数据后使用输出流输出到文件中，直到接受到null为止

- 代码实现

  ```java
  ublic class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端Socket对象
          Socket s = new Socket("192.168.1.66",10000);
          //数据来自于键盘录入，直到输入的数据是886，发送数据结束
          BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
          //封装输出流对象
          BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
          String line;
          while ((line=br.readLine())!=null) {
              if("886".equals(line)) {
                  break;
              }
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
          //释放资源
          s.close();
      }
  }
  
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器Socket对象
          ServerSocket ss = new ServerSocket(10000);
          //监听客户端连接，返回一个对应的Socket对象
          Socket s = ss.accept();
          //接收数据
          BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
          //把数据写入文本文件
          BufferedWriter bw = new BufferedWriter(new FileWriter("myNet\\s.txt"));
  
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          bw.close();
          ss.close();
      }
  }
  ```

**30.3.6TCP通信程序练习【应用】**

- 案例需求

  客户端：数据来自于文本文件

  服务器：接收到的数据写入文本文件

- 案例分析

  - 创建客户端，创建输入流对象指向文件，从文件循环读取数据，每读取一行就使用输出流给服务器输出一行
  - 创建服务端，创建输出流对象指向文件，从客户端接受数据，每接受一行就给文件中输出一行

- 代码实现

  ```java
  public class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端Socket对象
          Socket s = new Socket("192.168.1.66",10000);
  
          //封装文本文件的数据
          BufferedReader br = new BufferedReader(new FileReader("myNet\\InetAddressDemo.java"));
          //封装输出流写数据
          BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
  
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          br.close();
          s.close();
      }
  }
  
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器Socket对象
          ServerSocket ss = new ServerSocket(10000);
  
          //监听客户端连接，返回一个对应的Socket对象
          Socket s = ss.accept();
  
          //接收数据
          BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
          //把数据写入文本文件
          BufferedWriter bw = new BufferedWriter(new FileWriter("myNet\\Copy.java"));
  
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //释放资源
          bw.close();
          ss.close();
      }
  }
  
  ```

**30.3.7TCP通信程序练习【应用】**

- 案例需求

  客户端：数据来自于文本文件，接收服务器反馈

  服务器：接收到的数据写入文本文件，给出反馈

- 案例分析

  - 创建客户端对象，创建输入流对象指向文件，每读入一行数据就给服务器输出一行数据，输出结束后使用shutdownOutput()方法告知服务端传输结束
  - 创建服务器对象，创建输出流对象指向文件，每接受一行数据就使用输出流输出到文件中，传输结束后。使用输出流给客户端反馈信息
  - 客户端接受服务端的回馈信息

- 相关方法

  | 方法名                | 说明                               |
  | --------------------- | ---------------------------------- |
  | void shutdownInput()  | 将此套接字的输入流放置在“流的末尾” |
  | void shutdownOutput() | 禁止用此套接字的输出流             |

- 代码实现

  ```java
  public class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端Socket对象
          Socket s = new Socket("192.168.1.66",10000);
  
          //封装文本文件的数据
          BufferedReader br = new BufferedReader(new FileReader("myNet\\InetAddressDemo.java"));
          //封装输出流写数据
          BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
  
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          //public void shutdownOutput()
          s.shutdownOutput();
  
          //接收反馈
          BufferedReader brClient = new BufferedReader(new InputStreamReader(s.getInputStream()));
          String data = brClient.readLine(); //等待读取数据
          System.out.println("服务器的反馈：" + data);
  
          //释放资源
          br.close();
          s.close();
      }
  }
  
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器Socket对象
          ServerSocket ss = new ServerSocket(10000);
  
          //监听客户端连接，返回一个对应的Socket对象
          Socket s = ss.accept();
  
          //接收数据
          BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
          //把数据写入文本文件
          BufferedWriter bw = new BufferedWriter(new FileWriter("myNet\\Copy.java"));
  
          String line;
          while ((line=br.readLine())!=null) { //等待读取数据
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
          //给出反馈
          BufferedWriter bwServer = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
          bwServer.write("文件上传成功");
          bwServer.newLine();
          bwServer.flush();
  
          //释放资源
          bw.close();
          ss.close();
      }
  }
  
  ```

**30.3.8TCP通信程序练习【应用】**

- 案例需求

  客户端：数据来自于文本文件，接收服务器反馈

  服务器：接收到的数据写入文本文件，给出反馈，代码用线程进行封装，为每一个客户端开启一个线程

- 案例分析

  - 创建客户端对象，创建输入流对象指向文件，每读入一行数据就给服务器输出一行数据，输出结束后使用shutdownOutput()方法告知服务端传输结束
  - 创建多线程类，在run()方法中读取客户端发送的数据，为了防止文件重名，使用计数器给文件名编号，接受结束后使用输出流给客户端发送反馈信息。
  - 创建服务端对象，每监听到一个客户端则开启一个新的线程接受数据。
  - 客户端接受服务端的回馈信息

- 代码实现

  ```java
  public class ClientDemo {
      public static void main(String[] args) throws IOException {
          //创建客户端Socket对象
          Socket s = new Socket("192.168.1.66",10000);
  
          //封装文本文件的数据
          BufferedReader br = new BufferedReader(new FileReader("myNet\\InetAddressDemo.java"));
          //封装输出流写数据
          BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
  
          String line;
          while ((line=br.readLine())!=null) {
              bw.write(line);
              bw.newLine();
              bw.flush();
          }
  
          s.shutdownOutput();
  
          //接收反馈
          BufferedReader brClient = new BufferedReader(new InputStreamReader(s.getInputStream()));
          String data = brClient.readLine(); //等待读取数据
          System.out.println("服务器的反馈：" + data);
  
          //释放资源
          br.close();
          s.close();
      }
  }
  
  public class ServerThread implements Runnable {
      private Socket s;
  
      public ServerThread(Socket s) {
          this.s = s;
      }
  
      @Override
      public void run() {
          try {
              //接收数据写到文本文件
              BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
              //解决名称冲突问题
              int count = 0;
              File file = new File("myNet\\Copy["+count+"].java");
              while (file.exists()) {
                  count++;
                  file = new File("myNet\\Copy["+count+"].java");
              }
              BufferedWriter bw = new BufferedWriter(new FileWriter(file));
  
              String line;
              while ((line=br.readLine())!=null) {
                  bw.write(line);
                  bw.newLine();
                  bw.flush();
              }
  
              //给出反馈
              BufferedWriter bwServer = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
              bwServer.write("文件上传成功");
              bwServer.newLine();
              bwServer.flush();
  
              //释放资源
              s.close();
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  
  public class ServerDemo {
      public static void main(String[] args) throws IOException {
          //创建服务器Socket对象
          ServerSocket ss = new ServerSocket(10000);
  
          while (true) {
              //监听客户端连接，返回一个对应的Socket对象
              Socket s = ss.accept();
              //为每一个客户端开启一个线程
              new Thread(new ServerThread(s)).start();
          }
  
      }
  }
  ```

## 31 JDK新特性

### 31.1 Lambda表达式

**31.1.1体验Lambda表达式【理解】**

- 案例需求

  启动一个线程，在控制台输出一句话：多线程程序启动了

- 实现方式一

  - 实现步骤
    - 定义一个类MyRunnable实现Runnable接口，重写run()方法
    - 创建MyRunnable类的对象
    - 创建Thread类的对象，把MyRunnable的对象作为构造参数传递
    - 启动线程

- 实现方式二

  - 匿名内部类的方式改进

- 实现方式三

  - Lambda表达式的方式改进

- 代码演示

  ```java
  //方式一的线程类
  public class MyRunnable implements Runnable {
  
      @Override
      public void run() {
          System.out.println("多线程程序启动了");
      }
  }
  
  public class LambdaDemo {
      public static void main(String[] args) {
          //方式一
  //        MyRunnable my = new MyRunnable();
  //        Thread t = new Thread(my);
  //        t.start();
  
          //方式二
  //        new Thread(new Runnable() {
  //            @Override
  //            public void run() {
  //                System.out.println("多线程程序启动了");
  //            }
  //        }).start();
  
          //方式三
          new Thread( () -> {
              System.out.println("多线程程序启动了");
          } ).start();
      }
  }
  ```

- 函数式编程思想概述

  函数式思想则尽量忽略面向对象的复杂语法：“强调做什么，而不是以什么形式去做”

  而我们要学习的Lambda表达式就是函数式思想的体现

**31.1.2Lambda表达式的标准格式【理解】**

- 格式：

  ​	(形式参数) -> {代码块}

  - 形式参数：如果有多个参数，参数之间用逗号隔开；如果没有参数，留空即可

  - ->：由英文中画线和大于符号组成，固定写法。代表指向动作

  - 代码块：是我们具体要做的事情，也就是以前我们写的方法体内容

- 组成Lambda表达式的三要素：

  - 形式参数，箭头，代码块

**31.1.3Lambda表达式练习1【应用】**

- Lambda表达式的使用前提

  - 有一个接口

  - 接口中有且仅有一个抽象方法

- 练习描述

  ​	无参无返回值抽象方法的练习

- 操作步骤

  - 定义一个接口(Eatable)，里面定义一个抽象方法：void eat();

  - 定义一个测试类(EatableDemo)，在测试类中提供两个方法

    - 一个方法是：useEatable(Eatable e)

    - 一个方法是主方法，在主方法中调用useEatable方法

- 示例代码

  ```java
  //接口
  public interface Eatable {
      void eat();
  }
  //实现类
  public class EatableImpl implements Eatable {
      @Override
      public void eat() {
          System.out.println("一天一苹果，医生远离我");
      }
  }
  //测试类
  public class EatableDemo {
      public static void main(String[] args) {
          //在主方法中调用useEatable方法
          Eatable e = new EatableImpl();
          useEatable(e);
  
          //匿名内部类
          useEatable(new Eatable() {
              @Override
              public void eat() {
                  System.out.println("一天一苹果，医生远离我");
              }
          });
  
          //Lambda表达式
          useEatable(() -> {
              System.out.println("一天一苹果，医生远离我");
          });
      }
  
      private static void useEatable(Eatable e) {
          e.eat();
      }
  }
  ```

**31.1.4Lambda表达式练习2【应用】**

- 练习描述

  有参无返回值抽象方法的练习

- 操作步骤

  - 定义一个接口(Flyable)，里面定义一个抽象方法：void fly(String s);

  - 定义一个测试类(FlyableDemo)，在测试类中提供两个方法

    - 一个方法是：useFlyable(Flyable f)

    - 一个方法是主方法，在主方法中调用useFlyable方法

- 示例代码

  ```java
  public interface Flyable {
      void fly(String s);
  }
  
  public class FlyableDemo {
      public static void main(String[] args) {
          //在主方法中调用useFlyable方法
          //匿名内部类
          useFlyable(new Flyable() {
              @Override
              public void fly(String s) {
                  System.out.println(s);
                  System.out.println("飞机自驾游");
              }
          });
          System.out.println("--------");
  
          //Lambda
          useFlyable((String s) -> {
              System.out.println(s);
              System.out.println("飞机自驾游");
          });
  
      }
  
      private static void useFlyable(Flyable f) {
          f.fly("风和日丽，晴空万里");
      }
  }
  ```

**31.1.5Lambda表达式练习3【应用】**

- 练习描述

  有参有返回值抽象方法的练习

- 操作步骤

  - 定义一个接口(Addable)，里面定义一个抽象方法：int add(int x,int y);

  - 定义一个测试类(AddableDemo)，在测试类中提供两个方法

    - 一个方法是：useAddable(Addable a)

    - 一个方法是主方法，在主方法中调用useAddable方法

- 示例代码

  ```java
  public interface Addable {
      int add(int x,int y);
  }
  
  public class AddableDemo {
      public static void main(String[] args) {
          //在主方法中调用useAddable方法
          useAddable((int x,int y) -> {
              return x + y;
          });
  
      }
  
      private static void useAddable(Addable a) {
          int sum = a.add(10, 20);
          System.out.println(sum);
      }
  }
  ```

**31.1.6Lambda表达式的省略模式【应用】**

- 省略的规则

  - 参数类型可以省略。但是有多个参数的情况下，不能只省略一个
  - 如果参数有且仅有一个，那么小括号可以省略
  - 如果代码块的语句只有一条，可以省略大括号和分号，和return关键字

- 代码演示

  ```java
  public interface Addable {
      int add(int x, int y);
  }
  
  public interface Flyable {
      void fly(String s);
  }
  
  public class LambdaDemo {
      public static void main(String[] args) {
  //        useAddable((int x,int y) -> {
  //            return x + y;
  //        });
          //参数的类型可以省略
          useAddable((x, y) -> {
              return x + y;
          });
  
  //        useFlyable((String s) -> {
  //            System.out.println(s);
  //        });
          //如果参数有且仅有一个，那么小括号可以省略
  //        useFlyable(s -> {
  //            System.out.println(s);
  //        });
  
          //如果代码块的语句只有一条，可以省略大括号和分号
          useFlyable(s -> System.out.println(s));
  
          //如果代码块的语句只有一条，可以省略大括号和分号，如果有return，return也要省略掉
          useAddable((x, y) -> x + y);
      }
  
      private static void useFlyable(Flyable f) {
          f.fly("风和日丽，晴空万里");
      }
  
      private static void useAddable(Addable a) {
          int sum = a.add(10, 20);
          System.out.println(sum);
      }
  }
  ```

**31.1.7Lambda表达式的注意事项【理解】**

- 使用Lambda必须要有接口，并且要求接口中有且仅有一个抽象方法

- 必须有上下文环境，才能推导出Lambda对应的接口

  - 根据局部变量的赋值得知Lambda对应的接口

    ​	Runnable r = () -> System.out.println("Lambda表达式");

  - 根据调用方法的参数得知Lambda对应的接口

    ​	new Thread(() -> System.out.println("Lambda表达式")).start();

**31.1.8Lambda表达式和匿名内部类的区别【理解】**

- 所需类型不同
  - 匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
  - Lambda表达式：只能是接口

- 使用限制不同

  - 如果接口中有且仅有一个抽象方法，可以使用Lambda表达式，也可以使用匿名内部类

  - 如果接口中多于一个抽象方法，只能使用匿名内部类，而不能使用Lambda表达式

- 实现原理不同
  - 匿名内部类：编译之后，产生一个单独的.class字节码文件
  - Lambda表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会在运行的时候动态生成

### 31.2 接口组成更新

**31.2.1接口组成更新概述【理解】**

- 常量

  public static final

- 抽象方法

  public abstract

- 默认方法(Java 8)

- 静态方法(Java 8)

- 私有方法(Java 9)

**31.2.2接口中默认方法【应用】**

- 格式

  public default 返回值类型 方法名(参数列表) {   }

- 范例

  ```java
  public default void show3() { 
  }
  ```

- 注意事项

  - 默认方法不是抽象方法，所以不强制被重写。但是可以被重写，重写的时候去掉default关键字

  - public可以省略，default不能省略

**31.2.3接口中静态方法【应用】**

- 格式

  public static 返回值类型 方法名(参数列表) {   }

- 范例

  ```java
  public static void show() {
  }
  ```

- 注意事项

  - 静态方法只能通过接口名调用，不能通过实现类名或者对象名调用

  - public可以省略，static不能省略

**31.2.4接口中私有方法【应用】**

- 私有方法产生原因

  Java 9中新增了带方法体的私有方法，这其实在Java 8中就埋下了伏笔：Java 8允许在接口中定义带方法体的默认方法和静态方法。这样可能就会引发一个问题：当两个默认方法或者静态方法中包含一段相同的代码实现时，程序必然考虑将这段实现代码抽取成一个共性方法，而这个共性方法是不需要让别人使用的，因此用私有给隐藏起来，这就是Java 9增加私有方法的必然性

- 定义格式

  - 格式1

    private 返回值类型 方法名(参数列表) {   }

  - 范例1

    ```java
    private void show() {  
    }
    ```

  - 格式2

    private static 返回值类型 方法名(参数列表) {   }

  - 范例2

    ```java
    private static void method() {  
    }
    ```

- 注意事项

  - 默认方法可以调用私有的静态方法和非静态方法
  - 静态方法只能调用私有的静态方法

### 31.3 方法引用

**31.3.1体验方法引用【理解】**

- 方法引用的出现原因

  在使用Lambda表达式的时候，我们实际上传递进去的代码就是一种解决方案：拿参数做操作

  那么考虑一种情况：如果我们在Lambda中所指定的操作方案，已经有地方存在相同方案，那是否还有必要再写重复逻辑呢？答案肯定是没有必要

  那我们又是如何使用已经存在的方案的呢？

  这就是我们要讲解的方法引用，我们是通过方法引用来使用已经存在的方案

- 代码演示

  ```java
  public interface Printable {
      void printString(String s);
  }
  
  public class PrintableDemo {
      public static void main(String[] args) {
          //在主方法中调用usePrintable方法
  //        usePrintable((String s) -> {
  //            System.out.println(s);
  //        });
  	    //Lambda简化写法
          usePrintable(s -> System.out.println(s));
  
          //方法引用
          usePrintable(System.out::println);
  
      }
  
      private static void usePrintable(Printable p) {
          p.printString("爱生活爱Java");
      }
  }
  
  ```

**31.3.2方法引用符【理解】**

- 方法引用符

  ::  该符号为引用运算符，而它所在的表达式被称为方法引用

- 推导与省略

  - 如果使用Lambda，那么根据“可推导就是可省略”的原则，无需指定参数类型，也无需指定的重载形式，它们都将被自动推导
  - 如果使用方法引用，也是同样可以根据上下文进行推导
  - 方法引用是Lambda的孪生兄弟

**31.3.3引用类方法【应用】**

​	引用类方法，其实就是引用类的静态方法

- 格式

  类名::静态方法

- 范例

  Integer::parseInt

  Integer类的方法：public static int parseInt(String s) 将此String转换为int类型数据

- 练习描述

  - 定义一个接口(Converter)，里面定义一个抽象方法 int convert(String s);

  - 定义一个测试类(ConverterDemo)，在测试类中提供两个方法

    - 一个方法是：useConverter(Converter c)

    - 一个方法是主方法，在主方法中调用useConverter方法

- 代码演示

  ```java
  public interface Converter {
      int convert(String s);
  }
  
  public class ConverterDemo {
      public static void main(String[] args) {
  
  		//Lambda写法
          useConverter(s -> Integer.parseInt(s));
  
          //引用类方法
          useConverter(Integer::parseInt);
  
      }
  
      private static void useConverter(Converter c) {
          int number = c.convert("666");
          System.out.println(number);
      }
  }
  ```

- 使用说明

  Lambda表达式被类方法替代的时候，它的形式参数全部传递给静态方法作为参数

**31.3.4引用对象的实例方法【应用】**

​	引用对象的实例方法，其实就引用类中的成员方法

- 格式

  对象::成员方法

- 范例

  "HelloWorld"::toUpperCase

    String类中的方法：public String toUpperCase() 将此String所有字符转换为大写

- 练习描述

  - 定义一个类(PrintString)，里面定义一个方法

    public void printUpper(String s)：把字符串参数变成大写的数据，然后在控制台输出

  - 定义一个接口(Printer)，里面定义一个抽象方法

    void printUpperCase(String s)

  - 定义一个测试类(PrinterDemo)，在测试类中提供两个方法

    - 一个方法是：usePrinter(Printer p)
    - 一个方法是主方法，在主方法中调用usePrinter方法

- 代码演示

  ```java
  public class PrintString {
      //把字符串参数变成大写的数据，然后在控制台输出
      public void printUpper(String s) {
          String result = s.toUpperCase();
          System.out.println(result);
      }
  }
  
  public interface Printer {
      void printUpperCase(String s);
  }
  
  public class PrinterDemo {
      public static void main(String[] args) {
  
  		//Lambda简化写法
          usePrinter(s -> System.out.println(s.toUpperCase()));
  
          //引用对象的实例方法
          PrintString ps = new PrintString();
          usePrinter(ps::printUpper);
  
      }
  
      private static void usePrinter(Printer p) {
          p.printUpperCase("HelloWorld");
      }
  }
  
  ```

- 使用说明

  Lambda表达式被对象的实例方法替代的时候，它的形式参数全部传递给该方法作为参数

**31.3.5引用类的实例方法【应用】**

​	引用类的实例方法，其实就是引用类中的成员方法

- 格式

  类名::成员方法

- 范例

  String::substring

  public String substring(int beginIndex,int endIndex) 

  从beginIndex开始到endIndex结束，截取字符串。返回一个子串，子串的长度为endIndex-beginIndex

- 练习描述

  - 定义一个接口(MyString)，里面定义一个抽象方法：

    String mySubString(String s,int x,int y);

  - 定义一个测试类(MyStringDemo)，在测试类中提供两个方法

    - 一个方法是：useMyString(MyString my)

    - 一个方法是主方法，在主方法中调用useMyString方法

- 代码演示

  ```java
  public interface MyString {
      String mySubString(String s,int x,int y);
  }
  
  public class MyStringDemo {
      public static void main(String[] args) {
  		//Lambda简化写法
          useMyString((s,x,y) -> s.substring(x,y));
  
          //引用类的实例方法
          useMyString(String::substring);
  
      }
  
      private static void useMyString(MyString my) {
          String s = my.mySubString("HelloWorld", 2, 5);
          System.out.println(s);
      }
  }
  ```

- 使用说明

  ​    Lambda表达式被类的实例方法替代的时候
  ​    第一个参数作为调用者
  ​    后面的参数全部传递给该方法作为参数

**31.3.6引用构造器【应用】**

​	引用构造器，其实就是引用构造方法

- l格式

  类名::new

- 范例

  Student::new

- 练习描述

  - 定义一个类(Student)，里面有两个成员变量(name,age)

    并提供无参构造方法和带参构造方法，以及成员变量对应的get和set方法

  - 定义一个接口(StudentBuilder)，里面定义一个抽象方法

    Student build(String name,int age);

  - 定义一个测试类(StudentDemo)，在测试类中提供两个方法

    - 一个方法是：useStudentBuilder(StudentBuilder s)

    - 一个方法是主方法，在主方法中调用useStudentBuilder方法

- 代码演示

  ```java
  public class Student {
      private String name;
      private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  }
  
  public interface StudentBuilder {
      Student build(String name,int age);
  }
  
  public class StudentDemo {
      public static void main(String[] args) {
  
  		//Lambda简化写法
          useStudentBuilder((name,age) -> new Student(name,age));
  
          //引用构造器
          useStudentBuilder(Student::new);
  
      }
  
      private static void useStudentBuilder(StudentBuilder sb) {
          Student s = sb.build("林青霞", 30);
          System.out.println(s.getName() + "," + s.getAge());
      }
  }
  ```

- 使用说明

  Lambda表达式被构造器替代的时候，它的形式参数全部传递给构造器作为参数

### 31.4 函数式接口

**31.4.1函数式接口概述【理解】**

- 概念

  有且仅有一个抽象方法的接口

- 如何检测一个接口是不是函数式接口

  @FunctionalInterface

  放在接口定义的上方：如果接口是函数式接口，编译通过；如果不是，编译失败

- 注意事项

  我们自己定义函数式接口的时候，@FunctionalInterface是可选的，就算我不写这个注解，只要保证满足函数式接口定义的条件，也照样是函数式接口。但是，建议加上该注解

**31.4.2函数式接口作为方法的参数【应用】**

- 需求描述

  定义一个类(RunnableDemo)，在类中提供两个方法

  一个方法是：startThread(Runnable r)   方法参数Runnable是一个函数式接口

  一个方法是主方法，在主方法中调用startThread方法

- 代码演示

  ```java
  public class RunnableDemo {
      public static void main(String[] args) {
          //在主方法中调用startThread方法
  
          //匿名内部类的方式
          startThread(new Runnable() {
              @Override
              public void run() {
                  System.out.println(Thread.currentThread().getName() + "线程启动了");
              }
          });
          
  		//Lambda方式
          startThread(() -> System.out.println(Thread.currentThread().getName() + "线程启动了"));
  
      }
  
      private static void startThread(Runnable r) {
          new Thread(r).start();
      }
  }
  ```

**31.4.3函数式接口作为方法的返回值【应用】**

- 需求描述

  定义一个类(ComparatorDemo)，在类中提供两个方法

  一个方法是：Comparator<String> getComparator()   方法返回值Comparator是一个函数式接口

  一个方法是主方法，在主方法中调用getComparator方法

- 代码演示

  ```java
  public class ComparatorDemo {
      public static void main(String[] args) {
          //定义集合，存储字符串元素
          ArrayList<String> array = new ArrayList<String>();
  
          array.add("cccc");
          array.add("aa");
          array.add("b");
          array.add("ddd");
  
          System.out.println("排序前：" + array);
  
          Collections.sort(array, getComparator());
  
          System.out.println("排序后：" + array);
  
      }
  
      private static Comparator<String> getComparator() {
          //匿名内部类的方式实现
  //        return new Comparator<String>() {
  //            @Override
  //            public int compare(String s1, String s2) {
  //                return s1.length()-s2.length();
  //            }
  //        };
          
  		//Lambda方式实现
          return (s1, s2) -> s1.length() - s2.length();
      }
  }
  ```

**31.4.4常用函数式接口之Supplier【应用】**

- Supplier接口

  Supplier<T>接口也被称为生产型接口，如果我们指定了接口的泛型是什么类型，那么接口中的get方法就会生产什么类型的数据供我们使用。

- 常用方法

  只有一个无参的方法

  | 方法名  |                       说明                       |
  | ------- | :----------------------------------------------: |
  | T get() | 按照某种实现逻辑(由Lambda表达式实现)返回一个数据 |

- 代码演示

  ```java
  public class SupplierDemo {
      public static void main(String[] args) {
  
          String s = getString(() -> "林青霞");
          System.out.println(s);
          
          Integer i = getInteger(() -> 30);
          System.out.println(i);
      }
  
      //定义一个方法，返回一个整数数据
      private static Integer getInteger(Supplier<Integer> sup) {
          return sup.get();
      }
  
      //定义一个方法，返回一个字符串数据
      private static String getString(Supplier<String> sup) {
          return sup.get();
      }
  
  }
  ```

**31.4.5Supplier接口练习之获取最大值【应用】**

- 案例需求

  定义一个类(SupplierTest)，在类中提供两个方法

  一个方法是：int getMax(Supplier<Integer> sup)   用于返回一个int数组中的最大值

  一个方法是主方法，在主方法中调用getMax方法

- 示例代码

  ```java
  public class SupplierTest {
      public static void main(String[] args) {
          //定义一个int数组
          int[] arr = {19, 50, 28, 37, 46};
  
          int maxValue = getMax(()-> {
             int max = arr[0];
  
             for(int i=1; i<arr.length; i++) {
                 if(arr[i] > max) {
                     max = arr[i];
                 }
             }
  
             return max;
          });
  
          System.out.println(maxValue);
  
      }
  
      //返回一个int数组中的最大值
      private static int getMax(Supplier<Integer> sup) {
          return sup.get();
      }
  }
  ```

**31.4.6常用函数式接口之Consumer【应用】**

- Consumer接口

  Consumer<T>接口也被称为消费型接口，它消费的数据的数据类型由泛型指定

- 常用方法

  Consumer<T>：包含两个方法

  | 方法名                                               | 说明                                                       |
  | ---------------------------------------------------- | ---------------------------------------------------------- |
  | void  accept(T t)                                    | 对给定的参数执行此操作                                     |
  | default Consumer<T>          andThen(Consumer after) | 返回一个组合的Consumer，依次执行此操作，然后执行 after操作 |

- 代码演示

  ```java
  public class ConsumerDemo {
      public static void main(String[] args) {
  		//操作一
          operatorString("林青霞", s -> System.out.println(s));
  		//操作二
          operatorString("林青霞", s -> System.out.println(new StringBuilder(s).reverse().toString()));
          
          System.out.println("--------");
  		//传入两个操作使用andThen完成
          operatorString("林青霞", s -> System.out.println(s), s -> System.out.println(new StringBuilder(s).reverse().toString()));
      }
  
      //定义一个方法，用不同的方式消费同一个字符串数据两次
      private static void operatorString(String name, Consumer<String> con1, Consumer<String> con2) {
  //        con1.accept(name);
  //        con2.accept(name);
          con1.andThen(con2).accept(name);
      }
  
      //定义一个方法，消费一个字符串数据
      private static void operatorString(String name, Consumer<String> con) {
          con.accept(name);
      }
  }
  ```

**31.4.7Consumer接口练习之按要求打印信息【应用】**

- 案例需求

  String[] strArray = {"林青霞,30", "张曼玉,35", "王祖贤,33"};

  字符串数组中有多条信息，请按照格式：“姓名：XX,年龄：XX"的格式将信息打印出来

  要求：

  把打印姓名的动作作为第一个Consumer接口的Lambda实例

  把打印年龄的动作作为第二个Consumer接口的Lambda实例

  将两个Consumer接口按照顺序组合到一起使用

- 示例代码

  ```java
  public class ConsumerTest {
      public static void main(String[] args) {
          String[] strArray = {"林青霞,30", "张曼玉,35", "王祖贤,33"};
  
          printInfo(strArray, str -> System.out.print("姓名：" + str.split(",")[0]),
                  str -> System.out.println(",年龄：" + Integer.parseInt(str.split(",")[1])));
      }
  
      private static void printInfo(String[] strArray, Consumer<String> con1, Consumer<String> con2) {
          for (String str : strArray) {
              con1.andThen(con2).accept(str);
          }
      }
  }
  ```

**31.4.8常用函数式接口之Predicate【应用】**

- Predicate接口

  Predicate<T>接口通常用于判断参数是否满足指定的条件

- 常用方法

  | 方法名                                    | 说明                                                         |
  | ----------------------------------------- | ------------------------------------------------------------ |
  | boolean test(T t)                         | 对给定的参数进行判断(判断逻辑由Lambda表达式实现)，返回一个布尔值 |
  | default Predicate<T> negate()             | 返回一个逻辑的否定，对应逻辑非                               |
  | default Predicate<T> and(Predicate other) | 返回一个组合判断，对应短路与                                 |
  | default Predicate<T> or(Predicate other)  | 返回一个组合判断，对应短路或                                 |

- 代码演示

  ```java
  public class PredicateDemo01 {
      public static void main(String[] args) {
          boolean b1 = checkString("hello", s -> s.length() > 8);
          System.out.println(b1);
  
          boolean b2 = checkString("helloworld",s -> s.length() > 8);
          System.out.println(b2);
  
      }
  
      //判断给定的字符串是否满足要求
      private static boolean checkString(String s, Predicate<String> pre) {
  //        return !pre.test(s);
          return pre.negate().test(s);
      }
  }
  
  public class PredicateDemo02 {
      public static void main(String[] args) {
          boolean b1 = checkString("hello", s -> s.length() > 8);
          System.out.println(b1);
          boolean b2 = checkString("helloworld", s -> s.length() > 8);
          System.out.println(b2);
  
          boolean b3 = checkString("hello",s -> s.length() > 8, s -> s.length() < 15);
          System.out.println(b3);
  
          boolean b4 = checkString("helloworld",s -> s.length() > 8, s -> s.length() < 15);
          System.out.println(b4);
      }
  
      //同一个字符串给出两个不同的判断条件，最后把这两个判断的结果做逻辑与运算的结果作为最终的结果
      private static boolean checkString(String s, Predicate<String> pre1, Predicate<String> pre2) {
          return pre1.or(pre2).test(s);
      }
  
      //判断给定的字符串是否满足要求
      private static boolean checkString(String s, Predicate<String> pre) {
          return pre.test(s);
      }
  }
  ```

**31.4.9Predicate接口练习之筛选满足条件数据【应用】**

- 练习描述

  - String[] strArray = {"林青霞,30", "柳岩,34", "张曼玉,35", "貂蝉,31", "王祖贤,33"};

  - 字符串数组中有多条信息，请通过Predicate接口的拼装将符合要求的字符串筛选到集合ArrayList中，并遍历ArrayList集合

  - 同时满足如下要求：姓名长度大于2；年龄大于33

- 分析

  - 有两个判断条件,所以需要使用两个Predicate接口,对条件进行判断

  - 必须同时满足两个条件,所以可以使用and方法连接两个判断条件

- 示例代码

  ```java
  public class PredicateTest {
      public static void main(String[] args) {
          String[] strArray = {"林青霞,30", "柳岩,34", "张曼玉,35", "貂蝉,31", "王祖贤,33"};
  
          ArrayList<String> array = myFilter(strArray, s -> s.split(",")[0].length() > 2,
                  s -> Integer.parseInt(s.split(",")[1]) > 33);
  
          for (String str : array) {
              System.out.println(str);
          }
      }
  
      //通过Predicate接口的拼装将符合要求的字符串筛选到集合ArrayList中
      private static ArrayList<String> myFilter(String[] strArray, Predicate<String> pre1, Predicate<String> pre2) {
          //定义一个集合
          ArrayList<String> array = new ArrayList<String>();
  
          //遍历数组
          for (String str : strArray) {
              if (pre1.and(pre2).test(str)) {
                  array.add(str);
              }
          }
  
          return array;
      }
  }
  ```

**31.4.10常用函数式接口之Function【应用】**

- Function接口

  Function<T,R>接口通常用于对参数进行处理，转换(处理逻辑由Lambda表达式实现)，然后返回一个新的值

- 常用方法

  | 方法名                                       | 说明                                                         |
  | -------------------------------------------- | ------------------------------------------------------------ |
  | R  apply(T t)                                | 将此函数应用于给定的参数                                     |
  | default <V> Function andThen(Function after) | 返回一个组合函数，首先将该函数应用于输入，然后将after函数应用于结果 |

- 代码演示

  ```java
  public class FunctionDemo {
      public static void main(String[] args) {
  		//操作一
          convert("100",s -> Integer.parseInt(s));
  		//操作二
          convert(100,i -> String.valueOf(i + 566));
  		
          //使用andThen的方式连续执行两个操作
          convert("100", s -> Integer.parseInt(s), i -> String.valueOf(i + 566));
      }
  
      //定义一个方法，把一个字符串转换int类型，在控制台输出
      private static void convert(String s, Function<String,Integer> fun) {
  //        Integer i = fun.apply(s);
          int i = fun.apply(s);
          System.out.println(i);
      }
  
  
      //定义一个方法，把一个int类型的数据加上一个整数之后，转为字符串在控制台输出
      private static void convert(int i, Function<Integer,String> fun) {
          String s = fun.apply(i);
          System.out.println(s);
      }
  
  
      //定义一个方法，把一个字符串转换int类型，把int类型的数据加上一个整数之后，转为字符串在控制台输出
      private static void convert(String s, Function<String,Integer> fun1, Function<Integer,String> fun2) {
  
          String ss = fun1.andThen(fun2).apply(s);
          System.out.println(ss);
      }
  
  }
  ```

**31.4.11Function接口练习之按照指定要求操作数据【应用】**

- 练习描述

  - String s = "林青霞,30";

  - 请按照我指定的要求进行操作：

    1:将字符串截取得到数字年龄部分   

    2:将上一步的年龄字符串转换成为int类型的数据

    3:将上一步的int数据加70，得到一个int结果，在控制台输出

  - 请通过Function接口来实现函数拼接

- 示例代码

  ```java
  public class FunctionTest {
      public static void main(String[] args) {
          String s = "林青霞,30";
          convert(s, ss -> ss.split(",")[1], Integer::parseInt, i -> i + 70);
      }
  
      private static void convert(String s, Function<String, String> fun1, Function<String, Integer> fun2, Function<Integer, Integer> fun3) {
          int i = fun1.andThen(fun2).andThen(fun3).apply(s);
          System.out.println(i);
      }
  }
  ```

### 31.5 Strem流

**31.5.1体验Stream流【理解】**

- 案例需求

  按照下面的要求完成集合的创建和遍历

  - 创建一个集合，存储多个字符串元素
  - 把集合中所有以"张"开头的元素存储到一个新的集合
  - 把"张"开头的集合中的长度为3的元素存储到一个新的集合
  - 遍历上一步得到的集合

- 原始方式示例代码

  ```java
  public class StreamDemo {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //把集合中所有以"张"开头的元素存储到一个新的集合
          ArrayList<String> zhangList = new ArrayList<String>();
  
          for(String s : list) {
              if(s.startsWith("张")) {
                  zhangList.add(s);
              }
          }
  
  //        System.out.println(zhangList);
  
          //把"张"开头的集合中的长度为3的元素存储到一个新的集合
          ArrayList<String> threeList = new ArrayList<String>();
  
          for(String s : zhangList) {
              if(s.length() == 3) {
                  threeList.add(s);
              }
          }
  
  //        System.out.println(threeList);
  
          //遍历上一步得到的集合
          for(String s : threeList) {
              System.out.println(s);
          }
          System.out.println("--------");
  
          //Stream流来改进
  //        list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(s -> System.out.println(s));
          list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(System.out::println);
      }
  }
  ```

- 使用Stream流示例代码

  ```java
  public class StreamDemo {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //Stream流来改进
          list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(System.out::println);
      }
  }
  ```

- Stream流的好处

  - 直接阅读代码的字面意思即可完美展示无关逻辑方式的语义：获取流、过滤姓张、过滤长度为3、逐一打印

  - Stream流把真正的函数式编程风格引入到Java中

**31.5.2Stream流的常见生成方式【应用】**

- Stream流的思想

  ![Stream流思想](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/Stream%E6%B5%81%E6%80%9D%E6%83%B3.jpg)

- 生成Stream流的方式

  - Collection体系集合

    使用默认方法stream()生成流， default Stream<E> stream()

  - Map体系集合

    把Map转成Set集合，间接的生成流

  - 数组

    通过Stream接口的静态方法of(T... values)生成流

- 代码演示

  ```java
  public class StreamDemo {
      public static void main(String[] args) {
          //Collection体系的集合可以使用默认方法stream()生成流
          List<String> list = new ArrayList<String>();
          Stream<String> listStream = list.stream();
  
          Set<String> set = new HashSet<String>();
          Stream<String> setStream = set.stream();
  
          //Map体系的集合间接的生成流
          Map<String,Integer> map = new HashMap<String, Integer>();
          Stream<String> keyStream = map.keySet().stream();
          Stream<Integer> valueStream = map.values().stream();
          Stream<Map.Entry<String, Integer>> entryStream = map.entrySet().stream();
  
          //数组可以通过Stream接口的静态方法of(T... values)生成流
          String[] strArray = {"hello","world","java"};
          Stream<String> strArrayStream = Stream.of(strArray);
          Stream<String> strArrayStream2 = Stream.of("hello", "world", "java");
          Stream<Integer> intStream = Stream.of(10, 20, 30);
      }
  }
  ```

**31.5.3Stream流中间操作方法【应用】**

- 概念

  中间操作的意思是，执行完此方法之后，Stream流依然可以继续执行其他操作。

- 常见方法

  | 方法名                                          | 说明                                                       |
  | ----------------------------------------------- | ---------------------------------------------------------- |
  | Stream<T> filter(Predicate predicate)           | 用于对流中的数据进行过滤                                   |
  | Stream<T> limit(long maxSize)                   | 返回此流中的元素组成的流，截取前指定参数个数的数据         |
  | Stream<T> skip(long n)                          | 跳过指定参数个数的数据，返回由该流的剩余元素组成的流       |
  | static <T> Stream<T> concat(Stream a, Stream b) | 合并a和b两个流为一个流                                     |
  | Stream<T> distinct()                            | 返回由该流的不同元素（根据Object.equals(Object) ）组成的流 |
  | Stream<T> sorted()                              | 返回由此流的元素组成的流，根据自然顺序排序                 |
  | Stream<T> sorted(Comparator comparator)         | 返回由该流的元素组成的流，根据提供的Comparator进行排序     |
  | <R> Stream<R> map(Function mapper)              | 返回由给定函数应用于此流的元素的结果组成的流               |
  | IntStream mapToInt(ToIntFunction mapper)        | 返回一个IntStream其中包含将给定函数应用于此流的元素的结果  |

- filter代码演示

  ```java
  public class StreamDemo01 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //需求1：把list集合中以张开头的元素在控制台输出
          list.stream().filter(s -> s.startsWith("张")).forEach(System.out::println);
          System.out.println("--------");
  
          //需求2：把list集合中长度为3的元素在控制台输出
          list.stream().filter(s -> s.length() == 3).forEach(System.out::println);
          System.out.println("--------");
  
          //需求3：把list集合中以张开头的，长度为3的元素在控制台输出
          list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(System.out::println);
      }
  }
  ```

- limit&skip代码演示

  ```java
  public class StreamDemo02 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //需求1：取前3个数据在控制台输出
          list.stream().limit(3).forEach(System.out::println);
          System.out.println("--------");
  
          //需求2：跳过3个元素，把剩下的元素在控制台输出
          list.stream().skip(3).forEach(System.out::println);
          System.out.println("--------");
  
          //需求3：跳过2个元素，把剩下的元素中前2个在控制台输出
          list.stream().skip(2).limit(2).forEach(System.out::println);
      }
  }
  ```

- concat&distinct代码演示

  ```java
  public class StreamDemo03 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //需求1：取前4个数据组成一个流
          Stream<String> s1 = list.stream().limit(4);
  
          //需求2：跳过2个数据组成一个流
          Stream<String> s2 = list.stream().skip(2);
  
          //需求3：合并需求1和需求2得到的流，并把结果在控制台输出
  //        Stream.concat(s1,s2).forEach(System.out::println);
  
          //需求4：合并需求1和需求2得到的流，并把结果在控制台输出，要求字符串元素不能重复
          Stream.concat(s1,s2).distinct().forEach(System.out::println);
      }
  }
  ```

- sorted代码演示

  ```java
  public class StreamDemo04 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("linqingxia");
          list.add("zhangmanyu");
          list.add("wangzuxian");
          list.add("liuyan");
          list.add("zhangmin");
          list.add("zhangwuji");
  
          //需求1：按照字母顺序把数据在控制台输出
  //        list.stream().sorted().forEach(System.out::println);
  
          //需求2：按照字符串长度把数据在控制台输出
          list.stream().sorted((s1,s2) -> {
              int num = s1.length()-s2.length();
              int num2 = num==0?s1.compareTo(s2):num;
              return num2;
          }).forEach(System.out::println);
      }
  }
  ```

- map&mapToInt代码演示

  ```java
  public class StreamDemo05 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("10");
          list.add("20");
          list.add("30");
          list.add("40");
          list.add("50");
  
          //需求：将集合中的字符串数据转换为整数之后在控制台输出
  //        list.stream().map(s -> Integer.parseInt(s)).forEach(System.out::println);
  //        list.stream().map(Integer::parseInt).forEach(System.out::println);
  //        list.stream().mapToInt(Integer::parseInt).forEach(System.out::println);
  
          //int sum() 返回此流中元素的总和
          int result = list.stream().mapToInt(Integer::parseInt).sum();
          System.out.println(result);
      }
  }
  ```

**31.5.4Stream流终结操作方法【应用】**

- 概念

  终结操作的意思是，执行完此方法之后，Stream流将不能再执行其他操作。

- 常见方法

  | 方法名                        | 说明                     |
  | ----------------------------- | ------------------------ |
  | void forEach(Consumer action) | 对此流的每个元素执行操作 |
  | long count()                  | 返回此流中的元素数       |

- 代码演示

  ```java
  public class StreamDemo {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //需求1：把集合中的元素在控制台输出
  //        list.stream().forEach(System.out::println);
  
          //需求2：统计集合中有几个以张开头的元素，并把统计结果在控制台输出
          long count = list.stream().filter(s -> s.startsWith("张")).count();
          System.out.println(count);
      }
  }
  ```

**31.5.5Stream流综合练习【应用】**

- 案例需求

  现在有两个ArrayList集合，分别存储6名男演员名称和6名女演员名称，要求完成如下的操作

  - 男演员只要名字为3个字的前三人

  - 女演员只要姓林的，并且不要第一个

  - 把过滤后的男演员姓名和女演员姓名合并到一起

  - 把上一步操作后的元素作为构造方法的参数创建演员对象,遍历数据

  演员类Actor已经提供，里面有一个成员变量，一个带参构造方法，以及成员变量对应的get/set方法

- 代码实现

  ```java
  public class Actor {
      private String name;
  
      public Actor(String name) {
          this.name = name;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  }
  
  
  public class StreamTest {
      public static void main(String[] args) {
          //创建集合
          ArrayList<String> manList = new ArrayList<String>();
          manList.add("周润发");
          manList.add("成龙");
          manList.add("刘德华");
          manList.add("吴京");
          manList.add("周星驰");
          manList.add("李连杰");
  
  
          ArrayList<String> womanList = new ArrayList<String>();
          womanList.add("林心如");
          womanList.add("张曼玉");
          womanList.add("林青霞");
          womanList.add("柳岩");
          womanList.add("林志玲");
          womanList.add("王祖贤");
  
          /*
          //男演员只要名字为3个字的前三人
          Stream<String> manStream = manList.stream().filter(s -> s.length() == 3).limit(3);
  
          //女演员只要姓林的，并且不要第一个
          Stream<String> womanStream = womanList.stream().filter(s -> s.startsWith("林")).skip(1);
  
          //把过滤后的男演员姓名和女演员姓名合并到一起
          Stream<String> stream = Stream.concat(manStream, womanStream);
  
          //把上一步操作后的元素作为构造方法的参数创建演员对象,遍历数据
  //        stream.map(Actor::new).forEach(System.out::println);
          stream.map(Actor::new).forEach(p -> System.out.println(p.getName()));
          */
  
          Stream.concat(manList.stream().filter(s -> s.length() == 3).limit(3),
                  womanList.stream().filter(s -> s.startsWith("林")).skip(1)).map(Actor::new).
                  forEach(p -> System.out.println(p.getName()));
      }
  }
  ```

**31.5.6Stream流的收集操作【应用】**

- 概念

  对数据使用Stream流的方式操作完毕后，可以把流中的数据收集到集合中。

- 常用方法

  | 方法名                         | 说明               |
  | ------------------------------ | ------------------ |
  | R collect(Collector collector) | 把结果收集到集合中 |

- 工具类Collectors提供了具体的收集方式

  | 方法名                                                       | 说明                   |
  | ------------------------------------------------------------ | ---------------------- |
  | public static <T> Collector toList()                         | 把元素收集到List集合中 |
  | public static <T> Collector toSet()                          | 把元素收集到Set集合中  |
  | public static  Collector toMap(Function keyMapper,Function valueMapper) | 把元素收集到Map集合中  |

- 代码演示

  ```java
  public class CollectDemo {
      public static void main(String[] args) {
          //创建List集合对象
          List<String> list = new ArrayList<String>();
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
  
          /*
          //需求1：得到名字为3个字的流
          Stream<String> listStream = list.stream().filter(s -> s.length() == 3);
  
          //需求2：把使用Stream流操作完毕的数据收集到List集合中并遍历
          List<String> names = listStream.collect(Collectors.toList());
          for(String name : names) {
              System.out.println(name);
          }
          */
  
          //创建Set集合对象
          Set<Integer> set = new HashSet<Integer>();
          set.add(10);
          set.add(20);
          set.add(30);
          set.add(33);
          set.add(35);
  
          /*
          //需求3：得到年龄大于25的流
          Stream<Integer> setStream = set.stream().filter(age -> age > 25);
  
          //需求4：把使用Stream流操作完毕的数据收集到Set集合中并遍历
          Set<Integer> ages = setStream.collect(Collectors.toSet());
          for(Integer age : ages) {
              System.out.println(age);
          }
          */
          //定义一个字符串数组，每一个字符串数据由姓名数据和年龄数据组合而成
          String[] strArray = {"林青霞,30", "张曼玉,35", "王祖贤,33", "柳岩,25"};
  
          //需求5：得到字符串中年龄数据大于28的流
          Stream<String> arrayStream = Stream.of(strArray).filter(s -> Integer.parseInt(s.split(",")[1]) > 28);
  
          //需求6：把使用Stream流操作完毕的数据收集到Map集合中并遍历，字符串中的姓名作键，年龄作值
          Map<String, Integer> map = arrayStream.collect(Collectors.toMap(s -> s.split(",")[0], s -> Integer.parseInt(s.split(",")[1])));
  
          Set<String> keySet = map.keySet();
          for (String key : keySet) {
              Integer value = map.get(key);
              System.out.println(key + "," + value);
          }
      }
  }
  ```

## 32 类加载器

**32.1类加载【理解】**

- 类加载的描述
  - 当程序要使用某个类时，如果该类还未被加载到内存中，则系统会通过类的加载，类的连接，类的初始化这三个步骤来对类进行初始化。如果不出现意外情况，JVM将会连续完成这三个步骤，所以有时也把这三个步骤统称为类加载或者类初始化
- 类的加载
  - 就是指将class文件读入内存，并为之创建一个 java.lang.Class 对象
  - 任何类被使用时，系统都会为之建立一个 java.lang.Class 对象
- 类的连接
  - 验证阶段：用于检验被加载的类是否有正确的内部结构，并和其他类协调一致
  - 准备阶段：负责为类的类变量分配内存，并设置默认初始化值
  - 解析阶段：将类的二进制数据中的符号引用替换为直接引用
- 类的初始化
  - 在该阶段，主要就是对类变量进行初始化
- 类的初始化步骤
  - 假如类还未被加载和连接，则程序先加载并连接该类
  - 假如该类的直接父类还未被初始化，则先初始化其直接父类
  - 假如类中有初始化语句，则系统依次执行这些初始化语句
  - 注意：在执行第2个步骤的时候，系统对直接父类的初始化步骤也遵循初始化步骤1-3
- 类的初始化时机
  - 创建类的实例
  - 调用类的类方法
  - 访问类或者接口的类变量，或者为该类变量赋值
  - 使用反射方式来强制创建某个类或接口对应的java.lang.Class对象
  - 初始化某个类的子类
  - 直接使用java.exe命令来运行某个主类

**32.2类加载器【理解】**

**32.2.1类加载器的作用**

- 负责将.class文件加载到内存中，并为之生成对应的 java.lang.Class 对象。虽然我们不用过分关心类加载机制，但是了解这个机制我们就能更好的理解程序的运行！

**32.2.2JVM的类加载机制**

- 全盘负责：就是当一个类加载器负责加载某个Class时，该Class所依赖的和引用的其他Class也将由该类加载器负责载入，除非显示使用另外一个类加载器来载入
- 父类委托：就是当一个类加载器负责加载某个Class时，先让父类加载器试图加载该Class，只有在父类加载器无法加载该类时才尝试从自己的类路径中加载该类
- 缓存机制：保证所有加载过的Class都会被缓存，当程序需要使用某个Class对象时，类加载器先从缓存区中搜索该Class，只有当缓存区中不存在该Class对象时，系统才会读取该类对应的二进制数据，并将其转换成Class对象，存储到缓存区

**32.2.3Java中的内置类加载器**

- Bootstrap class loader：它是虚拟机的内置类加载器，通常表示为null ，并且没有父null
- Platform class loader：平台类加载器可以看到所有平台类 ，平台类包括由平台类加载器或其祖先定义的Java SE平台API，其实现类和JDK特定的运行时类
- System class loader：它也被称为应用程序类加载器 ，与平台类加载器不同。 系统类加载器通常用于定义应用程序类路径，模块路径和JDK特定工具上的类
- 类加载器的继承关系：System的父加载器为Platform，而Platform的父加载器为Bootstrap

**32.2.4ClassLoader 中的两个方法**

- 方法分类

  | 方法名                                    | 说明                       |
  | ----------------------------------------- | -------------------------- |
  | static ClassLoader getSystemClassLoader() | 返回用于委派的系统类加载器 |
  | ClassLoader getParent()                   | 返回父类加载器进行委派     |

- 示例代码

  ```java
  public class ClassLoaderDemo {
      public static void main(String[] args) {
          //static ClassLoader getSystemClassLoader()：返回用于委派的系统类加载器
          ClassLoader c = ClassLoader.getSystemClassLoader();
          System.out.println(c); //AppClassLoader
  
          //ClassLoader getParent()：返回父类加载器进行委派
          ClassLoader c2 = c.getParent();
          System.out.println(c2); //PlatformClassLoader
  
          ClassLoader c3 = c2.getParent();
          System.out.println(c3); //null
      }
  }
  ```

## 33 反射

**33.1反射的概述【理解】**

- 是指在运行时去获取一个类的变量和方法信息。然后通过获取到的信息来创建对象，调用方法的一种机制。由于这种动态性，可以极大的增强程序的灵活性，程序不用在编译期就完成确定，在运行期仍然可以扩展

**33.2获取Class类对象的三种方式【应用】**

**33.2.1三种方式分类**

- 类名.class属性
- 对象名.getClass()方法
- Class.forName(全类名)方法

**33.2.2示例代码**

```java
public class ReflectDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        //使用类的class属性来获取该类对应的Class对象
        Class<Student> c1 = Student.class;
        System.out.println(c1);

        Class<Student> c2 = Student.class;
        System.out.println(c1 == c2);
        System.out.println("--------");

        //调用对象的getClass()方法，返回该对象所属类对应的Class对象
        Student s = new Student();
        Class<? extends Student> c3 = s.getClass();
        System.out.println(c1 == c3);
        System.out.println("--------");

        //使用Class类中的静态方法forName(String className)
        Class<?> c4 = Class.forName("com.itheima_02.Student");
        System.out.println(c1 == c4);
    }
}
```

**33.3反射获取构造方法并使用【应用】**

**33.3.1Class类获取构造方法对象的方法**

- 方法分类

  | 方法名                                                       | 说明                           |
  | ------------------------------------------------------------ | ------------------------------ |
  | Constructor<?>[] getConstructors()                           | 返回所有公共构造方法对象的数组 |
  | Constructor<?>[] getDeclaredConstructors()                   | 返回所有构造方法对象的数组     |
  | Constructor<T> getConstructor(Class<?>... parameterTypes)    | 返回单个公共构造方法对象       |
  | Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes) | 返回单个构造方法对象           |

- 示例代码

  ```java
  public class ReflectDemo01 {
      public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
          //获取Class对象
          Class<?> c = Class.forName("com.itheima_02.Student");
  
          //Constructor<?>[] getConstructors() 返回一个包含 Constructor对象的数组， Constructor对象反映了由该 Class对象表示的类的所有公共构造函数
  //        Constructor<?>[] cons = c.getConstructors();
          //Constructor<?>[] getDeclaredConstructors() 返回反映由该 Class对象表示的类声明的所有构造函数的 Constructor对象的数组
          Constructor<?>[] cons = c.getDeclaredConstructors();
          for(Constructor con : cons) {
              System.out.println(con);
          }
          System.out.println("--------");
  
          //Constructor<T> getConstructor(Class<?>... parameterTypes) 返回一个 Constructor对象，该对象反映由该 Class对象表示的类的指定公共构造函数
          //Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes) 返回一个 Constructor对象，该对象反映由此 Class对象表示的类或接口的指定构造函数
          //参数：你要获取的构造方法的参数的个数和数据类型对应的字节码文件对象
  
          Constructor<?> con = c.getConstructor();
  
          //Constructor提供了一个类的单个构造函数的信息和访问权限
          //T newInstance(Object... initargs) 使用由此 Constructor对象表示的构造函数，使用指定的初始化参数来创建和初始化构造函数的声明类的新实例
          Object obj = con.newInstance();
          System.out.println(obj);
  
  //        Student s = new Student();
  //        System.out.println(s);
      }
  }
  ```

**33.3.2Constructor类用于创建对象的方法**

| 方法名                           | 说明                       |
| -------------------------------- | -------------------------- |
| T newInstance(Object...initargs) | 根据指定的构造方法创建对象 |

**33.4反射获取构造方法并使用练习1【应用】**

- 案例需求

  - 通过反射获取公共的构造方法并创建对象

- 代码实现

  - 学生类

    ```java
    public class Student {
        //成员变量：一个私有，一个默认，一个公共
        private String name;
        int age;
        public String address;
    
        //构造方法：一个私有，一个默认，两个公共
        public Student() {
        }
    
        private Student(String name) {
            this.name = name;
        }
    
        Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public Student(String name, int age, String address) {
            this.name = name;
            this.age = age;
            this.address = address;
        }
    
        //成员方法：一个私有，四个公共
        private void function() {
            System.out.println("function");
        }
    
        public void method1() {
            System.out.println("method");
        }
    
        public void method2(String s) {
            System.out.println("method:" + s);
        }
    
        public String method3(String s, int i) {
            return s + "," + i;
        }
    
        @Override
        public String toString() {
            return "Student{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    ", address='" + address + '\'' +
                    '}';
        }
    }
    ```

  - 测试类

    ```java
    public class ReflectDemo02 {
        public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
            //获取Class对象
            Class<?> c = Class.forName("com.itheima_02.Student");
    
            //public Student(String name, int age, String address)
            //Constructor<T> getConstructor(Class<?>... parameterTypes)
            Constructor<?> con = c.getConstructor(String.class, int.class, String.class);
            //基本数据类型也可以通过.class得到对应的Class类型
    
            //T newInstance(Object... initargs)
            Object obj = con.newInstance("林青霞", 30, "西安");
            System.out.println(obj);
        }
    }
    ```

**33.5反射获取构造方法并使用练习2【应用】**

- 案例需求

  - 通过反射获取私有构造方法并创建对象

- 代码实现

  - 学生类：参见上方学生类

  - 测试类

    ```java
    public class ReflectDemo03 {
        public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
            //获取Class对象
            Class<?> c = Class.forName("com.itheima_02.Student");
    
            //private Student(String name)
            //Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes)
            Constructor<?> con = c.getDeclaredConstructor(String.class);
    
            //暴力反射
            //public void setAccessible(boolean flag):值为true，取消访问检查
            con.setAccessible(true);
    
            Object obj = con.newInstance("林青霞");
            System.out.println(obj);
        }
    }
    ```

**33.6反射获取成员变量并使用【应用】**

**33.6.1Class类获取成员变量对象的方法**

- 方法分类

  | 方法名                              | 说明                           |
  | ----------------------------------- | ------------------------------ |
  | Field[] getFields()                 | 返回所有公共成员变量对象的数组 |
  | Field[] getDeclaredFields()         | 返回所有成员变量对象的数组     |
  | Field getField(String name)         | 返回单个公共成员变量对象       |
  | Field getDeclaredField(String name) | 返回单个成员变量对象           |

- 示例代码

  ```java
  public class ReflectDemo01 {
      public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
          //获取Class对象
          Class<?> c = Class.forName("com.itheima_02.Student");
  
          //Field[] getFields() 返回一个包含 Field对象的数组， Field对象反映由该 Class对象表示的类或接口的所有可访问的公共字段
          //Field[] getDeclaredFields() 返回一个 Field对象的数组，反映了由该 Class对象表示的类或接口声明的所有字段
  //        Field[] fields = c.getFields();
          Field[] fields = c.getDeclaredFields();
          for(Field field : fields) {
              System.out.println(field);
          }
          System.out.println("--------");
  
          //Field getField(String name) 返回一个 Field对象，该对象反映由该 Class对象表示的类或接口的指定公共成员字段
          //Field getDeclaredField(String name) 返回一个 Field对象，该对象反映由该 Class对象表示的类或接口的指定声明字段
          Field addressField = c.getField("address");
  
          //获取无参构造方法创建对象
          Constructor<?> con = c.getConstructor();
          Object obj = con.newInstance();
  
  //        obj.addressField = "西安";
  
          //Field提供有关类或接口的单个字段的信息和动态访问
          //void set(Object obj, Object value) 将指定的对象参数中由此 Field对象表示的字段设置为指定的新值
          addressField.set(obj,"西安"); //给obj的成员变量addressField赋值为西安
  
          System.out.println(obj);
  
  
  
  //        Student s = new Student();
  //        s.address = "西安";
  //        System.out.println(s);
      }
  }
  ```

**33.6.2Field类用于给成员变量赋值的方法**

| 方法名                           | 说明                           |
| -------------------------------- | ------------------------------ |
| voidset(Object obj,Object value) | 给obj对象的成员变量赋值为value |

**33.7反射获取成员变量并使用练习【应用】**

- 案例需求

  - 通过反射获取成员变量并赋值

- 代码实现

  - 学生类：参见上方学生类

  - 测试类

    ```java
    public class ReflectDemo02 {
        public static void main(String[] args) throws Exception {
            //获取Class对象
            Class<?> c = Class.forName("com.itheima_02.Student");
    
            //Student s = new Student();
            Constructor<?> con = c.getConstructor();
            Object obj = con.newInstance();
            System.out.println(obj);
    
            //s.name = "林青霞";
    //        Field nameField = c.getField("name"); //NoSuchFieldException: name
            Field nameField = c.getDeclaredField("name");
            nameField.setAccessible(true);
            nameField.set(obj, "林青霞");
            System.out.println(obj);
    
            //s.age = 30;
            Field ageField = c.getDeclaredField("age");
            ageField.setAccessible(true);
            ageField.set(obj,30);
            System.out.println(obj);
    
            //s.address = "西安";
            Field addressField = c.getDeclaredField("address");
            addressField.setAccessible(true);
            addressField.set(obj,"西安");
            System.out.println(obj);
        }
    }
    ```

**33.8反射获取成员方法并使用【应用】**

**33.8.1Class类获取成员方法对象的方法**

- 方法分类

  | 方法名                                                       | 说明                                       |
  | ------------------------------------------------------------ | ------------------------------------------ |
  | Method[] getMethods()                                        | 返回所有公共成员方法对象的数组，包括继承的 |
  | Method[] getDeclaredMethods()                                | 返回所有成员方法对象的数组，不包括继承的   |
  | Method getMethod(String name, Class<?>... parameterTypes)    | 返回单个公共成员方法对象                   |
  | Method getDeclaredMethod(String name, Class<?>... parameterTypes) | 返回单个成员方法对象                       |

- 示例代码

  ```java
  public class ReflectDemo01 {
      public static void main(String[] args) throws Exception {
          //获取Class对象
          Class<?> c = Class.forName("com.itheima_02.Student");
  
          //Method[] getMethods() 返回一个包含 方法对象的数组， 方法对象反映由该 Class对象表示的类或接口的所有公共方法，包括由类或接口声明的对象以及从超类和超级接口继承的类
          //Method[] getDeclaredMethods() 返回一个包含 方法对象的数组， 方法对象反映由 Class对象表示的类或接口的所有声明方法，包括public，protected，default（package）访问和私有方法，但不包括继承方法
  //        Method[] methods = c.getMethods();
          Method[] methods = c.getDeclaredMethods();
          for(Method method : methods) {
              System.out.println(method);
          }
          System.out.println("--------");
  
          //Method getMethod(String name, Class<?>... parameterTypes) 返回一个 方法对象，该对象反映由该 Class对象表示的类或接口的指定公共成员方法
          //Method getDeclaredMethod(String name, Class<?>... parameterTypes) 返回一个 方法对象，它反映此表示的类或接口的指定声明的方法 Class对象
          //public void method1()
          Method m = c.getMethod("method1");
  
          //获取无参构造方法创建对象
          Constructor<?> con = c.getConstructor();
          Object obj = con.newInstance();
  
  //        obj.m();
  
          //在类或接口上提供有关单一方法的信息和访问权限
          //Object invoke(Object obj, Object... args) 在具有指定参数的指定对象上调用此 方法对象表示的基础方法
          //Object：返回值类型
          //obj：调用方法的对象
          //args：方法需要的参数
          m.invoke(obj);
  
  //        Student s = new Student();
  //        s.method1();
      }
  }
  ```

**33.8.2Method类用于执行方法的方法**

| 方法名                                  | 说明                                                 |
| --------------------------------------- | ---------------------------------------------------- |
| Objectinvoke(Object obj,Object... args) | 调用obj对象的成员方法，参数是args,返回值是Object类型 |

**33.9反射获取成员方法并使用练习【应用】**

- 案例需求

  - 通过反射获取成员方法并调用

- 代码实现

  - 学生类：参见上方学生类

  - 测试类

    ```java
    public class ReflectDemo02 {
        public static void main(String[] args) throws Exception {
            //获取Class对象
            Class<?> c = Class.forName("com.itheima_02.Student");
    
            //Student s = new Student();
            Constructor<?> con = c.getConstructor();
            Object obj = con.newInstance();
    
            //s.method1();
            Method m1 = c.getMethod("method1");
            m1.invoke(obj);
    
            //s.method2("林青霞");
            Method m2 = c.getMethod("method2", String.class);
            m2.invoke(obj,"林青霞");
    
    //        String ss = s.method3("林青霞",30);
    //        System.out.println(ss);
            Method m3 = c.getMethod("method3", String.class, int.class);
            Object o = m3.invoke(obj, "林青霞", 30);
            System.out.println(o);
    
            //s.function();
    //        Method m4 = c.getMethod("function"); //NoSuchMethodException: com.itheima_02.Student.function()
            Method m4 = c.getDeclaredMethod("function");
            m4.setAccessible(true);
            m4.invoke(obj);
        }
    }
    ```

**33.10反射的案例【应用】**

**33.10.1反射练习之越过泛型检查**

- 案例需求

  - 通过反射技术，向一个泛型为Integer的集合中添加一些字符串数据

- 代码实现

  ```java
  public class ReflectTest01 {
      public static void main(String[] args) throws Exception {
          //创建集合
          ArrayList<Integer> array = new ArrayList<Integer>();
  
  //        array.add(10);
  //        array.add(20);
  //        array.add("hello");
  
          Class<? extends ArrayList> c = array.getClass();
          Method m = c.getMethod("add", Object.class);
  
          m.invoke(array,"hello");
          m.invoke(array,"world");
          m.invoke(array,"java");
  
          System.out.println(array);
      }
  }
  ```

**33.10.2运行配置文件中指定类的指定方法**

- 案例需求

  - 通过反射运行配置文件中指定类的指定方法

- 代码实现

  ```java
  public class ReflectTest02 {
      public static void main(String[] args) throws Exception {
          //加载数据
          Properties prop = new Properties();
          FileReader fr = new FileReader("myReflect\\class.txt");
          prop.load(fr);
          fr.close();
  
          /*
              className=com.itheima_06.Student
              methodName=study
           */
          String className = prop.getProperty("className");
          String methodName = prop.getProperty("methodName");
  
          //通过反射来使用
          Class<?> c = Class.forName(className);//com.itheima_06.Student
  
          Constructor<?> con = c.getConstructor();
          Object obj = con.newInstance();
  
          Method m = c.getMethod(methodName);//study
          m.invoke(obj);
      }
  }
  ```

## 34 模块化

**34.1模块化概述【理解】**

Java语言随着这些年的发展已经成为了一门影响深远的编程语言，无数平台，系统都采用Java语言编写。但是，伴随着发展，Java也越来越庞大，逐渐发展成为一门“臃肿” 的语言。而且，无论是运行一个大型的软件系统，还是运行一个小的程序，即使程序只需要使用Java的部分核心功能， JVM也要加载整个JRE环境。
为了给Java“瘦身”，让Java实现轻量化，Java 9正式的推出了模块化系统。Java被拆分为N多个模块，并允许Java程序可以根据需要选择加载程序必须的Java模块，这样就可以让Java以轻量化的方式来运行

其实，Java 7的时候已经提出了模块化的概念，但由于其过于复杂，Java 7，Java 8都一直未能真正推出，直到Java 9才真正成熟起来。对于Java语言来说，模块化系统是一次真正的自我革新，这种革新使得“古老而庞大”的Java语言重新焕发年轻的活力

**34.2模块的基本使用【应用】**

1. 在项目中创建两个模块。一个是myOne,一个是myTwo

2. 在myOne模块中创建以下包和以下类，并在类中添加方法

   ![01](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/01-1677568372301.png)

   ![02](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/02-1677568388705.png)

3. 在myTwo模块中创建以下包和以下类，并在类中创建对象并使用

   ![03](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/03-1677568397541.png)

   ![04](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/04-1677568433972.png)

   

4. 在myOne模块中src目录下，创建module-info.java，并写入以下内容

   ![05](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/05-1677568452459.png)

5. 在myTwo模块中src目录下，创建module-info.java，并写入以下内容

   ![06](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/06-1677568462426.png)

**34.3模块服务的基本使用【应用】**

1. 在myOne模块中新建一个包，提供一个接口和两个实现类

   ![07](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/07-1677568468720.png)

   ![08](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/08.png)

   ![09](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/09.png)

2. 在myOne模块中修改module-info.java文件，添加以下内容

   ![10](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/10.png)

3. 在myTwo模块中新建一个测试类

   ![11](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/11.png)

   ![12](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/12.png)

4. 在myTwo模块中修改module-info.java文件，添加以下内容

   ![13](Java%E5%9F%BA%E7%A1%80%E4%B8%8E%E8%BF%9B%E9%98%B6.assets/13.png)

