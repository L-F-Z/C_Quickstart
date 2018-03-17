# C语言速成(For UCAS Robot Group)

By LFZ

# 第一章 编程基础

## 二进制和八进制的转换

二进制向八进制的转换是每三位二进制数转换为一位八进制数，运算的顺序是从低位向高位依次进行，高位不足三位用零补充。

## 二进制和十六进制的转换

二进制向十六进制转换时，四位转换成十六进制的一位，运算的顺序是从低位向高位依次进行，高位不足四位用零补。

# 第二章 C语言初探

## C语言的基本框架

```c
#include <stdio.h>
int main()
{
  puts("Hello world!");
  return 0; //程序运行正确一般返回0
}
```

`puts` 为输出字符串，注意语句符号都要为半角符号。
`//`和`/* */`为注释符

```c
#include <stdlib.h>
int main()
{
  system("pause");
}
```

上部代码块可使程序暂停。
一个程序有且只有一个`main()`函数

## C语言的转义字符

通过`puts`可以输出字符串，例如：
`puts("123abc");`
"123abc" 对应的ASCII码值的八进制分别是 61、62、63、141、142、143，上面的代码也可以写为： 
`puts("\61\62\63\141\142\143");`
在C语言中，所有的ASCII码都可以用反斜杠`\`加数字（默认是8进制）来表示，称为转义字符（Escape Character），因为`\`后面的字符都不是它原来的ASCII字符的意思了。
除了八进制，也可以用十六进制来表示。用十六进制表示时数字要以`x`开头。"123abc" 对应的ASCII码值的十六进制分别是 31、32、33、61、62、63，所以也可以写为： `puts("\x31\x32\x33\x61\x62\x63");`
==注意：只能使用八进制或十六进制，不能使用十进制。==

| 转义字符 |          意义          | ASCII |
| :--: | :------------------: | :---: |
|  \a  |       响铃(BEL)        |  007  |
|  \b  |  退格(BS)，将当前位置移到前一列   |  008  |
|  \f  |  换页(FF)，将当前位置移到下页开头  |  012  |
|  \n  | 换行(LF)，将当前位置移到下一行开头  |  010  |
|  \r  |  回车(CR)，将当前位置移到本行开头  |  013  |
|  \t  | 水平制表(HT)(跳到下一个TAB位置) |  009  |
|  \v  |       垂直制表(VT)       |  011  |

输出`\`和`"`的方法：`printf("\\ \")`

# 第三章 变量和数据类型

## 为变量赋值的方法

```c
int a;
a=66;
```

```c
int a=66
```

## 数据类型

`short` `int` `long` `unsigned short` `unsigned int` `unsigned long` `float` `double` `long double` `char`

## 在屏幕上输出各种类型的数据

```c
printf("Hello world!")
  
int abc=999;
printf("The Value of abc is %d\n",abc)
```

printf格式控制符的标准格式 `%[flags][width][.precision]type`

- `type`为输出格式  

  `%d`有符号十进制整数
  `%u`无符号十进制整数 
  `%o`无符号八进制整数 
  `%x`\ `%X`无符号十六进制整数 
  `%c`字符 
  `%s`字符串 
  `%f`浮点数 
  `%e`\ `%E` 指数形式 
  `%g`\ `%G`根据数值和有效位数自动选择`%f`或`%e`形式
  `%p` 指针十六进制显示 

- `flags`为标志字符 `-`左对齐 `+`输出符号 输出值为+时冠以空格，为负时冠以负号 `#`对数据添加前缀

- `width`为最小输出宽度，对于整数和小数默认右对齐，不足的宽度以空格补齐。若使用`%04d`则代表以`0`补齐4位

- `.precision`为输出精度，对于整数其实为最小输出宽度，但不足的宽度是以`0`补齐的；对于浮点数表示精度，不足的以0补齐

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int a1=20, a2=345, a3=700, a4=22;
    int b1=56720, b2=9999, b3=20098, b4=2;
    int c1=233, c2=205, c3=1, c4=6666;
    int d1=34, d2=0, d3=23, d4=23006783;
    printf("%-9d %-9d %-9d %-9d\n", a1, a2, a3, a4);
    printf("%-9d %-9d %-9d %-9d\n", b1, b2, b3, b4);
    printf("%-9d %-9d %-9d %-9d\n", c1, c2, c3, c4);
    printf("%-9d %-9d %-9d %-9d\n", d1, d2, d3, d4);
    system("pause");
    return 0;
}
```

```20        345       700       22
56720     9999      20098     2
233       205       1         6666
34        0         23        23006783
```

## C语言中的整数

获取某个数据类型的长度可以使用 sizeof 操作符 

```c
int a,b,a_length,b_length;
a_length=sizeof a; //或a_length=sizeof(a);
b_length=sizeof (int);
```

整数的前缀 八进制-`0` 十六进制-`0X`或`0x`
整数的后缀 长整形-`L`或`l` 无符号-`U`或`u`
输出`short`用`%hd`，输出`int`用`%d`，输出`long`用`%ld`，向下兼容

## C语言中的小数

输出`float`用`%f`，输出`double`用`%lf`
`%f`默认保留6位小数，不足用0补齐，超过则四舍五入截取
将整数赋给float变量会转换为小数

## C语言中的字符

`char`为字符类型，其值用`' '`单引号包围，而字符串的值用`" "`双引号包围
定义方法：

```c
char ch;//定义字符
char *str="Hello World!"
```

## C语言中的标识符

C语言规定，标识符只能由字母(A~Z, a~z)、数字(0~9)和下划线(_)组成，并且第一个字符必须是字母或下划线。
在标识符中，大小写是有区别的，例如BOOK和book 是两个不同的标识符。

## C语言中的数学运算

加`+`  减`-`  乘`*`  除`/`  取余`%` 自增`++`  自减`--

- ++ 在前面叫做前自增（例如 ++a）。前自增先进行自增操作，再进行其他操作。
- ++在后面叫做后自增（例如 a++）。后自增先进行其他操作，再进行自增操作。
- `%`计算两数取绝对值，直接取余数，然后加符号，只和被除数的符号一样

```c
#include <stdio.h>
int main()
{
  int a;
  a=8;
  printf("%d\n",++a);
  printf("%d\n",a++);
  printf("%d\n",--a);
  printf("%d\n",a--);
  return 0;
}
```

```c
9
9
9
9
```

## 数据类型的转换

```c
#include <stdio.h>
int main(){
   int sum = 17, count = 5;
   double mean;
   mean = (double) sum / count;
   printf("Value of mean : %f\n", mean);
   return 0;
}
```

运行结果：` Value of mean : 3.400000`
需要注意的是，类型转换运算符`( )`的优先级高于`/`，`(double) sum / count`会先将 sum 转换为 double 类型，然后再进行除法运算。如果写作`(double) (sum / count)`，那么运行结果就是 3.000000。
无论是强制转换或是自动转换，都只是为了本次运算的需要而对变量的数据长度进行的临时性转换，而不改变数据说明时对该变量定义的类型。请看下面的例子： 

```c
#include<stdio.h>
int main(){
    float f=5.75;
    printf("(int)f=%d, f=%f\n",(int)f, f);
    return 0;
}
```

运行结果： `(int)f=5, f=5.750000`

# 第四章 C语言输入输出

## 在显示器上输出数据

`putchar()`只能输出单个字符，输出结束不换行

```c
putchar('a');
putchar(7);
putchar('\x46');
```

`puts()`只能输出字符串，输出结束自动换行
`printf()`可输出多种格式

## 从键盘输入数据

`scanf()`可以输入多种类型的数据

```c
int a,b,c,d,e,f;
scanf("%d %d",&a,&b); //输入数据应为 36 42
scanf("%d,%d",&c,&d); //输入数据应为 36,42
scanf("%dand%d",&e,&f)//输入数据应为 36and42
```

`&`为取地址符，即获取变量在内存中的地址
`getchar()`为获取单个字符，按下回车后才可获取 `<stdio.h>`
`getche()`为获取单个字符，输入完成自动获取，有回显 `<conio.h>`
`getch()`为获取单个字符，输入完成自动获取，无回显 `<conio.h>`
`gets()`为获取字符串，会读取整行内容，包括空格
`scanf("%s")`可以获取字符串，但遇到空格就结束，读取内容一定不含空格

# 第五章 分支结构和循环结构

##  C语言关系运算符与逻辑运算符

`<`小于 
`<=`小于或等于 
`>`大于 
`>=`大于或等于 
`==` 等于 
`!=` 不等于
`&&` 与运算
`||` 或运算
`!` 非运算
运算结果为真，值为1 ；运算结果为假，值为0

## if-else语句

标准格式

```c
if(表达式)
	{语句块1}
else
	{语句块2};

if(表达式)
	{语句块};
```

若表达式非0则执行语句块1，否则执行语句块2
例程 判断输入字符的类别

```c
#include <stdio.h>
int main(){
    char c;
    printf("Input a character:");
    c=getchar();
    if(c<32)
        printf("This is a control character\n");
    else if(c>='0'&&c<='9')
        printf("This is a digit\n");
    else if(c>='A'&&c<='Z')
        printf("This is a capital letter\n");
    else if(c>='a'&&c<='z')
        printf("This is a small letter\n");
    else
        printf("This is an other character\n");
    return 0;
}
```

==`else`总是与它前面最近的`if`配对==

## switch语句

标准格式

```c
switch(表达式){
  case 常量表达式1:语句1; break;
  case 常量表达式2:语句2; break;
  case 常量表达式3:语句3; break;
  default:语句n; break;  //最后一句可以不加break
}
```

==若不加`switch`语句，程序会执行从满足条件的一句开始，以下的每一个语句==

## 条件运算符

标准格式

```c
表达式1?表达式2:表达式3
```

条件运算符为C语言中唯一一个三目运算符，通常用于赋值语句中，求值规则为：
如果表达式1的值为真，则以表达式2的值作为整个条件表达式的值，否则以表达式3的值作为整个条件表达式的值。
范例 将a与b中较大值赋给max

```c
max=(a>b)?a:b;
```

## while语句

标准格式

```c
while(表达式){
  语句块
};

do{
  语句块
}while(表达式);
```

## for语句

标准格式

```
for(表达式1;表达式2;表达式3){
  语句块
}
```

例程 求1到100之和

```c
#include <stdio.h>
int main(){
    int i, sum=0;
    for(i=1; i<=100; i++){
        sum+=i;
    }
    printf("%d\n",sum);
    return 0;
}
```

### 注意

表达式123均可以省略，但分号不可以省略
表达式1和3可以为用逗号分隔的多个语句
若三个表达式均省略，相当于`while(1)`语句

## goto语句

标准格式

```c
goto 标签;
...
标签:语句
```

范例 错误判断

```
if (do_something() == ERR) 
    goto error;            
if (do_something2() == ERR) 
    goto error;             
if (do_something3() == ERR) 
    goto error;             
if (do_something4() == ERR)   // 使用普通的平铺形式
    goto error;
error：return 1;
```

==退出当前函数用`return`，退出程序用`exit(0)`（需要`stdlib.h`）==

## C语言跳出循环

`break`关键字用于终止当前层循环以执行后面的代码。
`continue`关键字用于结束本层本次循环，直接跳到下一次循环。此语句只用于`while`和`for`循环中。

# 第六章 C语言数组

## 定义方式

`dataType arrayName[length][length]...`
初始化示例 `int a[4]={20,345,700,22}`
可以只给部分元素赋值。当`{}`中值得个数小于元素个数时，只给前面部分元素赋值，其余元素自动赋`0`/`0.0`/`\0`值
可以用 `char c[10]={0}`将所有元素赋值为`\0`
如果给全部元素赋值，在定义数组时可以不给出数组长度，如`int a[]={1,2,3,4,5}`
二维数组初始化方式`int a[3][2]={{1,2},{3,4},{5,6}}`，如对全部元素赋初值，则第一维的长度可以不给出。
 二维数组`a[3][4]`，可分解为三个一维数组，其数组名分别为：`a[0]`、`a[1]`、`a[2]`。对这三个一维数组不需另作说明即可使用。这三个一维数组都有4个元素，例如：一维数组`a[0]`的元素为`a[0][0]`，`a[0][1]`，`a[0][2]`，` a[0][3]`。必须强调的是，`a[0]`，`a[1]`，`a[2]`不能当作下标变量使用，它们是数组名，不是一个单纯的下标变量。

## 字符数组和字符串

赋值方法

```c
char a[20]={'c',' ','p','r','o','g','r','a','m'};
char b[]={'c',' ','p','r','o','g','r','a','m'};
char c[20]={"c program"};
char d[20]="c program";
char e[]={"c program"};
char f[]="c program";
```

编译器会自动在字符串末尾加入`\0`，所以数组长度应该至少比字符串长度大1

### 常用字符串函数 (`string.h`)

**`strlen`字符串长度函数** 获取字符串长度，不包括字符串结束标志`\0`，语法格式为`strlen(arrayName)`，返回值为一个整数
**`strcat` 字符串连接函数** 拼接两个字符串，语法格式为`strcat(arrayName1,arrayName2)`，函数删除`arrayName1`最后的`\0`标志并将`arrayName2`连接到`arrayName1`后面
**`strcpy` 字符串复制函数** 语法格式为`strcpy(arrayName1,arrayName2)`，即把 `arrayName2`中的字符串拷贝入`arrayName1`中，`arrayName1`中全部原内容会消失
**`strcmp` 字符串比较函数** 语法格式为 `strcpy(arrayName1,arrayName2)`，即从第一位开始比较两个字符串的字符`ASCII`码值大小，返回`-1`，`0`，`1`

字符串的输入

- `scanf()`通过格式控制符`%s`输入字符串，读到空格即停止

例程

```c
#include <stdio.h>
int main(){
    char str1[20], str2[20], str3[20];
    printf("Input string: ");
    scanf("%s", str1);
    scanf("%s", str2);
    scanf("%s", str3);
    printf("str1: %s\nstr2: %s\nstr3: %s\n", str1, str2, str3);
    return 0;
}
```

```c
Input string: Java Python C-Sharp↙
 str1: Java
 str2: Python
 str3: C-Sharp
```

第一个 scanf() 读取到 "Java" 后遇到空格，结束读取，将"Python C-Sharp" 留在缓冲区。第二个 scanf() 直接从缓冲区中读取，不会等待用户输入，读取到 "Python" 后遇到空格，结束读取，将 "C-Sharp" 留在缓冲区。第三个 scanf() 读取缓冲区中剩下的内容。
==C语言规定，数组名就代表了该数组的地址，数组名所代表的地址为第0个元素的地址==

- `gets()`获取包括空格的字符串，以回车作为输入结束的标志

  如果希望读取的字符串中不包含空格，那么使用 scanf() 函数；如果希望获取整行字符串，那么使用 gets() 函数，它能避免空格的截断。

# 第七章 C语言函数

## 自定义函数

无参函数的定义格式

```c
返回值类型 函数名(){
  函数体
  return 返回值;
}
```

函数体必须由括号包围，即使只有一个语句
无返回值时返回值类型为`void`，也无需`return`语句
函数一旦遇到` return` 语句就返回（停止执行），后面的所有语句都不会被执行到
有参函数的定义格式

```c
返回值类型 函数名(参数列表){
  函数体
  return 返回值;
}
```

参数列表中可以定义一个或多个参数，多个参数之间用逗号`,`分隔。参数列表中给出的参数可以在函数体中使用。
函数定义时给出的参数称为**形式参数**，简称形参；函数调用时给出的参数（传递的数据）称为**实际参数**，简称实参。函数调用时，将实参的值传递给形参，相当于一次赋值操作。
==实参和形参的类型、数目必须一致==
范例

```c
#include <stdio.h>
int max(int a, int b){
    if (a>b){
        return a;
    }else{
        return b;
    }
}
int main(){
    int num1, num2, maxVal;
    printf("Input two numbers: ");
    scanf("%d %d", &num1, &num2);
    maxVal = max(num1, num2);
    printf("The max number: %d\n", maxVal);
    return 0;
}
```

##  函数的参数与返回值

- 形参变量只有在函数被调用时才分配内存单元，在调用结束时，立刻释放所分配的内存单元。因此，形参只有在函数内部有效，不能在函数外部使用。

- 函数调用中发生的数据传送是单向的，只能把实参的值传送给形参，而不能把形参的值反向地传送给实参。 因此在函数调用过程中，形参的值发生改变，而实参中的值不会变化。

- 函数中可以有多个 `return` 语句，但每次调用只能有一个`return`语句被执行，所以只有一个返回值。 一旦遇到 `return` 语句，不管后面有没有代码，函数立即运行结束，将值返回。

- `main` 函数中定义的变量也是局部变量，只能在 `main` 函数中使用；同时，main 函数中也不能使用其它函数中定义的变量。`main` 函数也是一个函数，与其它函数地位平等。

- 可以在不同的函数中使用相同的变量名，它们代表不同的对象，分配不同的单元，互不干扰，也不会发生混淆。

- 一旦函数的返回值类型被定义为 `void`，就不能再接收它的值了。例如，下面的语句是错误的： 

  ```c
  void func(){
      printf("Hello world!\n");
  }
  int main(){
    int a=func();
    return 0;
  } 
  ```

## 函数声明和函数原型

C语言代码由上到下依次执行，函数定义要出现在函数调用之前。 但是，如果在函数调用前进行了函数声明，那么函数定义就可以出现在任何地方了，甚至是其他文件。
函数声明的一般形式为： `返回值类型  函数名( 类型 形参, 类型 形参… );`
或为： `返回值类型  函数名( 类型, 类型…);`

函数声明给出了函数名、返回值类型、参数列表（参数类型）等与该函数有关的信息，称为函数原型（Function Prototype）。 函数原型的作用是告诉编译器与该函数有关的信息，让编译器知道函数的存在，以及存在的形式，即使函数暂时没有定义，也不会出错。
范例：

```c
#include <stdio.h>
// 函数声明
long factorial(int n);  //也可以写作 long factorial(int);
long sum(long n);  //也可以写作 long sum(long);

int main(){
    printf("1!+2!+...+9!+10! = %ld\n", sum(10));
    return 0;
}
long factorial(int n){    //求阶乘
    int i;
    long result=1;
    for(i=1; i<=n; i++){
        result *= i;
    }
    return result;
}
long sum(long n){   // 求累加的和
    int i;
    long result = 0;
    for(i=1; i<=n; i++){
        //嵌套调用
        result += factorial(i);
    }
    return result;
}
```

## 全局变量

在所有函数外部定义的变量称为全局变量`Global Variable`，它的作用域是整个源程序。例如： 

```c
int a, b;  //外部变量
void f1(){
    // Code
}
float x,y;  //外部变量
int fz(){
    // Code
}
int main(){
    // Code
    return 0;
}
```

a、b、x、y 都是在函数外部定义的全局变量。x、y 定义在函数f1之后，在f1内无效。a、b定义在源程序最前面，因此在f1、f2及main内都有效。
==在同一个源文件中，如果全局变量与局部变量同名，那么在局部变量的作用范围内，外部变量被“屏蔽”，也就是它不起作用。==

# 第八章 预处理命令

## #include命令

```c
#include <stdio.h>      //从系统默认相关目录中查找
#include "myHeader.h"   //从源程序目录中查找
```

一个`#include`命令只能包含一个头文件，多个头文件需要多个`#include`命令。

## #define命令

```c
#define 宏名 字符串     //宏定义标准格式，行末无需分号
#define M (n*n+3*n)    //宏表达式注意加括号，避免逻辑错误
```

程序中所有宏名所在位置都会在编译时被所对应字符串取代
宏名在源程序中若用引号括起来，则预处理程序不对其作宏代换
宏定义必须写在函数之外，其作用域为宏定义命令起到源程序结束。如要终止其作用域可使用`#undef`命令。
应注意用宏定义表示数据类型和用`typedef`定义数据说明符的区别。宏定义只是简单的字符串代换，是在预处理完成的，而`typedef`是在编译时处理的，它不是作简单的代换，而是对类型说明符重新命名。被命名的标识符具有类型定义说明的功能。请看下面的例子： 

```c
#define PIN1 int *
typedef (int *) PIN2;
```

从形式上看这两者相似， 但在实际使用中却不相同。`PIN1 a,b;`在宏代换后变成：`int *a,b`;表示a是指向整型的指针变量，而b是整型变量。然而：`PIN2 a,b;`表示a、b都是指向整型的指针变量。因为`PIN2`是一个类型说明符。由这个例子可见，宏定义虽然也可表示数据类型， 但毕竟是作字符代换。在使用时要分外小心，以避出错。
==为了避免宏代换时发生错误，宏定义中的字符串应加括号，字符串中出现的形式参数两边也应加括号。==

## 带参宏定义

```c
#include <stdio.h>
#define SSSV(s1, s2, s3, v) s1=l*w; s2=l*h; s3=w*h; v=w*l*h;
int main(){
    int l=3, w=4, h=5, sa, sb, sc, vv;
    SSSV(sa, sb, sc, vv);
    printf("sa=%d\nsb=%d\nsc=%d\nvv=%d\n", sa, sb, sc, vv);
    return 0;
}
```

注意参数列表和宏名之间不能有空格

## 条件编译

- 格式一

  ```c
  #ifdef  标识符
       程序段1
  #else
       程序段2
  #endif
  ```

  它的功能是，如果标识符已被` #define` 命令定义过则对程序段1进行编译；否则对程序段2进行编译。如果没有程序段2（它为空），本格式中的`#else`可以没有
  范例

  ```c
  #include <stdio.h>
  #define WIN16 true    //可以定义为任何字符串或不定义
  int main(void){
      #ifdef WIN16
          printf("The value of sizeof(int) is 2.\n");
      #else
          printf("The value of sizeof(int) is 4.\n");
      #endif
      return 0;
  }
  ```

- 格式二

  ```c
  #ifndef 标识符
       程序段1 
   #else 
       程序段2 
   #endif
  ```

  与第一种形式的区别是将`ifdef`改为`ifndef`。它的功能是，如果标识符未被#define命令定义过则对程序段1进行编译，否则对程序段2进行编译。这与第一种形式的功能正相反。

- 格式三

  ```c
  #if 常量表达式
       程序段1
   #else 
       程序段2
   #endif
  ```

  它的功能是，如常量表达式的值为真（非0），则对程序段1 进行编译，否则对程序段2进行编译。因此可以使程序在不同条件下，完成不同的功能。

# 第九章 C语言指针

## 指针变量的定义与引用

`类型说明符 *变量名;`
`float *p1`
一个指针变量只能指向同类型的变量，如 p3 只能指向浮点变量，不能时而指向一个浮点变量，时而又指向一个字符变量。 
C语言用地址运算符`&`来获取变量的地址。其一般形式为：`&变量名`;

```c
//赋值方法一
int a=10;
int *p=&a;
//赋值方法二
int a=10;
int *p;
p=&a;
//赋值方法三
int a[5], *pa;
pa=a;   //或pa=&a[0]
//赋值方法四
char *pc;
pc="C Language";
//赋值方法五
char *pc="C Language";
//赋值方法六  把函数的入口地址赋予指向函数的指针变量
int (*pf)();
pf = func;  //func 为函数名
```

指针变量和一般变量一样，存放在它们之中的值是可以改变的，也就是说可以改变它们的指向。例如： 

```c
int i, j, *p1, *p2;
i = 'a';
j = 'b';
p1 = &i;
p2 = &j;
```

这时赋值表达式：`p2=p1;`就使`p2`与`p1`指向同一对象`i`，此时`*p2`就等价于`i`，而不是`j`
如果执行如下表达式：`*p2=*p1;`则表示把`p1`指向的内容赋给`p2`所指的区域，`j`的值变为`a`

## 指针变量作为函数参数

```c
#include <stdio.h>
void swap(int *p1, int *p2){ // 交换两个数
    int temp;  //临时变量
    temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main(){
    int a, b;
    int *pointer_1, *pointer_2;
    scanf("%d, %d",&a, &b);
    pointer_1 = &a;
    pointer_2 = &b;
    if(a<b){
        swap(pointer_1, pointer_2);
    }
    printf("\n%d,%d\n",a, b);
    return 0;
}
```

## 指针加减算数运算(针对数组)

```c
int a[5],*pa;
pa=a;  //pa指向数组a，也是指向a[0]
pa=pa+2;  //pa指向a[2]，即pa的值为&pa[2]
```

## 两个指针变量之间的运算

**两指针变量相减**  两指针变量相减所得之差是两个指针所指数组元素之间相差的元素个数。
**两指针变量进行关系运算指**  向同一数组的两指针变量进行关系运算可表示它们所指数组元素之间的关系。例如：
`pf1==pf2` 表示`pf1`和`pf2`指向同一数组元素；
`pf1>pf2` 表示`pf1`处于高地址位置；
`pf1<pf2` 表示`pf2`处于低地址位置。
指针变量还可以与0比较。设`p`为指针变量，则`p==0`表明`p`是空指针，它不指向任何变量；`p!=0`表示`p`不是空指针。
空指针是由对指针变量赋予0值而得到的。例如：

```c
#define NULL 0
int *p = NULL;
```

对指针变量赋0值和不赋值是不同的。指针变量未赋值时，值是随机的，是垃圾值，不能使用的，否则将造成意外错误。而指针变量赋0值后，则可以使用，只是它不指向具体的变量而已。

## 数组指针

如果指针变量p已指向数组中的一个元素，则p+1指向同一数组中的下一个元素。
如果`p`的初值为`&a[0]`，则：`p+i` 和 `a+i` 就是 `a[i]` 的地址，或者说它们指向`a`数组的第 `i` 个元素。
` *(p+i) `或 `*(a+i)` 就是 `p+i` 或 `a+i` 所指向的数组元素（的内容），即`a[i]`。例如，`*(p+5)` 或`*(a+5) `就是 `a[5]`。
指向数组的指针变量也可以带下标，如 `p[i]` 与 `*(p+i) `等价。
指针变量可以实现本身的值的改变。如`p++`是合法的；而`a++`是错误的。因为`a`是数组名，它是数组的首地址，是常量。
如果p当前指向a数组中的第i个元素，则：` *(p--)`相当于`a[i--]`；` *(++p)`相当于`a[++i]`；`*(--p)`相当于`a[--i]`。
用数组作函数参数时，形参数组和实参数组的长度可以不相同，因为在调用时，只传送首地址而不检查形参数组的长度。在函数形参表中，允许不给出形参数组的长度，例如可以写为：`void nzp(int a[])`；也可以用指针来代替：`void nzp(int *a)`

## 字符串指针

范例 输出字符串中n个字符后的所有字符

```c
#include <stdio.h>
int main(){
    char *ps = "This is a good tutorial!";
    int n=10;
    ps=ps+n;
    printf("%s\n", ps);
    return 0;
}
```

范例 不使用 strcpy 函数实现字符串的复制

```c
#include <stdio.h>
void cpystr(char *pss, char *pds){
    while((*pds=*pss)!='\0'){
        pds++;
        pss++;
    }
}
int main(){
    char *pa = "TheCLanguage", b[100], *pb;
    pb=b;
    cpystr(pa, pb);
    printf("string a=%s\nstring b=%s\n",pa, pb);
    return 0;
}
```

字符数组是一个数组，每个元素的值都可以改变。而字符串指针指向的是一个常量字符串，它被存放在程序的静态数据区，一旦定义就不能改变。这是最重要的区别。
对字符串指针方式：`char *ps="C Language";`可以写为：`char *ps; ps="C Language";`
而对数组方式：`char st[]={"C Language"};`不能写为： `char st[20]; st={"C Language"};`只能对字符数组的各元素逐个赋值。

## 指针型函数

一个函数的返回值是一个指针（即地址），这种返回指针值的函数称为指针型函数。定义指针型函数的一般形式为： 

```c
数据类型 *函数名(形参列表){
  函数体
}
```

范例

```c
#include <stdio.h>
// 返回两个字符串中较长的一个
char *func(char *str1, char *str2){
    if(strlen(str1) >= strlen(str2)){
        return str1;
    }else{
        return str2;
    }
}
int main(){
    char *s1 = "C Language";
    char *s2 = "C is very great!";
    char *longstr = func(s1, s2);
    printf("Long string: %s\n", longstr);
    return 0;
}
```

## 指针数组

```c
#include <stdio.h>
int main(){
    int a[3][4] = {0,1,2,3,4,5,6,7,8,9,10,11};
    int *pa[3]={a[0], a[1], a[2]};  //也可以不指定长度，写作 int*pa[]
    int *p=a[0];  //整型指针
    printf("%d, %d, %d\n", a[1][2], *a[1], *(*(a+1)+2));
    printf("%d, %d, %d\n", *pa[1], p[2], *(p+2));
    return 0;
}
```

```
6, 4, 6
4, 2, 2
```

==`int *p[n];` 定义指针数组`p`，它由`n`个指向整型数据的指针元素组成。== 
==`int (*p)[n];` `p`为指向含`n`个元素的一维数组的指针变量。==

## 指向指针的指针

定义方式 `数据类型 **变量名`
指向指针的指针常用在二维数组中。请看下面的例子： 

```c
#include <stdio.h>
int main(){
    char *name[]={
        "Follow me",
        "BASIC",
        "Great Wall",
        "FORTRAN",
        "Computer desighn"
    };
    char **p=name;
    printf("*p=%s\n", *p);
    printf("*(p+1)=%s\n", *(p+1));
    printf("**(p+1)=%c\n", **(p+1));
    printf("**(p+1)=%c\n", *(*(p+2)+3));
    return 0;
}
```

```c
*p=Follow me
*(p+1)=BASIC
**(p+1)=B
**(p+1)=a
```

# 第十章 结构体、共用体和位运算

## 结构体

结构体`Struct`来存放一组不同类型的数据。定义结构体的一般形式为： 

```c
struct 结构体名{
     类型说明符 成员名1;
     类型说明符 成员名2;
     类型说明符 成员名3;
};
```

结构体也是一种数据类型，可以用来说明变量。例如：`struct stu stu1,stu2;`

```c
//定义方法一
struct stu{
    char *name;  //姓名
    int num;  //学号
    char sex;  //性别
    float score;  //成绩
} stu1, stu2;
//定义方法二
struct{  //没有写 stu
    char *name;  //姓名
    int num;  //学号
    char sex;  //性别
    float score;  //成绩
} stu1, stu2;
//定义方法三
#define STU struct stu
STU{
    char *name;  //姓名
    int num;  //学号
    char sex;  //性别
    float score;  //成绩
};
STU stu1, stu2;
```

获取成员方法 `结构变量名.成员名`

```c
//赋值方法一
stu1.name = "Tom";
02.stu2.score = 90.5;
//赋值方法二
struct stu{
    char *name;  //姓名
    int num;  //学号
    char sex;  //性别
    float score;  //成绩
} stu1, stu2 = { "Tom", 10, 'M', 90 };
```

结构体数组

```c
//定义方法
struct stu{
    char *name;
    int num;
    char sex;
    float score;
}class[5];
//获取方法
class[4].score;
```

结构体指针

```c
//定义方法1
struct stu{
    char *name;
    int num;
    char sex;
    float score;
} *pstu, stu1, stu2;
//定义方法2
struct stu *pstu;
//优秀定义格式
#define STU struct stu
STU{
    int num;
    char *name;
    char sex;
    float score;
}boy[5]={
    {101,"Li ping",'M',45},
    {102,"Zhang ping",'M',62.5},
    {103,"He fang",'F',92.5},
    {104,"Cheng ling",'F',87},
    {105,"Wang ming",'M',58}
};
//正确赋值方法
pstu = &stu1;
//错误赋值方法
pstu = &stu;
pstu = stu1;
pstu = &stu1.sex;
//引用方法
(*pstu).num  //注意(*pstu)两侧的括号不可少，因为.的优先级高于*
pstu->num
```

一个结构体指针变量虽然可以用来访问结构体变量或结构体数组元素的成员，但是，不能使它指向一个成员。也就是说不允许取一个成员的地址来赋予它。所以，下面的赋值是错误的： `pstu=&stu1.sex;`

## 枚举类型

```c
//定义方法一
enum week{sun, mon, tue, wed, thu, fri, sat};
enum week a, b, c;
//定义方法二
enum week{sun, mon, tue, wed, thu, fri, sat} a, b, c;
//赋值方法一
a=sun;
//赋值方法二
a=(enum week)1;
//输出方法
printf("%d\n",a);
```

## 共用体

```c
//定义方法一
union data{
    int i;
    char ch;
};
data a, b, c;
//定义方法二
union data{
    int i;
    char ch;
} a, b, c;
//赋值方法
a.ch='A';
a.i=12;
```

共用体所占用的内存空间大小等于最长的成员所占用的字节数。共用体使用了覆盖技术，几个成员变量相互覆盖，从而使几个不同变量共占同一段内存。这也就意味着，同一时刻只能存放一个成员变量的值，只能有一个成员存在，不可能像结构体一样同时存放。如果对新的成员变量赋值，就会把原来成员变量的值覆盖掉。==不能在定义共用体变量时进行初始化==
共用体`data`中，成员`i`所占用的空间最大，为 4 个字节，所以`data`类型的变量（也就是`a`、`b`、`c`）也占用4个字节的内存。

## 类型定义符 typedef

定义格式为`typedef 原类型名 新类型名`
范例

```c
typedef char NAME[20]; //习惯上新类型名大写
NAME a1, a2, s1, s2;
//等效于char a1[20], a2[20], s1[20], s2[20];
typedef struct stu{
    char name[20];
    int age;
    char sex;
} STU;
STU body1,body2;
//
typedef (int*) PINT;
```

## 位运算

| 运算符  |  &   |  \|  |  ^   |  ~   |  <<  |  >>  |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|  说明  | 按位与  | 按位或  | 按位异或 |  取反  |  左移  |  右移  |

`1&1=1` `0&0=0` `1&0=0` `0&1=0`
`1&1=1` `0&0=0` `1&0=1` `0&1=1`
`1^1=0` `0^0=0` `1^0=1` `0^1=1`
`~1=0` `~0=1`
范例

```
9|5=13 //按位或运算
  00001001  9的二进制
 |00000101  5的二进制
  00001101 13的二进制

a=9;
a<<3;  //左移运算 向左移3位
  00001001  9的二进制
  01001000 72的二进制
```

需要注意的是，对于有符号数，在右移时，符号位将随同移动。当为正数时，最高位补0，而为负数时，符号位为1，最高位是补0或是补1 取决于编译器的规定。

# 第十一章 文件操作

## 文件打开  fopen函数

函数原型`FILE *fopen(char *filename, char *mode);`
范例 
`FILE *fp = ("demo.txt", "r");` 打开当前目录的文件
`FILE *fp = fopen("D:\\demo.txt","rb");`  打开D盘的文件
**MODE**

| 打开方式 | 说明                                       |
| ---- | ---------------------------------------- |
| r    | 以只读方式打开文件，只允许读取，不允许写入。该文件必须存在。           |
| r+   | 以读/写方式打开文件，允许读取和写入。该文件必须存在。              |
| rb+  | 以读/写方式打开一个二进制文件，允许读/写数据。                 |
| rt+  | 以读/写方式打开一个文本文件，允许读和写。                    |
| w    | 以只写方式打开文件，若文件存在则长度清为0，即该文件内容消失，若不存在则创建该文件。 |
| w+   | 以读/写方式打开文件，若文件存在则文件长度清为零，即该文件内容会消失。若文件不存在则建立该文件。 |
| a    | 以追加的方式打开只写文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾，即文件原先的内容会被保留（EOF符保留)。 |
| a+   | 以追加方式打开可读/写的文件。若文件不存在，则会建立该文件，如果文件存在，则写入的数据会被加到文件尾后，即文件原先的内容会被保留（原来的EOF符 不保留)。 |
| wb   | 以只写方式打开或新建一个二进制文件，只允许写数据。                |
| wb+  | 以读/写方式打开或建立一个二进制文件，允许读和写。                |
| wt+  | 以读/写方式打开或建立一个文本文件，允许读写。                  |
| at+  | 以读/写方式打开一个文本文件，允许读或在文本末追加数据。             |
| ab+  | 以读/写方式打开一个二进制文件，允许读或在文件末追加数据。            |

在打开一个文件时，如果出错，fopen将返回一个空指针值NULL。在程序中可以用这一信息来判别是否完成打开文件的工作，并作相应的处理。因此常用以下程序段打开文件： 

```c
if( (fp=fopen("D:\\demo.txt","rb") == NULL ){
    printf("Error on open D:\\demo.txt file!");
    getch();
    exit(1);
}
```

## 文件关闭  fclose函数

函数原型 `int fclose(FILE *fp);`       `fp` 为文件指针
范例 `fclose(fp);` 
文件正常关闭时，fclose() 的返回值为0，如果返回非零值则表示有错误发生。

## 字符读取  fgetc函数

函数原型 `int fgetc (FILE *fp);`
`fp`为文件指针。`fgetc() `读取成功时返回读取到的字符，读取到文件末尾或读取失败时返回`EOF`

```c
char ch;
FILE *fp = fopen("D:\\demo.txt", "r+");
ch = fgetc(fp);
```

 在文件内部有一个位置指针，用来指向当前读写到的位置，也就是读写到第几个字节。在文件打开时，该指针总是指向文件的第一个字节。使用`fgetc`函数后，该指针会向后移动一个字节，所以可以连续多次使用`fgetc`读取多个字符。

`feof()`函数用来判断文件内部指针是否指向了文件末尾，它的原型是： `int feof ( FILE * fp );`
当指向文件末尾时返回非零值，否则返回零值。

`ferror()`函数用来判断文件操作是否出错，它的原型是： `int ferror ( FILE *fp );`
出错时返回非零值，否则返回零值。

## 字符写入  fputc函数

函数原型 `int fputc ( char ch, FILE *fp );`
范例 `fputc('a', fp);`
从键盘输入一行字符，写入文件。 

```c
#include<stdio.h>
#include<stdlib.h>
int main(){
    FILE *fp;
    char ch;

    //判断文件是否成功打开
    if( (fp=fopen("D:\\demo.txt","wt+")) == NULL ){
        printf("Cannot open file, press any key to exit!\n");
        getch();
        exit(1);
    }
    printf("Input a string:\n");
    //每次从键盘读取一个字符并写入文件
    while ( (ch=getchar()) != '\n' ){
        fputc(ch,fp);
    }
    fclose(fp);
    return 0;
}
```

## 字符串读取  fgets函数

函数原型 `char *fgets ( char *str, int n, FILE *fp );`
str 为字符数组，n 为要读取的字符数目，fp 为文件指针。
==读取到的字符串会在末尾自动添加 '\0'，n 个字符也包括 '\0'。也就是说，实际只读取到了 n-1 个字符，如果希望读取 100 个字符，n 的值应该为 101==
==在读取到 n-1 个字符之前如果出现了换行，或者读到了文件末尾，则读取结束。这就意味着，不管n的值多大，fgets() 最多只能读取一行数据，不能跨行。在C语言中，没有按行读取文件的函数，我们可以借助 fgets()，将n的值设置地足够大，每次就可以读取到一行数据。==
 fgets() 遇到换行时，会将换行符一并读取到当前字符串。该示例的输出结果之所以和 demo.txt 保持一致，该换行的地方换行，就是因为 fgets() 能够读取到换行符。而 gets() 不一样，它会忽略换行符。
范例 一行一行地读取文件

```c
#include <stdio.h>
#include <stdlib.h>
#define N 100
int main(){
    FILE *fp;
    char str[N+1];
    if( (fp=fopen("d:\\demo.txt","rt")) == NULL ){
        printf("Cannot open file, press any key to exit!\n");
        getch();
        exit(1);
    }
   
    while(fgets(str, N, fp) != NULL){
        printf("%s", str);
    }
    fclose(fp);
    system("pause");
    return 0;
}
```

## 字符串写入  fputs函数

函数原型 `int fputs( char *str, FILE *fp );`
str 为要写入的字符串，fp 为文件指针。写入成功返回非负数，失败返回`EOF`

## 数据块形式读写

函数原型 `size_t fread ( void *ptr, size_t size, size_t count, FILE *fp );`
函数原型 `size_t fwrite ( void * ptr, size_t size, size_t count, FILE *fp );`

- `ptr` 为内存区块的指针，它可以是数组、变量、结构体等。`fread()` 中的 ptr 用来存放读取到的数据，`fwrite()` 中的 `ptr` 用来存放要写入的数据。
- `size`：表示每个数据块的字节数。


- `count`：表示要读写的数据块的块数。


- `fp`：表示文件指针。

理论上，每次读写 `size*count` 个字节的数据。

## 格式化读写文件

函数原型 `int fscanf ( FILE *fp, char * format, ... );`
函数原型 `int fprintf ( FILE *fp, char * format, ... );`
与`scanf()`和`printf()`相比，它们仅仅多了一个`fp`参数。
`fprintf()`返回成功写入的字符的个数，失败则返回负数。`fscanf()`返回参数列表中被成功赋值的参数个数。
如果将`fp`设置为`stdin`，那么`fscanf()`函数将会从键盘读取数据，与 `scanf`的作用相同；设置为`stdout`，那么`fprintf()`函数将会向显示器输出内容，与`printf`的作用相同。

## 文件定位  rewind函数和fseek函数

`rewind()`用来将位置指针移动到文件开头
函数原型 `void rewind ( FILE *fp );`
`fseek()`用来将位置指针移动到任意位置
函数原型 `int fseek ( FILE *fp, long offset, int origin );`

-  fp 为文件指针，也就是被移动的文件。
-  offset 为偏移量，也就是要移动的字节数。之所以为 long 类型，是希望移动的范围更大，能处理的文件更大。
-  origin 为起始位置，也就是从何处开始计算偏移量。C语言规定的起始位置有三种，分别为文件开头、当前位置和文件末尾，每个位置都用对应的常量来表示： 0 文件开头   1 当前位置   2 文件末尾

例如，把位置指针移动到离文件开头100个字节处： `fseek(fp, 100, 0);`
==`fseek()一般用于二进制文件，在文本文件中由于要进行转换，计算的位置有时会出错。==

## 例程

```c
#include<stdio.h>
#define N 2
struct stu{
    char name[10];
    int num;
    int age;
    float score;
} boya[N], boyb[N], *pa, *pb;

int main(){
    FILE *fp;
    int i;
    pa=boya;
    pb=boyb;
    if( (fp=fopen("D:\\demo.txt","wt+")) == NULL ){
        printf("Cannot open file, press any key exit!");
        getch();
        exit(1);
    }
    //从键盘读入数据，保存到boya
    printf("Input data:\n");
    for(i=0; i<N; i++,pa++){
        scanf("%s %d %d %f", pa->name, &pa->num, &pa->age, &pa->score);   
    }
    pa = boya;
    //将boya中的数据写入到文件
    for(i=0; i<N; i++,pa++){
        fprintf(fp,"%s %d %d %f\n", pa->name, pa->num, pa->age, pa->score);   
    }
    //重置文件指针
    rewind(fp);
    //从文件中读取数据，保存到boyb
    for(i=0; i<N; i++,pb++){
        fscanf(fp, "%s %d %d %f\n", pb->name, &pb->num, &pb->age, &pb->score);
    }
    pb=boyb;
    //将boyb中的数据输出到显示器
    for(i=0; i<N; i++,pb++){
        printf("%s  %d  %d  %f\n", pb->name, pb->num, pb->age, pb->score);
    }
    fclose(fp);
    return 0;
}
```

