# 个人编程模板





## ✔️01、常量定义和变量名

```cpp
static const int maxn=1e5+5;
```

```txt
常用变量名：
loop  循环   
sentry 哨兵
ret   返回值
res/result  结果
INF / MAXN / N   很大的值
odd   奇数 
even  偶数
exp  指数
cof  系数
poly 多项式
score 分数
```





## ✔️02、格式化输出模板

```cpp
while( loop-- )
{
    printf("%d%c",solve[loop], loop?' ': '\n'); 
    //32是空格的ASCII，10是换行符号的ASCII
    //等价于printf("%d%c",solve[loop], loop?: 32 : 10);
    //ASCII炫技，很不妥了，可读性很尴尬
}
```

- 下面的有2个技巧

```cpp
#include<bits/stdc++.h>
using namespace std;

//第1个地方，这个方式可以用于区分在本地和OJ
//#define HACV	

int main()
{
	for(int i=0; i<10; ++i)
	{
        //第2个地方，和前面炫技有异曲同工之妙
		printf( (i!=9) ? "num=%d\n" : "Last num=%d\n" , i);
	}

	#ifdef HACV
	system("pause");
	#endif

	return 0;
}
```





## ✔️03、『四舍五入』模板

**1、printf的格式化输出**

`%3d`表示输出3位数，不满3位的高位补『空格』

`%03d`表示输出3位整数，不满3位的高位补『0』

**2、四舍五入『模板』**

- +0.5是精髓
- 但是，一直，不晓得是哪节课，讲解了sqrt在之前还是啥的，要和0.5啥的
  ？？？哪个技巧没做到笔记（后面找到了笔记，eps）

```cpp
double num=3.5;
printf("%d\n",num);//直接截取
printf("%d\n", (int)(num+0.5));//四舍五入
```



```cpp
//num=(num*pow(10,2)+0.5)/pow(10,2);  
//注意，pow(10,需要保留的位数)
////如果采用『四舍五入』
		printf("第%d名选手的最好成绩为:%.2lf\n", (3-loop), num );
```



```cpp
#include<stdio.h>
#include<math.h>
#include<stdlib.h>


struct node
{
	double val[3];
} solve[3];


int main()
{



	//第（3-loop）个选手的成绩
	int loop=3;
	while( loop-- )
	{
		printf("请输入第%d名选手的三次成绩\n", (3-loop) );

		//输入第（tag+1）个成绩
		int tag=0;
		while( tag<3 )
		{
			//如果输入错误则要求强制重新输入
			while( 1 )
			{	
				double num;
				scanf("%lf",&num);
				if( (num-0.0)>0.0001 && (num-10.0)<0.0001 )
				{
					solve[loop].val[tag]=num;
					break;//关键之处：用while(1)和break的组合来弄出那样的效果
				}
				else
				{
					printf("输入错误,请重新输入！\n");
				}
			}//#end while( 1 )

			++tag;
		}//#end while( tag<3 )

			
	}//#end while( loop-- )


	loop=3;
	while( loop-- )
	{
		double num=solve[loop].val[0];
		int i=1;
		for(; i<3; ++i)
		{
			if( num<solve[loop].val[i] )
			{
				num=solve[loop].val[i];
			}
		}
		printf("第%d名选手的最好成绩为:%.2lf\n", (3-loop), num );

	}


	return 0;
}
```



**3、注意事项**

```cpp
%d 是直接将double第1位小数截取
%.1f是指将第二位小数直接去掉还是要四舍五入？
    答：%.1f (注意是1)对第二位小数，四舍五入！！
```

```txt
%.2lf竟然是四舍五入的！

以此留念。
```

```cpp
C语言printf函数%.2f输出为什么四舍五入实现机制不同？
```

知乎上[回答](https://www.zhihu.com/question/364159510)



## ✔️04、判断某个整数奇/偶

```cpp
int n;
if( n&1 )
{
    //奇数
}
else
{
	//偶数
}
```

## ✔️05、判断是否非0

```cp
int n;
if( n )
{
	//n=1，还有n=-1啥的
}
```



## ✔️06、『逆向思维』编程技巧

反转反转，这种逆向思维，来自高中物理，在代码中也有用到

- 比如，大数加法



## ✔️07、大数算法『模板』



### （1）大数加法

- 牛客网，[两个链表生成相加链表](https://www.nowcoder.com/questionTerminal/c56f6c70fb3f4849bc56e33ff2a50b6b)

### （2）大数乘法



### （3）大数阶乘

- [牛客网](https://blog.nowcoder.net/n/158ab1f38b3a4e75b79788e92139a8e2)，N的[阶乘](https://www.nowcoder.com/practice/f54d8e6de61e4efb8cce3eebfd0e0daa?tab=answerKey)



## ✔️08、常用字符函数『记忆』

> 常用的『判别7子』

```cpp
//如果是'0'-'9'返回对应的ASCII码，否则返回0『表示不是』
int isdigit( int ch ); 

//如果是'a'-'z'返回对应的ASCII码，否则返回0『表示不是』
int islower( int ch ); 
//如果是'A'-'Z'返回对应的ASCII码，否则返回0『表示不是』
int isupper( int ch ); 
//如果是'a'-'z'或者'A'-'Z'，返回对应的ASCII码，否则返回0『表示不是』
int isalpha( int ch ); 

//单词来源：alnum= alpha+num
//如果是'0'-'9'或'a'-'z'或者'A'-'Z'，返回对应的ASCII码，否则返回0『表示不是』
int isalnum( int ch ); 
```



转换类

```cpp
//如果是'A'-'Z'返回对应的'a'-'z'，否则返回它本身『也就是不变化』
int tolower( int ch ); 

int toupper( int ch ); //小写转大写
```

- 测试上面代码

```cpp
//测试代码
char a='A';
char b='+';
printf("%c %c\n", tolower(a), tolower(b) );
```





## ✔️09、字符串比较『记忆法』

```cpp
记忆方法：类比数学
strcmp(a,b)>0  表示a-b>0  也就是，表示a比b的字典序大
strcmp(a,b)<0  表示a-b<0  也就是，表示a比b的字典序小
strcmp(a,b)==0  表示a-b=0  也就是，表示a和b相同
```





## ✔️10、积累的小Tips

```cpp
### 类型转换：

#### （1）自动类型转换
当运算符的两边出现不一致的类型时，会自动转换成较大的类型
大的意思是能表达的数的范围更大
char -> short -> int -> long -> long long
int  ->float  ->double
特殊：
1、对于printf，任意小于int的类型会被转换成int
2、但是scanf不会，要输入short，需要%hd	『注意事项』


#### （2）强制类型转换
要把一个量强制转换成另一个类型（通常是较小的类型）
注意，这时候的安全性，小的变量不总能表达大的量
只是从那个变量计算出了一个新的类型的值。
它并不改变那个变量，无论是值还是类型都不改变
```





## ✔️11、cin和scanf速度相关

```cpp
sync_with_stdio  site: https://blog.nowcoder.net/hacv

#define lson rt<<1
#define rson rt<<1|1
#define lowbit(x) x&(-x)
#define name2str(name) (#name)
#define bug printf("*********\n")
#define debug(x) cout<<#x"=["<<x<<"]" <<endl
#define FIN freopen("","r",stdin)
#define IO ios::sync_with_stdio(false),cin.tie(0)



ios::sync_with_stdio(false);
cin.tie(0);
cout.tie(0);
在ACM里，经常出现数据集超大造成 cin TLE的情况。这时候大部分人认为这是cin的效率不及scanf的错，甚至还上升到C语言和C++语言的执行效率层面的无聊争论。
    其实像上文所说，这只是C++为了兼容而采取的保守措施。我们可以在IO之前将stdio解除绑定，这样做了之后要注意不要同时混用cout和printf之类。

在默认的情况下cin绑定的是cout，每次执行 << 操作符的时候都要调用flush，这样会增加IO负担。可以通过tie(0)（0表示NULL）来解除cin与cout的绑定，进一步加快执行效率。
```



## ✔️12、getchar设计read函数快速读入（正负）

- 即输入字符转换成数字，效率高，在输入数据量特别大的时候采用快速读入可以『避免超时』
- Q：为什么要写快读，cin，scanf不是很简单吗，难道这很慢吗，真的！（之前Pascal就无所谓，全部都read/readln）
- A：我们知道读入字符却是很快的(即getchar)，那么很显然，我们可以用读入字符转数字来加快读入
- A：写成inline函数是为了加速读入『C++技巧』

```cpp
#include<bits/stdc++.h>
using namespace std;

inline int read()
{
	//res表示数字本身,NumSign代表正负,最后乘上res就可以了。
	int res=0;
	int NumSign=1;
	char c=getchar();

	//c如果是非数字字符
	while( c<'0'||c>'9' ) 
	{
		//如果c是负号就把NumSign赋为-1
		if( '-'==c )
		{
			NumSign=-1;
		}
		c=getchar();
	}

	while( c>='0'&&c<='9' ) 
	{
		res= res*10 + c-'0';
		c=getchar();
	}
	
	return NumSign*res;//乘起来输出
}


int main()
{
	int n;
	n=read();

	if( n<=0 )
	{
		printf("num=%d\n",n);
		system("pause");
	}
	int solve[n];
	int loop=n;
	while( loop-- )
	{
		scanf("%d",&solve[loop]);
	}

	for(int i=0; i<n; ++i)
	{
		printf("%d%c",solve[i], i!=(n-1) ? ' ' : '\n' );
	}
	
	system("pause");
	return 0;
}
```

### 『算法选修课上轶事』

```cpp
老师说：getchar()的作用
- 隔壁中南ICPC有人，每次输入输出用getchar()，从来不用cin和scanf，那个要很久。能够省略0.4s，那次就竟然，，，就AC了，那次是卡的常数。那次，卡点，，AC了
- 个人观点：这些技巧学学就好了，算法才是硬实力，感觉老师上课有点太推崇这些。。。似乎不是很好。。编码技巧不是算法课程的注重点。
    这种奇技淫巧的喜爱？？？
    但是，ACM比赛的话，我们不应该重点在于如何提高我们的算法能力吗？？？那些技巧，能学会也好，但是不要太依赖那些
```



## ✔️13、数据表示的范围

- long long的最大值：9223372036854775807
- long long的最小值：-9223372036854775808
- unsigned long long的最大值：18446744073709551615
- __int64的最大值：9223372036854775807
- __int64的最小值：-9223372036854775808
- unsigned __int64的最大值：18446744073709551615



> 最大值的优缺点：

```cpp
对于无穷大的初始化：
const int inf = 0x3f3f3f3f;
const int INF = 0x7fffffff;

memset(a, inf, sizeof(a)); //正确
memset(a, INF, sieof(a)); //错误

对于int型数组a可以用0x3f3f3f3f初始化，但不可以用0x7fffffff，如果非要把a数组初始化为0x7ffffff，可以用语句 fill(a, a+n, INF); //n为元素个数
```







- ICPC类编码手法

```cpp
就讲讲历史，讲讲推荐参考书
本课程知识点（已经讲了的，记得备注一下）
>>- 第1章 经典数规结构与算法
	- 草草的讲了一下stack，queue
>- 第2章 动态规划(Dynanic Programming)
>- 第三章 贪心算法 (Greedy)
>>- 讲了
>- 第四章 穷举搜索 (Complete Search)
>- 第五章 最短路径 (Shortest Path)
>- 第六章 背包问题 (Knapsack)
>- 第七帝 计算几何学Computational Geometr)
>- 第八章 网络流与二部阁匹阳 (Network Flow)
>- 第九章 凸包问题(Iwo-Dimeasional Convex Hul)
>- 第十章 数论与大数问题 (BigNums)
>- 第11章 线性规划与整数规划
>- 第12章 着色问题与排队论
>- 第13章 最小生成树(Minimun Spanning Tree)
>- 第14章 DFS与BFS以及剪枝问题
>- 第15章 组合数学与概率论
>- 第16章 启发式搜索(Heuristic Search)
>- 第17章 近似搜索Aproxinate Scarch)
>- 第18章 泛滥填充(Iood Fll)
>- 第19章 欧拉回路(Eulerian Path)
>- 第20章 回溯搜索技术(Recursive Search Techniques)
```





讲解了：

>- 现在的ACM不是很卡内存了
>  所以，上课没讲空间复杂度（这逻辑绝了）
>  现在不讲空间复杂度了，比如长春赛区，开了二维线段树，很大，接近4G也AC了
>  所以现在，一般你的电脑能开多大内存，一般也能给你弄
>  **现在比赛一般不卡内存了**。。。。。。


>- 还是有**卡内存**的题目，比如**幻方矩阵**。





**比赛也很少考常数（常数级别算法？？）的，也就是1-2倍的区别**
比赛一般放8倍





暴力算法是我们进步的阶梯

每次自己写快速排序，，，，不
每早，打快排，(也就是公众号中所说的，我们要做的事情是熟练)

string公式要记忆，组合数，估计阶乘，估计，可以使得题目简单





date: 2020-09-12 eps经验




负值，不能开根号啦

### 浮点数，计算的精度



是的，开根号有误差
第二，在X取整之前需要加0.05，为什么不加？


```cpp
(int)6.99
```

//上面强制类型转换后是6而不是7

```txt
1, 10, 100, 1000...
Time Limit: 1000ms, Special Time Limit:2500ms, Memory Limit:32768KB
Total submit users: 915, Accepted users: 691
Problem 10238 : No special judgement
Problem description
Let's consider an infinite sequence of digits constructed of ascending powers of 10 written one after another. Here is the beginning of the sequence: 110100100010000... You are to find out what digit is located at the definite position of the sequence.

Input
There is the only positive integer number N in the first line, N < 65536. The i-th of N left lines contains the positive integer Ki - the number of position in the sequence. It's given that Ki < 231..

Output
You are to output N digits 0 or 1 separated with a space. More precisely, the i-th digit of output is to be equal to the Ki-th digit of described above sequence.

Sample Input
4
3
14
7
6
Sample Output
0 0 1 0
Problem Source
USU Open. October'2002 Junior
```


### AC的代码

```cpp
#include<cstdio>
#include<cmath>

const double eps=0.05;

int test(int n)
{
	double x=sqrt(8.0*n+1);
	
	//用这种，0.05的来在强制转换（int)前是为了防止
	//本来经过很多次计算，应该获得是（int)7.00，最终是7
	//但是可能出现(int)6.999就变成了6这样的情况 
	//但是有一说一，有这比较方式，还不如，直接fabs(x-x)<=eps 
	if(0==x-(int)(x+eps))
	{
		return 1;
	}
	else
	{
		return 0;
	}
} 
 
 
int main()
{
	int n;
	int temp;
	while(~scanf("%d",&n))
	{
		while(n--)
		{
			scanf("%d",&temp);
			//可读性极差，。。
			printf("%d%c",test(temp-1),n?32:10);
		}
	}
	return 0;
}
```

### 一行区别的WA

```cpp
#include<cstdio>
#include<cmath>

const double eps=0.05;

int test(int n)
{
    double x=sqrt(8.0*n+1);
    
    //用这种，0.05的来在强制转换（int)前是为了防止
    //本来经过很多次计算，应该获得是（int)7.00，最终是7
    //但是可能出现(int)6.999就变成了6这样的情况 
    //但是有一说一，有这比较方式，还不如，直接fabs(x-x)<=eps 
    if(0==x-(int)(x+eps))
    {
        return 1;
    }
    else
    {
        return 0;
    }
} 
 
 
int main()
{
    int n;
    int temp;
    while(~scanf("%d",&n))
    {
        while(n--)
        {
            scanf("%d",&temp);
            //32是空格的ASCII，10是换行符号的ASCII
            //这样写代码很炫，但是，可读性极差，。。。炫技 
//            printf("%d%c",test(temp-1),n?32:10);
            printf("%d\n",test(temp-1));
        }
    }
    return 0;
}
```











### OJ数学题

```txt
Reduced ID Numbers 
Time Limit: 2000ms, Special Time Limit:2500ms, Memory Limit:32768KB
Total submit users: 624, Accepted users: 574
Problem 10275 : No special judgement
Problem description
T. Chur teaches various groups of students at university U. Every U-student has a unique Student Identification Number (SIN). A SIN s is an integer in the range 0 ≤ s ≤ MaxSIN with MaxSIN = 106-1. T. Chur finds this range of SINs too large for identification within her groups. For each group, she wants to find the smallest positive integer m, such that within the group all SINs reduced modulo m are unique.

Input
On the first line of the input is a single positive integer N, telling the number of test cases (groups) to follow. Each case starts with one line containing the integer G (1 ≤ G ≤ 300): the number of students in the group. The following G lines each contain one SIN. The SINs within a group are distinct, though not necessarily sorted.

Output
For each test case, output one line containing the smallest modulus m, such that all SINs reduced modulo m are distinct.

Sample Input
2
1
124866
3
124866
111111
987651
Sample Output
1
8
Problem Source
NWERC 2005
```

### 考点：同余定理



这道题是对同余定理的考查，思路很简单，暴力地枚举j，直到j满足集合中任意两个数对j取余都不相等，此时停止循环；

对于代码中的memset，比用for循环初始化为0快，只是在数组大的时候。在数组大小比较小时则for初始化比较省时（我在这超时了4、5次了）

一共是n个学生，所以去完模之后至少要有n个不同的值，所有程序里面的j要从n开始的。当然从1开始也不会错，只是一个小小的优化吧。

代码如下：

```cpp
#include <stdio.h>
#include <string.h>
#include <math.h>

int a[10000001];

int main()
{
	int i,j,n;
	int cas,ans,t;
	int s[303];
	int f;
	scanf("%d",&cas);
	while(cas--)
	{
		scanf("%d",&n);
		for(i=0;i<n;i++)
			scanf("%d",&s[i]);
		for(j=n;j<1000000;j++)
		{
			f=0;
			for(i=0;i<=j;i++)		//这里用memset的话会超时的！
				a[i]=0;
			for(i=0;i<n;i++)
			{
				if(a[s[i]%j])
				{
					f=1;
					break;
				}
				a[s[i]%j]=1;	
			}
			if(!f)
				break;
		}
		printf("%d\n",j);
	}
	return 0;
}
```



- 湖大OJ上还能用gets『2020年记载的』







title: 浮点数相关
date: 2020-10-03 
浮点数的一个坑的细节

## 二、浮点数细节


本文为自己的一个快速记录。

### 1、杭电视频

[杭电-C语言程序设计2](http://mooc1.chaoxing.com/course/206090161.html#courseArticle_157633879)

- 其中的，浮点数部分的视频



在杭电的视频中
(11100.101)<sub>2</sub>=0.11100101*2<sup>101</sup>
指数上面的101，其实是二进制，真的是坑，记得以前在很多书上都不告知，那些数字的由来，注明进制




### 2、清华教材

教材：《C++语言程序设计(第4版)》(郑莉,董渊) 

- 面数：`page15`

<img src="https://gitee.com/HACV/images_bed/raw/master/MainBlog/2020/2020_10/10_03/1.png">

如上，第一个红色箭头

>- 提醒：
>  原码的符号位和数值位是**分离**管理的
>  补码的符号位和数值位是**一起**管理的

所以可以解释，第1个箭头和第2个箭头












## 三、『贪心』解决过桥问题




### 1、题面

>- ●N个人在晚上想通过桥。每次最多过去2个人，需要有手电筒。现在只有1个手电筒。每个人过桥的速度都不一样，过桥的时间以慢的为准。你的工作是找到最少的过桥的方法;
>  ●输入:
>  首先是n,然后n行是过桥的时间。
>  人数不超过1000，而且没有人过桥的时间超过100秒;
>  ●输出:
>  首先输出总共所需最少时间;下面表示过桥的过程(见样例)，如果有多种过桥方案，输出其中一种。
>- 来源：IBM面试题，一道标准的贪心题目

```txt
样例输入：
输入样例
4 	//4个人
1
2
5
10
样例输出：
输出样例
17
1 2			//1和2先过去
1			//1回来
5 10		//5和10过去
2			//2回来
1 2		    //1 2 过去
```


### 2、解法

算法复杂度在于排序


```txt
样例：
4
1 2 5 10
```

#### 1）贪心第1部分——贪心策略1（表述不如，算法清晰）

>- 1）每次过桥2个人， ~~希望一起过去的人时间相差最小~~ ，选领近的两个，所以采用贪心技术。（第1个要贪心的）
>- 理解：比如，上面的最大的10是肯定没有办法避免的，但是我就希望这个5就不要在出现在我的和式里面了
>  时间相差最小：比如，时间最多的人和时间次多的人一起过，这样我们最大的那个时间10就只出现一次
>  怎么办？所以，我希望在过桥的时候，是5和10一起过
>  -2）而且返回的时间要少，所以用时间最少的人返回;往回送手电筒的人，时间要少（第2个贪心）






#### 2）贪心策略1的算法：

预处理：我们将过桥的时间从小到大排好序，标记为T1,T2,T3..Tn

>- 1.首先让时间最少的两人过去，T1，T2（这2个人的使命是：用来往回送手电筒的）      
>- 2.然后，返回T1和T2中的哪一个呢？
>  -- Q：难道返回任何一个都没有关系？
>  -- A：T1不是这次返回的话，反正下次还是要返回的
>  但是，请看这个样例：如果只有3个人，1 2 3，显然如果要T2回去送，返回的时候会长一点点，会影响时间
>- 3.让Tn和Tn-1一起过去，我们希望在时间的总和里面，Tn出现，但是比他稍微小一点的Tn-1就不用再出现了
>- 4.然后余下的T2返回

显然，观察容易知道，经过以上4个步骤会出现：
T1和T2又回到了最初的位置，Tn和Tn-1却过河了
这样，我们就从n个人转换为了n-2个人过河
来回2趟，送过去2个人，得到一个部分最优解。
在这个基础上，不断的分解


#### 3）贪心第2部分——贪心策略2

Q：先前的策略是，时间最小的2个人来送手电筒，那么能否只让时间最小的1个人来送手电筒？
A：不能，因为从数学上可以证明

显然，我们上面的样例中，那个时间5会加到我们的总和中去，

广义的数学证明这个贪心策略不行：

抽象从小到大的4个数，T1，T2，Tn-1，Tn

```txt
贪心策略1：
比如，Tn-1不会出现在最终和式中
T1 T2过去 （T2）
T1回来		（T1）
Tn-1和Tn过去	（Tn)
T2回来		(T2)
sum1=Tn+2*T2+T1;

贪心策略2：
Tn,Tn-1啥的都会出现在最终和式
T1 Tn过去  （Tn）
T1回来		（T1）
T1和Tn-1过去	（Tn-1)
T1回来		(T1)
sum2=Tn+T（n-1）1+2*T1
```

显然
sum2-sum1<0的时候，需要满足Tn-1< 2*T2-T1才能使用
比如这个样例

```txt
4
1 4 5 10
贪心策略1：
10+2*4+1=19
贪心策略2：
10+5+2*1=17
```

所以，我们使用贪心策略1还是2的时候，需要判别Tn-1< 2*T2-T1的成立与否


### 3、结合两种贪心策略的最终代码





```cpp
#include<bits/stdc++.h>
using namespace std;

const int maxn=1000+5;
int test[maxn];




//伪代码，时间复杂度是O（n）
void solve()
{

	//t表示的意识是
	t=2*T2- T1 （最小的T1，次小的T2）

	//2个人来回送手电筒贪心策略
	for(int i=n-l; (s[i-l]>t)&(i>2) ;i-=2)
	{
		printf ("%d %d\n",s[0],s[1]);
		printf ("%d\n",s[0]);
		printf ("%d %d\n",s[i-1],s[i]);
		printf ("%d\n",s[1]);
	}

	//Tn-1< 2*T2-T1才能使用
	//1个人来回送手电筒贪心策略
	for(int j=i; j>l ; --j)
	{
		printf("%d %d\n", s[0],s[j]);
		printf("%d\n", s[0]);
	}
}



//真实代码
int main()
{
	int n;
	while(~scanf("%d",&n))
	{
		for(int i=0;i<n;++i)
		{
			scanf("%d",&test[i]);
		}

		sort(test,test+n);//将所有的时间排序是贪心法的预备工作

	}

	return 0;
}



```








## 四、『分治』算法



- 很显然，递归这种编码技巧，就是分治算法的完美体现之一


### 1、使用情况

问题规模比较大的时候，难以求解
想办法减少



`贪心，DP，分治，减治`
减治，由于时间的关系，我们就不举例子了。


分治：
我们用得比较多的也是二分法，或者三分法





### 2、分治法-到底如何分解问题

到底如何分解问题，其实我一直很迷惑，9.2号。我突然想到一个好像不错的方法：

```txt
1）找到最大的问题
2）找到最简化的问题（最小的问题）
3）分析如何从最大的问题一步步转换为最小的问题
```

我后面，自己找了一个3人，3鬼的方法验证  
3人3鬼过河，人的数目要比鬼多，否则鬼会吃掉人。  

### 3、最大问题

```txt
人人人 鬼鬼鬼|  |
```





### 4、最小问题

```txt
人 鬼|	|
这个容易解决，一次性过去。
```





### 5、中等问题

```txt
人人鬼鬼| |
```

显然，中等问题要成功，最后的状态要是

```txt
人鬼|  |人鬼
```

或者

```txt
鬼| |人人鬼
```



**转换关系**

最大要转换为

```txt
人人鬼鬼|（船在这）  |人鬼
```

中等问题要转换为

```txt
人鬼|（船在这） |人鬼
```









## ICPC轶事

- 印度尼西亚赛区，出现过
- 一上来就AC，10分钟一道
- 万能程序：
- 『多次提交，读到答案』



## 参考资料

- GitHub，机试技巧与STL
- 柳婼，《从放弃C语⾔到使⽤C++刷算法的简明教程》



# 个人模板





## 一、做题步骤

- 1、选择『数据结构』承载

```txt
看到题目，先想能用什么数据结构
以前，为了练习数组和各种前缀和或双指针
故意，没有这些stack和queue
现在，需要拿起这些，并且往往更好想到解法。
```

- 2、针对『数据结构』设计『算法』









## 二、数组和链表专题

排序数组中的搜索问题，首先想到 二分法 解决。    

排序数组使用双指针也是高频选项

### （1）指针的题目

1）首先记得想，会不会是NULL（顺路也考虑了程序的健壮性）

2）指针的题目，就是不断的移动指针达到题目要求




### （2）链表的常见技巧

#### 1、哨兵

- 参考[CSDN](https://blog.csdn.net/w453908766/article/details/50916790)

- 哨兵，顾名思义，是用来解决国家之间**边界问题**的，不直接参与生产活动。  
同样，计算机科学中提到的哨兵，也用来解决边界问题。  
A sentinel is a dummy object that allows us to simplify boundary conditions.
哨兵是用来简化边界问题的虚设对象  
比如：我们在判断链表是否为空，加不加一个头结点，就能看见代码的改善与否。











## 三、树专题

树和链表都是递归结构，很多树的问题可以使用递归来处理。

几种遍历，

其中，主要考察，我们对递归的实现？

但是其实有非递归的实现，（面试可能考！！！）





### 1、基础杂谈



**关于递归到底好不好？**

可能以前在做ACM题目的时候，个人对递归有偏见。

但是面试以来，递归是很好的，它能保证递归有足够的空间去，一般不会爆栈！！！！
此外面试的时候是有时间控制的，你需要做的是精简代码。快速解答、

- 110平衡二叉树+剑指offer55
  借助做过的求树的高度的题目进行递归
  其实自己都不知道为什么AC了，但是获得了经验

1、递归不一定只是递归本身。可以几个不同函数一起递归，分解问题








### 2、树的层序遍历（BFS）

牛客上，没有return最终结果，竟然还能出现内存超限的情况。。。

我在LeetCode上，有用过两个vector模拟队列，但是在这，我用len控制了遍历的节点数。
就能只用一个队列。
















### 3、树的三大遍历

#### （1）递归写法

- 递归写法（习惯递归这种技巧，强化）
  前序、中序、后序遍历，一套框架（伪代码）

```cpp
void DFS( TreeNode * root )
{

    if( nullptr==root )
    {
        return ;
    }

    //前序遍历visit
    DFS( root->left );
    //中序遍历visit
    DFS( root->right );
    //后序遍历visit
}

```




#### （2）栈模拟写法（非递归）

- 非递归写法一（重点掌握，防止爆内存栈）——借助栈实现

#### 1、前序遍历


原理：
根-》左-》右
变为
先访问根

stack先入右边，后入左边，这样，出栈遍历就OK

```cpp
vector<int> preorderTraversal(TreeNode* root) 
{
        
    vector<int> ret;//返回值
    if( nullptr==root )
    {
        return ret;
    }

    stack<TreeNode *> st;
    st.push( root );

    while( !st.empty() )
    {
        TreeNode * temp=st.top();
        st.pop();

        if( nullptr==temp )
        {
            continue;
        }

        ret.push_back( temp->val );//先访问根节点val

        //下面是核心代码：先右后左，这样就能在出栈的时候保证，左子树先被遍历
        st.push( temp->right );
        st.push( temp->left );
    }

    return ret;
}
```


#### 2、后序遍历

原理：借鉴了前序的，想办法，将两者的写法尽量统一！
前序遍历为root->left->right
后序遍历为left->right->root
我们如果可以修改前序遍历为root->right->left
显然就可以用STL的reverse算法反转就OK了

```cpp
vector<int> postorderTraversal(TreeNode* root) 
{

    vector<int> ret;
    if( nullptr==root )
    {
        return ret;
    }

    stack<TreeNode * > st;
    st.push(root);

    while( !st.empty() )
    {
        TreeNode * temp=st.top();
        st.pop();

        if( nullptr==temp )
        {
            continue;
        }

        ret.push_back( temp->val );
        st.push( temp->left );
        st.push( temp->right );
    }

    //反转
    reverse( ret.begin(), ret.end() );
    return ret;
    }
```


#### 3、中序遍历

- 1、这个的理解和前面两个不一样，这个需要借助DFS的角度来看
- 2、可以借助《算法笔记》中DFS走迷宫来理解代码。


```cpp
vector<int> inorderTraversal(TreeNode* root) 
{
    vector<int> ret;
    if( nullptr == root )
    {
        return ret;
    }

    stack<TreeNode * > st;

    TreeNode * cur=root;
    //注意是或
    while( nullptr!=cur || (!st.empty()) )
    {
        //DFS之一条路走到最左的
        while( nullptr!=cur )
        {
            st.push( cur );
            cur=cur->left;
        }

        TreeNode * temp=st.top();
        st.pop();

        ret.push_back( temp->val );//放入输出的数组
        //注意是变成temp的右边
        cur= temp->right;//开始到当前节点的右边去遍历，如果没有，显然会先经过根
    }

    return ret;
}
```














### （3）Morris遍历、化树为链表（非递归）


#### 1、中序遍历

特点，改变了二叉树结构，将二叉树变成了“链表”

- 时间复杂度：$O(n)$ $O(n)$，其中 nn 为二叉搜索树的节点个数。Morris 遍历中每个节点会被访问两次，因此总时间复杂度为 $O(2n)$=$O(n)$$O(2n)$=$O(n)$。
- 空间复杂度：$O(1)$ $O(1)$。


讲解：
[1、Leecode动画演示](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/dong-hua-yan-shi-94-er-cha-shu-de-zhong-xu-bian-li/)

2、讲解算法

```txt
思路与算法
作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/er-cha-shu-de-zhong-xu-bian-li-by-leetcode-solutio/
来源：力扣（LeetCode）
```

- 代码

```cpp
vector<int> inorderTraversal(TreeNode* root) 
{
    vector<int> rt;
    TreeNode * preNode=nullptr;

    while( nullptr!=root )
    {
        //1.链表的左边，要先遍历的
        if( nullptr!=(root->left) )
        {
            //（1）第1步，preNode节点就是当前 root 节点向左走一步，
            //然后一直向右走至无法走为止（理解）
            preNode=root->left;

            while( nullptr!= (preNode->right)  && (preNode->right) != root )
            {
                preNode=preNode->right;
            }


            //（2）第2步，如果，这个preNode的右边节点是nullptr
            //显然我还没有改变成链表
            if( nullptr==(preNode->right) )
            {
                //改变为“链表”
                preNode->right=root;
                //局部改变之后，我们移动root，准备下一次的改变成链表
                root=root->left;
            }
            else
            {
                //（2）第2步，如果，preNode->right == root
                //说明左子树已经访问完了，我们可以直接开始遍历了
                //此外我们需要断开链接？？
                rt.push_back( root->val );
                preNode->right=nullptr;//断开？？？这步需要吗？
                root=root->right;
            }


        }
        else
        {
            //2.没有左孩子，则直接访问右孩子
            rt.push_back( root->val );
            root=root->right;//不断看被改成的链表右侧
        }

    }   

    return rt;
}
```







### （4）线索化二叉树（非递归）

实际做OJ的时候，这种解法可能有局限，毕竟要修改结构体。
新增两个指针。



### 4、重建二叉树『模板』



#### （1）需要熟练的树的代码

- 效果：手到码出
- 递归：前、中、后序遍历
- 迭代：前、中、后序遍历



#### （2）重建二叉树『模板』



> 有2个新名词：

- 1、序列化：必须保存1个中序遍历的结果，然后外加1个前序or后序遍历的结果
- 2、反序列化：根据2次遍历生成的结果恢复二叉树




#### 1、中序+前序->二叉树『树无重复元素』

- [105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
- [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)


#### （1）递归模板

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

TreeNode * solve
(
    vector<int>::iterator preBegin, vector<int>::iterator preEnd, 
    vector<int>::iterator inBegin, vector<int>::iterator inEnd 
)
{
    if( preBegin==preEnd || inBegin==inEnd )
    {
        return nullptr;
    }

    TreeNode * root= new TreeNode( *preBegin );
    //不记得下面这个函数，也可以用for循环自行查找。
    vector<int>::iterator it= find( inBegin, inEnd, root->val );
    int num=(it-inBegin);

    //递归，左闭右开『注意事项』
    root->left=solve( preBegin+1, preBegin+1+num, inBegin,inBegin+num);
    root->right=solve( preBegin+1+num, preEnd, inBegin+num+1, inEnd);
    return root;
}

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) 
    {
        return solve
        ( 
            preorder.begin() , preorder.end() , 
            inorder.begin() , inorder.end()
        );
    }
};
```





#### 2、中序+后序->二叉树『树无重复元素』

- [106. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
- PTA甲级[1020 Tree Traversals](https://pintia.cn/problem-sets/994805342720868352/problems/994805485033603072)



#### （1）递归模板

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
TreeNode * solve
(
    vector<int>::iterator inBegin, vector<int>::iterator inEnd,
    vector<int>::iterator postBegin, vector<int>::iterator postEnd
)
{
    if( inBegin==inEnd || postBegin==postEnd )
    {
        return nullptr;
    }

    TreeNode * root=new TreeNode( *(postEnd-1) );
    vector<int>::iterator it;
    for( it=inBegin; it<inEnd; ++it)
    {
        if( *it==root->val )
        {
            break;
        }
    }
	//注意：左闭右开
    int num=it-inBegin;
    root->left=solve( inBegin, inBegin+num, postBegin, postBegin+num );
    root->right=solve( inBegin+num+1, inEnd, postBegin+num, postEnd-1 );
    return root;
}
class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {

        return solve( inorder.begin(), inorder.end(), postorder.begin(), postorder.end() );
    }
};
```







#### 3、中序+层序->二叉树

- 这个结论，是在『算法笔记』上看到的，我们写出下面的模板代码
- 注意：区间的开闭

> [参考博客](https://www.w3xue.com/exp/article/20193/27695.html)





#### 4、前序+后序->二叉树『不唯一』

（显然树不唯一）



[889. 根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)







## 参考资料

- [日]秋叶拓哉 / [日]岩田阳一 / [日]北川宜稔，《[挑战程序设计竞赛](https://book.douban.com/subject/24749842/)》
- labuladong的算法小抄





# 字符串匹配算法

———突破深信服字符串匹配————

字符串匹配之BF&RK
字符串匹配暴力和hash优化

>- <font face="楷体" color=red size=5>单模式串匹配算法</font>
>
>>- <b>BF算法</b>（Brute Force 的缩写，也叫暴力匹配算法，朴素匹配算法)
>>
>>>- Brute adj. 蛮干不动脑筋的
>>
>>- <b>RK算法</b>（Rabin-Karp 算法）
>>
>>>- 由它的两位发明者 Rabin 和 Karp 的名字来命名的
>>
>>- <b>BM算法</b>（Boyer-Moore 算法）
>>
>>>- 它是一种非常高效的字符串匹配算法，有实验统计，它的性能是著名的KMP 算法的3到4倍。
>>
>>- <b>KMP算法</b>
>
>- <font face="楷体" color=red size=5>多模式串匹配算法</font>
>
>>- <b>Trie树</b>，（又称前缀树，字典树，单词查找树）
>>
>>>- Trie这个术语来自于retrieval根据词源学, trie的发明者Edward Fredkin把它读作/'tri:/ "tree"。但是 ,其他作者把它读作/'tra1/ "try"。
>>
>>- <b>AC自动机算法</b>（Aho–Corasick算法）是由Alfred V.Aho和Margaret J.Corasick 发明的
>>
>>>- 其实，Trie树跟AC自动机之间的关系，就像单模式串匹配中朴素的串匹配算法，跟KMP 算法之间的关系一样，只不过前者针对的是多模式串而已。所以，AC自动机实际上就是在Trie树之上，加了类似KMP的next数组，只不过此处的next数组是构建在树上罢了。

- <b>单模式串匹配的算法</b>
  也就是一个串和一个串进行匹配
- <b>多模式串匹配的算法</b>
  是在一个串中同时查找多个串





## 一、BF算法『暴力』

一顿暴力，直接贴代码

//指针做输入，const修饰避免改动。

```cpp
int BF(const char *text /*in*/ , const char *pattern /*in*/ )
{
    if((NULL==text)||(NULL==pattern))
    {
		return -2;//非法输入
	}
    
    int pos=0;//位置 
    while('\0'!=text[pos])
    {
    	int i=pos;	//text回溯 
    	int j=0;	//pattern回溯 
    	int sum=0;	//已经匹配字符长度
    	while('\0'!=pattern[j])
        {
        	if(text[i]==pattern[j])
            {
            	++sum;
            	++j;
            	++i; 
            }
            else
            {
            	break;
			}
		}
	 
        if(sum==strlen(pattern))
        {
        	return pos;
		}
        
        ++pos;
    }
    
    return -1;//匹配失败    
}
```

分析BF算法：

>- 时间复杂度$O(n*m)$
>- 空间复杂度$O(1)$


其他补充：

>- 尽管理论上，BF算法的时间复杂度很高，但在实际的开发中，它却是一个比较常用的字符串匹配算法：
>
>>- 1.实际的软件开发中，大部分情况下，模式串和主串的长度都不会太长。而且每次模式串与主串中的子串匹配的时候，当中途遇到不能匹配的字符的时候，就可以就停止了，不需要把m个字符都比对一下。所以，尽管理论上的最坏情况时间复杂度大，但是，统计意义上，大部分情况下，算法执行效率要比这个高很多。
>>- 2.BF算法思想简单，代码实现也非常简单。简单意味着不容易出错，如果有bug 也容易暴露和修复。<b>在工程中，在满足性能要求的前提下，简单是首选。</b>这也是我们常说的<b>KISS（Keep it Simple and Stupid）设计原则</b>。所以，在实际的软件开发中，绝大部分情况下，BF算法就够用了



## 二、RK算法

<b>联系</b>：RK算法是BF算法的改进，它巧妙借助了我们前面讲过的哈希算法，引入<font face="楷体" color=red size=5>哈希算法</font>，时间复杂度立刻就会降低。
<b>难点</b>：设计一个可以应对各种类型字符的哈希算法并不简单

<b>思路</b>:我们通过哈希算法对主串中的n-m+1个子串分别求哈希值，然后逐个与模式串的哈希值比较大小。如果某个子串的哈希值与模式串相等，那就说明对应的子串和模式串匹配了（当然我们需要考虑哈希冲突的问题）。比较哈希值是非常快速的，所以效率提高了。
不过这又<b>引入一个问题</b>：通过哈希算法计算子串的哈希值的时候，我们需要遍历子串中的每个字符。尽管模式串与子串比较的效率提高了，但是，算法整体的效率并没有提高。有没有方法可以提高哈希算法计算子串哈希值的效率？
<b>哈希算法设计技巧</b>：我们假设要匹配的字符串的字符集中只包含K个字符，我们可以用一个K进制数来表示一个子串，这个K进制数转化成十进制数，作为子串的哈希值。

<b>没有冲突的哈希</b>：我们只需要比较一下模式串和子串的哈希值
<b>有冲突的哈希</b>：当存在哈希冲突的时候，有可能存在这样的情况，子串和模式串的哈希值虽然是相同的，但是两者本身并不匹配。解决方法很简单。当我们发现一个子串的哈希值跟模式串的哈希值相等的时候，我们只
需要再对比一下子串和模式串本身就好了。
当然，如果子串的哈希值与模式串的哈希值不相等，那对应的子串和模式串肯定也是不匹配的，就不需要比对子串和模式串本身了。

总结：哈希算法的冲突概率要相对控制得低一些，如果存在大量冲突，就会导致 RK 算法的时间
复杂度退化，效率下降。极端情况下，如果存在大量的冲突，每次都要再对比子串和模式串本
身，那时间复杂度就会退化成$O(n*m)$

<b>但一般情况下，冲突不会很多，RK 算法的效率还是比 BF 算法高的。</b>


- 分类，只写一个，，比如编程语言
  summary: BM算法





——————————突破深信服字符串匹配






## 三、BM算法

BM算法的名字取自于它的两位发明者，计算机科学家Bob Boyer 和JStrother Moore

前面的背景：

>- BF算法缺陷：在整个执行过程中,某些轮的比较没有意义，但BF算法还是老老实实地让模式串一位一位挪动。
>- RK算法：为了克服这个缺陷BF，干脆回避了字符的直接比较，改为比较两个字符串的哈希值。但这样做可能产生哈希冲突，性能并不稳定。
>- BM算法：则是想，那么我们能否仍然采用字符比较的思路，并且尽量减少无谓的比较呢?BM算法，本质上其实就是在<b>寻找一种规律</b>。借助这种规律，在模式串与主串匹配的过程中，当模式串和主串某个字符串匹配的时候，能够<b>跳过一些肯定不会匹配的情况</b>，将模式串往后多滑动几位。


为了减少无谓的比较，BM算法制定了两条规则：

>- <b>坏字符规则</b>（bad character rule）
>- <b>好后缀规则</b>（good suffix shift）







### 1、坏字符规则

注意：

>- BF和RK算法，在匹配的过程中，是按模式串的下标从小到大的顺序，依次与主串中的字符进行匹配的。符合我们的思维习惯
>- <b>BM算法的匹配顺序是按照模式串下标从大到小的顺序，倒着匹配的。</b>
> <b>优点</b>：当检测到第一个坏字符之后，我们并不需要让模式串一位一位向后挪动和比较。因为只有模式串与坏字符T对齐的位置也是字符T的情况下，两者才有匹配的可能，坏字符的位置越靠右，下一轮模式串的挪动跨度就可能越长，节省的比较次数也就越多。这就是BM算法从右向左检测的好处。

定义：我们从<b>模式串的</b>末尾往前<b>倒着匹配</b>，当我们发现某个字符没法匹配的时候。我们把这个没有匹配的字符叫作<font color=red>坏字符(主串中的字符)</font>。







### 2、好后缀规则

所谓某个字符串s的后缀子串，就是最后一个字符跟s对齐的子串，比如abc的后缀子串就包
括c, bc。所谓前缀子串，就是起始字符跟s对齐的子串，比如abc的前缀子串有a, ab。 我们
从好后缀的后缀子串中，找一个最长的并且能跟模式串的前缀子串匹配的，假设是{v}, 然后将模
式串滑动到如图所示的位置。



我们可以在每一轮的字符比较之后,按照坏字符和好后缀规则分别计算相应的挪动距离，哪一种距离更长，我们就把模式串挪动对应的长度。这种处理方法还可以避免，根据坏字符规则，计算得到的往后滑动的位数，有可能是负数的情况。





完整代码：

```cpp
#include<cstdio>
#include<cstdlib>
#include<cmath>
#include<cstring>

const int maxn=256;
char text[1000];
char pattern[500];

//1————坏字符规则
//bc为散列表,构建坏字符哈希表
//另外可以这样定义函数，用一级指针做输入，另一级指针做输出
//void generateBC( const char *pattern/*in*/, int m , char * bc /*out*/)
void generateBC(const char pattern[] , int m , char bc[] ) 
{
	for (int i = 0; i < maxn; ++i) 
	{
		bc[i] = -1; // 初始化 bc
	}

	for (int i = 0; i < m; ++i) 
	{
		int ascii = (int)pattern[i]; // 计算 b[i] 的 ASCII 值
		bc[ascii] = i;
	}

}


//2————好后缀规则
//GS（Good Suffix好后缀）存后缀的数组  prefix前缀
//void generateGS(char *pattern /*in*/ , int m , int *suffix /*out*/ , bool * prefix /*out*/)
void generateGS(char pattern[] , int m, int suffix[] , bool prefix[]) 
{
	for (int i = 0; i < m; ++i) 
	{
		// 初始化
		suffix[i] = -1;
		prefix[i] = false;
	}

	for (int i = 0; i < m - 1; ++i ) 
	{ 
		// pattern[0, i]
		int j = i;
		int k = 0; // 公共后缀子串长度
		while (j >= 0 && pattern[j] == pattern[m-1-k]) 
		{ 
			// 与 pattern[0, m-1] 求公共后缀子串
			--j;
			++k;
			suffix[k] = j+1; 
			//j+1 表示公共后缀子串在 text[0, i] 中的起始下标
		}
		if (j == -1) 
			prefix[k] = true; 
		// 如果公共后缀子串也是模式串的前缀子串
	}

}



// j表示坏字符对应的模式串中的字符下标; m 表示模式串长度
int moveByGS(int j, int m, int suffix[], bool prefix[]) 
{
	int k = m - 1 - j; 

	// 好后缀长度
	if (suffix[k] != -1) 
		return j - suffix[k] +1;

	for(int r = j+2; r <= m-1; ++r) 
	{
		if (prefix[m-r] == true) 
		{
			return r;
		}
	}

	return m;
}



//n是text的长度，m是pattern的长度
int BM(char text[], int n, char pattern[], int m )
{
	if((NULL==text)||(NULL==pattern))
	{
		return -2;	//非法输入
	}

	//记录模式串中每个字符最后出现的位置
	char bc[maxn];//bad char 坏字符简写
	generateBC( pattern , m, bc); //构建坏字符哈希表


	int * suffix=(int *)malloc( sizeof(int) * m);
	bool * prefix=(bool *)malloc( sizeof(bool) * m);
	//好后缀数组
	generateGS(pattern, m, suffix, prefix);

	int i = 0; 
	// j 表示主串与模式串匹配的第一个字符
	while (i <= n - m) 
	{
		int j;
		for (j = m - 1; j >= 0; --j) 
		{ 
			// 模式串从后往前匹配
			if (text[i+j] != pattern[j]) break; 
			// 坏字符对应模式串中的下标是 j
		}
		if (j < 0) 
		{
			//释放堆中内存，防止内存泄漏
			free(suffix);
			free(prefix);

			// 匹配成功，返回主串与模式串第一个匹配的字符的位置
			return i; 
		}
		int x = j - bc[(int)text[i+j]];
		int y = 0;
		if (j < m-1) 
		{ 
			//如果有好后缀的话
			y = moveByGS(j, m, suffix, prefix);
		}

		//选择坏字符和好后缀中能让它后移更远的
		int max_num=y;
		if(x>y)
		{
			max_num=x;
		}
		i = i + max_num;

	}

	//释放堆中内存，防止内存泄漏
	free(suffix);
	free(prefix);
	return -1;//未匹配到
}


int main()
{
	scanf("%s%s",text,pattern);
	int n=strlen(text);
	int m=strlen(pattern);
	printf("%d\n",BM(text,n,pattern,m));

	return 0;
} 
```