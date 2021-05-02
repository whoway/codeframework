# OJ多组和单组输入输出

编码的多组输入和单组输入    
说明：本文部分摘选自牛客、POJ并加入了个人思路历程

## 📑 目录

- ⭐️一、OJ多组和单组输入输出
- ✡️二、OJ使用经验
- ✏️三、C语言输入输出
- ☁️四、PAT和牛客对比『解决gets禁用』
- 🐾五、C++中string和C语言风格的字符数组的快速互换





## ⭐️一、OJ多组和单组输入输出

### （1）循环I/O处理FAQ

- 多组输入和输出的做法在ACM和各大OJ也是很常见这些，现在企业招聘使用的一些平台很多也是支持这样的。
- **碎碎念**：笔者以前的时候，第一次接触接触这种输入输出的时候，很是不适应，但是后来，看到下面的一段文字才深刻理解了，单组输入输出和多组输入输出的联系。后来我就没有以前那么纠结，每次做题都想这题到底有没有按暗示我多组输入输出。后来我想通了之后的做法，就是，能用多组输入输出的我也懒得用单组输入输出了，因为多组的方式也能AC掉单组的，但是反正不一定，原因见下面的两端文字吧：
	- 1、为什么需要循环输入输出：通常来说 OJ 对于每道题里面有.in 和.out 文件，分别表示测试数据的输入和输出。如果某些编程题的<b>所有数据</b>都只做在<b>一个.in </b>和<b>一个.out </b>中，这样就会变成多组测试了，所以需要提交的代码中循环处理。
	- 2、处理方法：其实这个问题可以避免，就是编程题后台每个样例做一组对应的.in和.out 文件，这样就变成单组测试，代码就不需要循环处理，但是平时练习的题目质量不一，这个问题都会出现。代码里面循环处理了即使是单组测试也会完全没问题，所以为了偷懒，可以<font style="background: yellow"><b>全写成循环处理</b></font>。	

在线评测系统，你的程序的输入和输出是相互独立的（也就是说，一个在.in文件，输出会重定向到另一个.out文件），因此，每当处理完一组测试数据，就应当按题目要求进行相应的输出，而不必将所有结果存储起来一起输出。





###  （2）常见语法

```c
#include <stdio.h>
int main() {
    int a,b;
    while(scanf("%d%d",&a, &b) != EOF)	//注意while处理多个case
        printf("%d\n",a+b);
    return 0;
}
```
但是我本人，还喜欢这种方式
```c
#include <stdio.h>
int main() {
    int a,b;
    while(~scanf("%d%d",&a,&b))	//注意while处理多个case
        printf("%d\n",a+b);
    return 0;
}
```

解释：`while(~scanf("%d%d",&a,&b))`和` while(scanf("%d%d",&a, &b) != EOF)`是等效的
~是按位取反，scanf的返回值是输入值的个数，如果没有输入值就是返回-1
而我们知道-1的补码表示就是全1，按位取反显然就是0

//特别的，还有在多组输入同时还要求a或者b不为0的
```c
#include<cstdio>
int main()
{
	int a,b;
	while(scanf("%d%d",&a,&b)!=EOF&&(a!=0||b!=0))
	{
		printf("%d\n",a+b);
	}
	return 0;
}
```

```cpp
#include <iostream>
using namespace std;
int main() {
    int a,b;
    while(cin >> a >> b)//注意while处理多个case
        cout << a+b << endl;
}
```



### （3）补充——防踩坑
>- 1）循环输入输出：会发生一个问题(十分常见！！！！)，如果测试数据是多组的，但是恰巧你代码里面需要些标记数组，map，set 等，在循环内一定记得清空，不然可能会产生前面的测试样例影响了后续数据的答案。

>- 2）一般多组输出，记得要换行，printf("%d\n",sum);
>//第一次的时候，由于没有加\n，OJ告诉我是，答案错误
>//加了\n就对了



### （4）什么叫特判『Special judge』

> 大概意思是：题目同样的样例，你的输出可能和题目不一样也没所谓
>
> 反正答案对就行，比如某个矩阵，横竖斜和是15，答案不唯一，你只要写出一个也OK

- 在幻方矩阵一题中，还有那个所谓的（特殊判断）
- 笔者在，2020年（即2021届秋招）腾讯笔试中遇见了



### （5）牛客多组I/O传送门

[OJ在线编程常见输入输出练习场](https://ac.nowcoder.com/acm/contest/5650) 



## ✡️二、OJ使用经验




### （1）超时

- Q：如何知道自己代码是否太慢了，超时？
背景：实际编码的时候，大家其实都不会去马上分析时间复杂度，可能是先写完再看会不会超时，那就产生上面的问题。
- A：可以用大的边界的数据，最耗时的那种
用1 1000000000000，本地，自我运行了一次，发现，2秒没出来，很显然超时，毕竟比赛的也就1-2秒，测一下也不掉肉



### （2）常见边界数据

- 数据全相同
- 全0
- 元素无
- 空指针



### （3）『特殊判据』

- 也就是你输出的结果可以和题目中样例输出结果不一样，但是是对的。
- 比如『幻方矩阵』这个题目，行检查，列检测也可以

> 特判底层原理：将你的输出数据，输入去检测，而不是一般的比对

- 2020年秋季，参加腾讯笔试的时候，我碰到了这种特判。



## ✏️三、C语言输入输出



### （1）辨析单引号和双引号

`'3'`代表的是“字符”3

`"3"`代表的是“字符串”3



### （2）常见数字格式——输入输出

|           | 输入 | 输出 |
| --------- | ---- | ---- |
| int       | %d   | %d   |
| long long | %lld | %lld |
| double    | %lf  | %lf  |



### （3）字符串输入输出

注意：

字符串是个逻辑概念

- 纯C语言中，用字符数组来承载它，也就是我们所说的具体实现
- 纯C++写法中，用string来承载它。PS：string底层封装了字符数组，但是比较复杂，初学C++不需要深究，不看源代码，无法理解。

我们只考虑，C语言的输入输出。

C++的string，请用cin啥的。



|        | 输入 | 输出 |
| ------ | ---- | ---- |
| 字符串 | %s   | %s   |
| 字符   | %c   | %c   |

字符和字符串的差别，在第1讲讲了。难点在字符串用“字符数组承载”



#### 1、用scanf

scanf的%s

输入：是识别到`' '`（空格）或者`'\n'`（换行）就不要了，然后在扫描进的后面自动加上`'\0'`

输出：是识别到`'\0'`就输出完毕

```cpp
#include<bits/stdc++.h>
using namespace std;

static const int maxn=1e5+5;
int solve[maxn];

int main()
{
    scanf("%s",solve);
    //第1组测试123 24343
    //第2组测试23134131
    
    printf("%s",solve);
    return 0;
}
```



> scanf的%s是以 空白符（包括空格）来进行截断的！！
> 注意，在读入n之后，要使用getchar来接收后面的换行符，否则会使得for循环内的gets读入这个换行符，导致第1个字符串读取错误。
>



#### 2、用gets

```cpp
char test[105];
int i=0;
while(NULL!=gets(test)) 
{
    ++i;
}
```



- PAT中C语言编译器允许用
- PAT中C++编译器**禁止**这个用法！（由于可以利用该函数进行『缓冲区溢出攻击』）
- 牛客上C++编译器**禁止**这个用法！（由于可以利用该函数进行『缓冲区溢出攻击』）

gets输入一行，无论中间会不会有空格

**它识别到'\n'就不要了**

> Tips：由于，gets这个函数可以进行“缓冲区溢出”攻击，在很多平台开始禁用！
>
> - 牛客网禁用
> - PTA禁用



**PTA和牛客对比注意：**

1.PAT上数据比牛客上严格  
2.PAT上2020年有一些题目的边界数据的增加，有的教程上代码无法AC了    

### （4）使用cin.getline解决gets禁用

**PAT编译器上的坑**  

- 『1』PAT的这两个`C++`编译器(`C++ gcc6.5.0`和`C++ clang++ 6.0.1`）都不支持`gets()`  
要是你的C++代码中出现了，就会导致（似乎原因是什么不安全...）    
```txt
a.cpp: In function ‘int main()’:
a.cpp:12:11: error: ‘gets’ was not declared in this scope
  gets(str1);
```

- 『**解决方式**』：使用 **iostream**库中的`cin.getline`函数代替`gets`

```cpp
/* 读入一行（可含空格），直到换行符结束
 * 将其前num-1个字符存入数组a中并以字符c结尾 */
cin.getline(a, num, c);
解决方式：
使用 iostream 库中的cin.getline函数代替gets
tips：
1、也可以不传入第三个参数c，则默认 '\0' 结尾
2、若num大于所读入的字符数，则直接存入整行字符串，再在末尾加入字符c结尾
    
比如
    cin.getline(ch2,6);//在不遇到结束符的情况下，最多可接收6-1=5个字符到ch2中 

```

- 演示如下：

```cpp
char solve[20];
//注意，下面我们用的是20，但是实际上获得的是19个，因为最后那个被识别到的'\0'也要识别进去
//然后，
while( cin.getline( solve, 20) )
{
    printf("%s\n",solve);
    printf("Ok\n");
}
```

- 『2』PAT上面的C语言编译器支持`gets()`（可以用C语言编译器），如果你不想用`C++`的STL的话。  





## ☁️四、OJ多组输入输出『分语言』







### （1）纯C++语言版本（不准用C语言版本）

为了能够熟练的使用`C++`的STL  
由于自己熟练C语言的字符数组，思维方式快成纯C语言的了，但是这些很影响刷OJ做题的速度。  
所以，打算，使用`C++`中的`String`代替字符数组  
弃用字符数组。  

原因
```txt
比如字符查找，我就可以懒得写了
字符匹配，也懒得写
```

- **1、整型数据**

```cpp
#include<iostream>
using namespace std;

int main()
{
	int a,b;
	
	while(cin>>a>>b)
	{
		cout<<a+b<<endl;
	}
	return 0;
} 
```

**严格的**

这样的格式
```txt
3,6
```

//cin.get()使用比较难讲，不要赖用
```cpp
#include<iostream>
using namespace std;

int main()
{
	int a,b;
	char c;
	while((cin>>a)&&(c=cin.get())&&(cin>>b))
	{
		cout<<a+b<<endl;
        cout.put(c);
	}
	return 0;
} 
```

- **2、字符数组**（C++中用string类——自己不准自己用字符数组）

注意，这种输入，下面这样的数据，注意也用这组数据测试3）
```txt
asdad asdsa
```
```cpp
#include<iostream>
#include<string> 
using namespace std;

int main()
{
	string str;
	while(cin>>str)
	{
		cout<<str<<endl;
	}
	
	return 0;
} 
```

- **3、字符数组**（C++中用string类）两个-用空格分开

```cpp
#include<iostream>
#include<string> 
using namespace std;

int main()
{
	string one;
	string two;
	while(cin>>one>>two)
	{
		cout<<one<<endl;
		cout<<two<<endl;
	}
	
	return 0;
} 
```

- **4、整行字符(string)，包括空格**『学习记忆』

```cpp
#include<iostream>
#include<string> 
using namespace std;

int main()
{
	string one;
	string two;
	//未考查下面这种多组输入 
	while(getline(cin,one))
	{
		cout<<one<<endl;
		
	}
	
	return 0;
} 
```










### （2）纯C语言版本

- 0、单个字符

- **1、整型数据**

```c
#include<stdio.h>

int main()
{
	long long int a,b;
	while(~scanf("%lld%lld",&a,&b)) 
	{
		printf("%lld\n",a+b);
	}
	return 0;
}
```



- **2、字符数组**

```c
#include<stdio.h>

int main()
{
	char test[100];
	while(~scanf("%s",test)) 
	{
		printf("%s\n",test);
	}
	return 0;
}
```



- **3、字符数组两个-用空格分开**

```txt
aa ss
```

```c
#include<stdio.h>

int main()
{
	char one[100];
	char two[100];
	
	while(~scanf("%s%s",one,two)) 
	{
		printf("%s 中间加上我 %s\n",one,two);
	}
	return 0;
}
```



- **4、整行字符，包括空格**

```c
#include<stdio.h>

int main()
{
	char test[100];
	
	while(NULL!=gets(test)) 
	{
		printf("%s\n",test);
	}
	return 0;
}
```







### （3）Java版本

//我自己配置的notepad++的java环境的，快捷键是F6就可以调用`插件NppExec`
Java在很多OJ  
<font style="background: yellow">1）只能使用 Main 作为主类名 </font> 
<font style="background: yellow">2）代码中必须存在一个public class Main。不允许出现其他的public class。 </font> 
牛客上还规定：

```txt
JAVA，注意类名必须为Main, 不要有任何package xxx信息
注意hasNext和hasNextLine的区别
```

附上[OJ中提交Java程序的一些套路](https://blog.csdn.net/bat67/article/details/79685997)
[Java：OJ中常用的各种输入](https://blog.csdn.net/da_kao_la/article/details/80225003)

- **1、整型数据**

```java
import java.util.Scanner;
public class Main
{
	//只能保存为Main.java
    public static void main(String[] args)
	{
        Scanner in = new Scanner(System.in);

        while (in.hasNextInt())
		{
			//注意while处理多个case
            int a = in.nextInt();
            int b = in.nextInt();
            System.out.println(a + b);
        }

    }
}
```







## 🐾五、C++中string和C语言风格的字符数组的快速互换



受到C语言中`sscanf`和`sprintf`的启发

### （1）string→字符数组

- **方法1、用string类的成员函数copy**
- 注意，其实，C语言输入输出和C++输入输出，最好不要混合输入输出，我这样写只是为了论证这样可以

```cpp
#include<iostream>
#include<string> 
#include<cstring> 
using namespace std;

int main()
{
	
	while(1)
	{
		string str;
		cin>>str;
		char test[10]; 
		memset(test,-1,sizeof(test));
		//上面的memset是我故意，用来让自己注意
		//string转换到字符数组后，末尾的'\0'要手动加，不然就不行
		 
		
		str.copy(  test,  str.size()  );
		test[str.size()]='\0';
		 
		printf("%s\n",test);
	} 
	return 0;
} 
```



- **方法2、string的c_str()和C语言中的strcpy**

```cpp
#include<iostream>
#include<string> 
#include<cstring> 
using namespace std;

int main()
{
	
	while(1)
	{
		string str;
		cin>>str;
		char test[10]; 
		memset(test,-1,sizeof(test));
		//上面的memset是我故意，告诉我们这样就不用管这些 
		
		strcpy(  test,  str.c_str()  ); 
		 
		printf("%s\n",test);
	} 
	return 0;
} 
```



### （2）字符数组→string



```cpp
string (1)	
	string& operator= (const string& str);
c-string (2)	
	string& operator= (const char* s);
character (3)	
	string& operator= (char c);
initializer list (4)	
	string& operator= (initializer_list<char> il);
move (5)	
	string& operator= (string&& str) noexcept;
```



```cpp
#include<iostream>
#include<string> 
#include<cstring> 
using namespace std;

int main()
{
	char test[10];
	while(~scanf("%s",test))
	{
		
		string str;
		str=test;//字符数组转换为string ，注意，这个是可以的『因为重载了operator::=()』去
        //参考：http://www.cplusplus.com/reference/string/string/operator=/
		
		printf("%s\n",str.c_str());
	} 
	return 0;
} 
```

- 另一种用构造函数写的，但是有坑，那就是只能在构造的时候，初始化时

```cpp
#include<iostream>
#include<string> 
#include<cstring> 
using namespace std;

int main()
{
	char test[10];
	while(~scanf("%s",test))
	{
		
		string str(test);//注意——只能在初始化的时候，字符数组转换为string 
		
		//注意——下面这种方式不准！！ 
//		string str;
//		str(test);
		
		printf("%s\n",str.c_str());
	} 
	return 0;
} 
```



