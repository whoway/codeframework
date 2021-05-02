# C++中STL熟练手册





## [📑 目录](https://hacv.gitee.io/studycpp2.0/#/?id=📑-目录)

- ⭐️STL参考资料
- ➕STL熟悉的好处和坏处
- ✏️C++





## ⭐️参考资料

- 网站[Cplusplus](http://www.cplusplus.com/reference/string/string/?kw=string)

> 配套习题：来自我的『牛客博客』





## ➕STL优点和缺点

- 数据结构学习建议
- 不要拿C语言学数据结构『巨佬轻拍』

- 不要用纯C语言刷算法题『巨佬轻拍』
- C++中STL是学习数据结构和算法的利器

请使用**C++11编译选项**编译！！！！

```txt
-std=c++11
```

- STL不熟悉的教训

```txt
1、STL不熟，什么都容易变成用C语言的想法，写代码就要自力更生
比如，字符串匹配，就想着自己写，却不知道用string
『强烈建议』：要把STL弄得炉火纯青再去刷题！！！！！
2、能用STL的，除非极限的效率，不然，绝对不自己写！！
其实这也是阻碍我一直以来没有快速进步的原因！！！
3、本来算法应该重点在如何进行。而不是代码如何实现，但是由于当时我自己的代码实现水平的太差，搞得，其实我有其他想法，但是算法的时候，我就又改为C语言风格的了。代码量冗长，对比赛和秋季招聘『笔试』极其不利！！！
4、我在某大厂面试的时候，由于记错STL的成员函数...debug了一段时间，然后挂了。。
```

- STL的缺点

```txt
面试时候的，可能要你手写『堆排序』，那么你就不准用STL的make_heap和sort_heap来解答
```





## ✏️STL训练习题集



>- 类模板 
>- 函数模板
>- 数据结构
>- 算法
>- 封装



> 1、数据结构类

### （1）vector（单端数组）

- **单端数组**/向量/可变长数组



`#include<vector>`

可变长数组
底层实现是数组
具体可以看清华邓俊辉的

```txt
**单端数组**/向量/可变长数组
erase函数
26. 删除排序数组中的重复项
```



### （2）list（双向链表）

```cpp
#include<list>
```

双向链表



### （3）set『3种』

```cpp
#include<set>
```



set（集合-有序）

集合
内部自动有序
并且不含重复元素的容器，也就是会去重。

内部实现是**红黑树**

##### **1、multiset**『多重集合-有序』

> set中元素是唯一的。
> 而我的这个的元素不是唯一的。
> 也就是元素没有去重。

样例：

```txt
输入一个长度不超过20的字符串，对所输入的字符串，
按照ASCII码的大小从小到大进行排序，请输出排序后的结果
```

```cpp
#include<stdio.h>
#include<string.h>
#include<set>
using namespace std;
 
 
int main()
{
    char str[20+1]={0};
    multiset<char> st;//要是用set，则去重了，不行baca这样子的
    while(~scanf("%s",str))
    {
        st.clear();
        int i=0;
         
        while(str[i]!='\0')
        {
            st.insert(str[i]);
            ++i;
        }
         
        for(multiset<char>::iterator it=st.begin() ; it!=st.end() ;it++)
        {
            printf("%c",*it);
        }
         
        printf("\n");
        memset(str,0,sizeof(str));
    }
     
    return 0;
 }
```





##### **2、unordered_set**『无序集合』

<font color="red" size=5>C++11标准中添加的</font>

> 可以用来处理只去重复，但是不排序
> 内部实现是散列（hash）

### （4）map『3种』

- 映射-有序

```cpp
#include<map>
```



映射

可以将任何基本类型和STL容器，映射到任何基本类型和STL容器

注意，map中的键和值是唯一的

内部实现是**红黑树**






##### **1、multimap**『映射-有序』

> 一个键对应多个值





##### **2、unordered_map**『无序映射』

<font color="red" size=5>C++11标准中添加的</font>

> 底层实现是散列（hash）



#### unordered_map的『经典用法』题目

1、两数之和

[两数之和](https://www.nowcoder.com/practice/20ef0972485e41019e39543e8e895b7f?tpId=191&&tqId=36133&rp=1&ru=/ta/job-code-high-algorithm&qru=/ta/job-code-high-algorithm/question-ranking)

**注意点**：

1）unordered_map的find要是找不到返回的东西 mp.end()  
2）map的键和值是唯一的，所以本题显然是不能用的。  
3）multimap可以一个键对应多个值，unorder_map也是一样。  

- 区别，mulimap不仅映射并且按key排序的需求  
- unorder_map只映射，不按key(键)排序。  

所以，我们才可以将比如 3 2 2 3 寻找6  
将3映射为0，将3映射为3，这样来解题  

```cpp
//奇怪的是，为什么这题中，我想要用unordered_map还用亲自弄头文件
//当然显然#include <unordered_map>也是可以的
#include<bits/stdc++.h>

class Solution {
public:
    /**
     * 
     * @param numbers int整型vector 
     * @param target int整型 
     * @return int整型vector
     */
    vector<int> twoSum(vector<int>& numbers, int target) {
        // write code here
        unordered_map<int,int> mp;
        
        int len=numbers.size();
        for( int i=0; i<len ; ++i )
        {
            mp[ numbers[i] ]=i;
        }
        
        for( int i=0; i<len ; ++i )
        {
            int num=target-numbers[i];
            
            //如果num存在！！！并且不是nums[i]本身
            if( mp.find(num)!= mp.end() && mp[num]!=i )
            {
                int a=i+1;
                int b=mp[num]+1;
                vector<int> rt;
                rt.push_back(a);
                rt.push_back(b);
                return rt;
            }
        }
        
        
    }
};
```











### （5）string

```cpp
#include<string>
```









### （6）queue『3种』

```cpp
#include<queue>
```



队列

##### 1』deque（双端数组）

> 双端队列。双向队列

##### 2』priority_queue（优先队列/堆）

> `include<queue>`就可以用优先队列
> 优先队列
> 用堆实现的**默认**将当前队列**最大元素**置于队首的容器

请用`priority_queue`设置最小堆写   
用`make_heap`设置最小堆写  
[腾讯笔试-石子合并](https://www.nowcoder.com/questionTerminal/3eef8d66b0fa4f71a8498974547fe670)  







### （7）stack

```cpp
#include<stack>
```



### （8）pair

（使）成对
`#include<utility>`才能使用（奇奇怪怪）

注意，map内部实现涉及到了pair,所以，要是我们
`#include<map>`
那么我们要是想要使用pair，就不用另外`#include<utility>`了







### （9）bitset『比特集合』

```cpp
#include<bitset>
```



```cpp
头⽂件是 #include <bitset> ，bitset可能在PAT、蓝桥OJ中不常⽤

但是在LeetCode OJ中经常⽤到～⽽且知道bitset能够简化⼀些操作，可能⼀些复杂的问题能够
直接⽤bitset就很轻易地解决～

以下是⼀些常⽤⽤法
```



若干个位



> 2、算法类头文件

```cpp
#include<algorithm>
```











## 🌞STL增删改查（CRUD）

- Create(创建)
- Read Retrieve(读取)
- Update（更新）
- Delete（删除）



### 一、string字符串



> 注意，这个类的底层有个静态变量
>
> `string::npos`
>
> `npos` is a static member constant value with the greatest possible value for an element of member type `size_type`.

### （1）others成员函数

- 1、构造函数

```cpp
『默认构造』
    string();
『拷贝构造』
    string(const string &str);//比如string strDst(str)
	string(const char *s);//比如string strDst( solve )
	string(int n, char c);
```

- 2、赋值

```cpp
『重载赋值运算符』 
    string & operator=( const string & s );//str=s;

『assign函数』
	string & assign( const char * s);//str.assign(s);
	string & assign( const char * s, int n);
	string & assign( const string & s );
	string & assign( int n, char c );
	string & assign( const string & s, int start, int n);
```

- 3、长度

```cpp
int length()const;	//长度不包括字符串末尾的'\0'
bool empty()const;	//当前字符串是否为空
```

- 4、拷贝『string→字符数组』

```cpp
int copy( char * Dst, int n, int pos=0 )const;

//str.copy( dst, str.size() , 0 );
//str.copy( dst, str.size() );
```

```cpp
const char * c_str( ) const;//返回1个以'\0'结尾的字符串的首地址
```







### （2）『增』元素



- 1、字符串连接

```cpp
运算符重载：
    string & operator+=( const string & S);
	string & operator+=( const char * s);

append单词
	string & append( const char * s ); 
	
```



### （3）『删』元素

```cpp
//删除从postion开始的n个字符，返回修改后的字符串
string & erase( int pos=0, int Len=npos );
```



### （4）『改』元素



- 1、插入元素

```cpp
string & insert( int pos, const char * s );
string & insert( int pos, const string & S);

```

- 2、替换元素

```cpp
//删除从pos开始的n个字符，然后在pos处插入s
string & replace( int pos, int n, const char * s);
string & replace( int pos. int n, const string & S);
```

- 3、交换string

```cpp
void swap(string & s2);
```



### （5）『查』元素

- 1、从前往后和从后往前查找

```cpp
//找不到就返回-1
int find( char c, int pos=0 )const;
int find( const char * s, int pos=0 ) const;
int find( const string & S, int pos=0 )const;


//从后往前找
int rfind( char c, int pos=npos )const;
int rfind( const char * s, int pos=npos )const;
int rfind( const string & S, int pos=npos )const;
```

- 2、获取string的子串

```cpp
string substr (int pos = 0, int Len = npos) const;
```



### 二、list双向链表



### （1）others成员函数

- 1、构造函数

```cpp
list<int> mylist;
list<node *> mylist;
list< pair<int， vector<int>::iterator > > mylist;
```

- 2、赋值

```cpp
list & operator=( const list & Lst );

MyList.assign( beg , end );//拷贝[beg,end)区间的数据
MyList.assign( n, elem );
```



- 3、长度获取和修改

```cpp
list.size();
list.empty();

list.resize( num );//变长，用默认值0填充，变短，尾部的元素被删掉
list.resize( num ,elem );//用num而不是0填充
```





- 反转链表『233，想起，面试题』

```cpp
mylist.reverse();
```



### （2）『增』元素



- 1、使用push之类的

```cpp
list.push_back( elem );//尾巴增加
list.push_front( elem );//前面增加，这叫“双向”之一
```

- 2、使用insert之类的

```cpp
MyList.insert( pos, elem );//在pos位置插入1个elem元素的拷贝，返回新数据的位置
MyList.insert( pos, n, elem );//插入n个元素，无返回值
MyList.insert( pos, beg, end );
```





### （3）『删』元素

- 1、pop一类的

```cpp
list.pop_back();//删掉尾巴1个
list.pop_front();
```

```cpp
MyList.erase( beg, end );
MyList.erase( pos );
```

```cpp
//删掉，容器中『所有与elem』值相匹配的元素
MyList.remove( elem );

//移除，整个容器中的所有数据
MyList.clear();
```



### （4）『改』元素



### （5）『查』元素

- 1、查前面和后面

```cpp
int num=list.front();
int num=list.back();//注意是back，不是end!!! 
```





### 三、优先队列priority_queue



### （1）others成员函数














































### C++ lamda表达式

10. 正则表达式匹配

















## 一、vector类型

```cpp
copy(solve.begin(), solve.end(), flag.begin()+3);//将solve数组中的数据，拷贝到flag.begin()+3的位置开始
```



```cpp
vector<int> solve;
vector<int> temp(solve.begin(),solve.end());

int a[5]={1,2};
vector<int> demo(a,a+5);

demo.resize(10);
```



```cpp
vector<int> mySolve(5);
```







## 二、to_string  将数字转换为string



[LeetCode剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

```cpp
bool cmp(string s1 , string s2)
{
    return (s1+s2)<(s2+s1);
}



class Solution {
public:

    string minNumber(vector<int>& nums) {



        vector<string> solve;

        int len=nums.size();



        for( int i=0; i<len; ++i )

        {

			//此处使用了

            solve.push_back( to_string( nums[i] ) );

        }



        sort( solve.begin(), solve.end(), cmp);



        string rt;

        for(int i=0; i<len; ++i)

        {

            rt+=solve[i];

        }



        return rt;

    }

};

```



## 三、random_shuffle打乱



```cpp
//1、播种随机数种子，如果不播种，也行，只是每次运行随机都是一样的。 
srand(time(0));
random_shuffle( arr.begin() , arr.end() );//arr是vector
reverse( arr.begin(), arr.end() );//arr是vector
```







## ➕03.字符串专题详解





# C++的OJ编程强化（字符和字符串）

目的，精简代码，强化数据结构和算法

- 03.字符和字符串专题（采用C++11编译选项）


##  前置说明




### 1）参考手册网址
用于查看声明，比VS系列编译器的简洁明了一些，还有示例程序
1）[cplusplus.com（我常用这个）](http://www.cplusplus.com/reference/)
网址：`http://www.cplusplus.com/reference/`

2）[zh.cppreference（看C++11常用）](https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5)
网址：`https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5`





### 2）字符和字符串在C语言和C++中的区别和联系

>- 字符：
>C语言和`C++`中都是用char来承载，`C++`中string类，[]运算符返回的也是char
>- 字符串：
>C语言中，用字符数组来承载
>`C++`中用string类来承载
>为了能够将`C++`中其他STL和string类的配合到极致，我们需要非常熟悉C语言风格的字符数组和`C++`的string类的互相转化。







## 一、精简代码



### 1）简化判别字母、数字


分类函数,所在函数库为`ctype.h`

**注意，虽然输入说是int，但是其实我们要放进去的是char（其实是对应的ASCII码值），这样才能判断。**

```cpp
int isalpha(int ch);
//alphabet n.字母表
//若ch是字母('A'-'Z','a'-'z')返回 非0值 ,否则返回0
//虽然我测试大写字母，返回是1，小写字母是2，但我还是不确定底层是不是这样规定的。

int isalnum(int ch);
//alphabet+number
//若ch是字母('A'-'Z','a'-'z')或数字('0'-'9') 返回非0值,否则返回0


int isdigit(int ch);
//digit n.数字
//若ch是数字('0'-'9')返回非0值,否则返回0


int islower(int ch)；
//若ch是小写字母('a'-'z')返回非0值,否则返回0


int isupper(int ch);
//若ch是大写字母('A'-'Z')返回非0值,否则返回0

int tolower(int ch);
//若ch是大写字母('A'-'Z')返回相应的小写字母('a'-'z')
//否则对应的ASCII码不变，直接返回原先的
//返回值是ASCII码，可以强制转换为char

int toupper(int ch);
//若ch是小写字母('a'-'z')返回相应的大写字母('A'-'Z')
//否则对应的ASCII码不变，直接返回原先的
//返回值是ASCII码，可以强制转换为char


int isxdigit(int ch);
//若ch是16进制数('0'-'9','A'-'F','a'-'f')返回非0值, 否则返回0


```



## 二、C++中string类细节源码阅读

<font style="background: yellow" size=3>Tips:字符串是逻辑概念，C语言中用字符数组来承载，C++中用string类来承载</font>

要想短时间强化这些，请暂停自己熟悉的字符数组，进行下面的强化。



### 1）[]运算符重载（用途：完成string类到char的转换）

#### （1-1）cplusplus.com（我常用这个）上的声明如下

<font style="background: yellow" size=5>重点：返回的是“字符”，不是什么string类</font>



```txt

const char& operator[] (size_t pos) const;

char& operator[] (size_t pos);

```





有C++教程上写的声明是，显然是参考的这，并且教程讲参考手册的改为这样，增加了可读性。

```txt

const char & operator[] (int n) const;

char & operator[] (int n);

const char & at(int n) const;

```



#### （1-2）zh.cppreference声明如下

```txt

// 元素访问

    constexpr const_reference operator[](size_type pos) const;

    constexpr reference       operator[](size_type pos);

    constexpr const_reference at(size_type n) const;

    constexpr reference       at(size_type n);

```





[知乎](https://www.zhihu.com/question/35614219/answer/798370856)上对于constexpr的解释

```txt

constexpr是`C++11`引入的，一方面是为了引入更多的编译时计算能力，另一方面也是解决 C++98 的 const 的双重语义问题。

在 C 里面，const 很明确只有「只读」一个语义，不会混淆。C++ 在此基础上增加了「常量」语义，也由 const 关键字来承担，引出来一些奇怪的问题。C++11 把「常量」语义拆出来，交给新引入的 constexpr 关键字。

在 C++11 以后，建议凡是「常量」语义的场景都使用 constexpr，只对「只读」语义使用 const。

```






### 2）成员函数c_str()（用途：完成string类到字符数组的转换）


连接string类和C语言字符数组的桥梁



<font style="background: yellow" size=3>重点：返回的是“const char*”，不是什么string类</font>

cplusplus.com上的声明如下

```txt
const char* c_str() const;	//返回一个以'\0'结尾的字符串的首地址
```





```txt
Get C string equivalent
Returns a pointer to an array that contains a null-terminated sequence of characters (i.e., a C-string) representing the current value of the string object.
This array includes the same sequence of characters that make up the value of the string object plus an additional terminating null-character ('\0') at the end.
翻译：该数组包括组成字符串对象值的相同字符序列，最后还有一个额外的终止空字符（'\ 0'）
```
<font style="background: red" size=3>从说明来看，我们使用这个进行string到字符数组的转换，我们就不要担心在字符数组后有没有加'\0'了，而如果用string类的成员函数copy()来进行转换，它却没有给我们在最后加'\0'，容易导致一些人误用</font>



#### 用法1

//主要要注意，这种const修饰，表示指向位置的内容不准修改。

```cpp

#include<iostream>

#include<string>

using namespace std;



int main()

{

	string str;

	str="abscv";

	//主要要注意，这种const修饰，表示指向位置的内容不准修改。

	const char * p=str.c_str(); 

	

	printf("%c\n",p[1]);

	printf("%c\n",p[2]);

	

	return 0;

}

```



#### 用法2（常用）

用这种复制的方式，就突破了，上一种方式无法修改的桎梏 



```cpp

#include<iostream>

#include<string>

#include<cstring>

using namespace std;



int main()

{

	string str;

	str="abscv";

	

	char p[10];

	//用这种复制的方式，就突破了，上一种方式无法修改的桎梏 

	strcpy(p,str.c_str());

	

	p[1]='K'; 

	printf("%c\n",p[1]);

	printf("%c\n",p[2]);

	

	return 0;

}

```





### 3）C语言字符数组和字符到string类

<font style="background: yellow" size=3>C语言字符数组和字符到string类都很简单，因为都实现了运算符+=和=的重载</font>

#### +=重载（字符用）
```cpp
#include<iostream>
using namespace std;

int main()
{
	char c='9';
	string str="432";
	str+=c;//原型是string& operator+= (char c);
	cout<<str; 
	return 0;
 } 
```


#### =重载（字符用）

```cpp
#include<iostream>
using namespace std;

int main()
{
	char c='9';
	string str="432";
	str=c;//原型是string& operator= (char c);
	cout<<str; 
	return 0;
}
//输出9
```


#### +=重载（字符串用）

```cpp
#include<iostream>
using namespace std;

int main()
{
	char test[]="356425462";
	string str;
	str+=test;//原型string & operator+=(const char * s);
	cout<<str; 
	return 0;
} 
```

#### =重载（字符串用）
```cpp
#include<iostream>
using namespace std;

int main()
{
	char test[]="11111";
	string str="432";
	str=test;//原型为 string& operator= (const char* s);
	cout<<str; 
	return 0;
} 
//输出11111
```






### 3）强化string类的成员函数（熟练到，心到码到）

string类和map等容器的配合，后续会知道好处的。


find查找
substr子串

深信服的笔试似乎蛮喜欢考字符串的。
CCF/CSP好像蛮喜欢那些字符串。









## 4）C++11支持的正则表达式（对付CSP第3题）

正则的编译时比较慢的，我们暂时
字符编码，我们的控制台的字符编码是GBK的，所以，要是能够改为UTF-8就不会乱码

<font size=5 style="background: yellow">注意记得开启C++11编译选项和`#include <regex>`</font>

[链接:看regex头文件定义的传送门](https://zh.cppreference.com/w/cpp/regex)

注意`C++11`新增了正则表达式的标准库支持
在 `C++` 中使用正则表达式，和其它语言差别不大
`C++11` 自带了 6 种正则表达式语法的支持
```txt
ECMAScript
basic
extended
awk
grep
egrep
C++11 默认使用 ECMAScript 语法，这也是 6 种语法中最强大的，假如想使用其他 5 种语法，只需在声明 regex 对象时指定即可
```





C++正则表达式最常用的三个函数为，也是一般用法。
正则表达式算是字符串匹配中的一个微型元。







### 正则表达式
```txt
.表示任意匹配单个字符
*表示匹配0-n个前面那个字符串
+是1-n次
[a-z]区间，a-z
\d{3}表示匹配3个数字，固定是3个
```

### 1）regex_match（正则匹配）
尝试匹配一个正则表达式到整个字符序列(函数模板)


```cpp
#include<iostream>
#include<string>
#include<regex>
using namespace std;

int main()
{
	//正则表达式，也就是匹配规则	 
	//R的意思是取消转义，这样我们就能在里面不用转义了。否则下面的\d要改为\\d 
	regex test(R"(\d*)");
	
	string str="43141324";//现在全是数字，能够匹配上，输出是OK
    
    bool t;
    t=regex_match(str,test);
    //前面是要匹配的，后面是正则表达式（匹配规则）
    //但是如果是"123okom231"这样，用前面的正则表达式，那么结果是No
	
	if(t)
	{
		cout<<"OK"<<endl;
	} 
	else
	{
		cout<<"No"<<endl;
	}
    
    return 0; 
}
```

```cpp
#include<iostream>
#include<string>
#include<regex>
using namespace std;

int main()
{
	//正则表达式，也就是匹配规则	 
	//R的意思是取消转义，这样我们就能在里面不用转义了。否则下面的\d要改为\\d 
	regex test(R"(\d+[a-z]{2}\d+)");
	
	string str="4314er1324";
    
    bool t;
    t=regex_match(str,test);//前面是要匹配的，后面是正则表达式（匹配规则）
	
	if(t)
	{
		cout<<"OK"<<endl;
	} 
	else
	{
		cout<<"No"<<endl;
	}
    
    return 0; 
}
```


### 2）regex_search（正则搜索）





### 3）regex_replace（正则替换）





## 04.C++中string源码剖析



# C++中string源码剖析

 2020-12-11 08:00:01

## 一、源代码来源



分析采用：

### （1）源代码

DevC++5.9.2中的

TDM-GCC 4.8.1

如果没有安装DevC++可以移步网页源代码版本

[libstdc++在线文档：传送门](https://gcc.gnu.org/onlinedocs/gcc-4.9.0/libstdc++/api/a00999_source.html)

### （2）string的使用接口

[cplusplus中string使用传送门](http://www.cplusplus.com/reference/string/string/?kw=string)



## 二、string头文件（标注版）

```cpp
// Components for manipulating sequences of characters -*- C++ -*-
用于操作字符序列的组件 manipulating,v.(暗中)控制，操纵
// Copyright (C) 1997-2013 Free Software Foundation, Inc.
// 
    Copyright,n.版权;著作权
————————描述“自由软件授权begin”————
// This file is part of the GNU ISO C++ Library.  This library is free
// software; you can redistribute it and/or modify it under the
// terms of the GNU General Public License as published by the
// Free Software Foundation; either version 3, or (at your option)
// any later version.

// This library is distributed in the hope that it will be useful,
// but WITHOUT ANY WARRANTY; without even the implied warranty of
// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
// GNU General Public License for more details.

// Under Section 7 of GPL version 3, you are granted additional
// permissions described in the GCC Runtime Library Exception, version
// 3.1, as published by the Free Software Foundation.

// You should have received a copy of the GNU General Public License and
// a copy of the GCC Runtime Library Exception along with this program;
// see the files COPYING3 and COPYING.RUNTIME respectively.  If not, see
// <http://www.gnu.org/licenses/>.
————————描述“自由软件授权end”————
/** @file include/string
 *  This is a Standard C++ Library header.
 */

//
// ISO C++ 14882: 21  Strings library
//

#ifndef _GLIBCXX_STRING
#define _GLIBCXX_STRING	1

#pragma GCC system_header

#include <bits/c++config.h>
#include <bits/stringfwd.h>		//这是一个"内部头文件"，包含在其他库头文件中。不要试图直接使用它
#include <bits/char_traits.h>  // NB: In turn includes stl_algobase.h
#include <bits/allocator.h>		//分配器，用于管理承载字符的“容器”string的内存分配
#include <bits/cpp_type_traits.h>	//"内部头文件"(不要试图直接使用它)
#include <bits/localefwd.h>    // For operators >>, <<, and getline.
#include <bits/ostream_insert.h>	//"内部头文件"
#include <bits/stl_iterator_base_types.h>	//此文件包含所有与迭代器相关的通用实用程序类型，例如iterator_traits和struct iterator。"内部头文件"
#include <bits/stl_iterator_base_funcs.h>	//此文件包含所有与迭代器相关的通用实用程序函数，如distance（）和advance（）。"内部头文件"，不要试图直接使用它
#include <bits/stl_iterator.h>	//这个文件实现了反向迭代器、back-insert\u迭代器，front_insert_迭代器、insert_iterator、__normal_iterator及其支持函数和重载运算符。在剖器STL源代码的地方，用到了."内部头文件"
#include <bits/stl_function.h> // For less	//"内部头文件"
#include <ext/numeric_traits.h> 	//@文件ext/numeric_traits.h，此文件是标准C++库的GNU扩展。
#include <bits/stl_algobase.h> 		//"内部头文件",基础算法头文件
#include <bits/range_access.h>		//"内部头文件",迭代器相关头文件
#include <bits/basic_string.h>		//重点分析1，"内部头文件"
#include <bits/basic_string.tcc>	//重点分析2，basic_string在basic_string.h中定义，部分成员函数在basic_string.tcc中定义。"内部头文件"

#endif /* _GLIBCXX_STRING */
```



参见cplusplus总述：

```txt
String class	（string 类）
Strings are objects that represent sequences of characters.
字符串是表示字符序列的对象。
The standard string class provides support for such objects with an interface similar to that of a standard container of bytes, but adding features specifically designed to operate with strings of single-byte characters.
标准string类提供了对此类对象的支持，其接口类似于标准字节容器的接口，但添加了专门用于操作单字节字符字符串的功能。
The string class is an instantiation of the basic_string class template that uses char (i.e., bytes) as its character type, with its default char_traits and allocator types (see basic_string for more info on the template).
string类是“basic_string（基本字符串） 类模板”的一个实例化，该模板使用char（即字节）作为其字符类型，并具有默认的char_特征和分配器类型（有关模板的更多信息，请参阅basic_string）。
Tips：这个地方就告诉我们具体的实现要看basic_string.h头文件！！！！（重要）
第2点，告诉我们string类是一个“类模板”实例化成的“模板类”！！！（重要）

Note that this class handles bytes independently of the encoding used: If used to handle sequences of multi-byte or variable-length characters (such as UTF-8), all members of this class (such as length or size), as well as its iterators, will still operate in terms of bytes (not actual encoded characters).
注意，这个类独立于所使用的编码来处理字节：如果用于处理多字节或可变长度字符（如UTF-8）的序列，则该类的所有成员（如length或size）及其迭代器仍将按字节（而不是实际编码字符）来操作。

```









## 三、bits/basic_string.h头文件

如果直接去看源码，会比较难理解，因为basic_string的实现使用了COPY-ON-WRITE技术。关于COPY-ON-WRITE技术可移步

写时拷贝技术(copy-on-write)



STL之basic_string好的[CSDN文章传送门](https://blog.csdn.net/liuyuan185442111/article/details/45870441)





## 四、Linux写时拷贝技术

[参考](https://www.cnblogs.com/lengender-12/p/7054896.html)

title: STL强化
date: 2020-06-13 16:00:57
summary: 自用STL





## :smile:05.仿函数统一场理论

# 自建函数和比较类(仿函数)的统一场理论

- STL中自建函数和比较类（仿函数）总结对比、统一





## 应用：自建比较priority_queue和sort

- priority_queue内元素优先级设置
- sort函数中优先级设定


## 一、priority_queue

### 0）难点（没搞懂）

`priority_queue` 优先队列中结构体的优先级设置  
如何理解结构体中overload的小于号呢？  

- 1、可以理解为重载后`小于号`作用是比较出数组中优先级更小的数据，如果返回的是某个数据值更大的一方则值越大优先级越小，相反则值越小优先级越大。  
- 2、优先队列是输出优先级最高的数据的队列。  
- 3、可以简单的记为与sort中的cmp函数效果相反。  



### 1）基本数据类型

int，double，char

>- 优先队列对它们的优先级设置一般是**数字大**的**优先级越高**。

比如下面2个是等价的（最大堆）

```cpp
priority_queue<int> q;
priority_queue<int,vector<int>,less<int> > q;
```

上面

- 第2个参数
  `vector<int>`填写的是来**承载**底层数据结构堆的**容器**
- 第3个参数
  是对第1个参数的**比较类（是1个类）**

如果对于**基本数据类型**想要最小堆

```cpp
priority_queue<int,vector<int>,greater<int> > q;
```


### 2）结构体类型（重载<）

```cpp
struct fruit
{
	string name;
	int price;
};
```

##### 111、方法一

**——下面这几句话很重要——**  

- 1.设置int的优先级，这样**小于<号**的作用还是**小于<号**的作用，所以priority_queue默认还是**最大堆**
  （此处虽然难理解，但是也算是我给自己的“记忆宫殿”**设定的一种记忆逻辑**）
   （PS：原因是，**sort函数中cmp的设定就有点不一样**）

```cpp
struct fruit
{
	string name;
	int price;
	//结构体增加一个，友元函数
	friend bool operator < (fruit f1,fruit f2)
	{
		return f1.price<f2.price;
	}
};
```

- 2.设定string的优先级
- 这样**小于<号**的作用还是**小于<号**的作用，所以priority_queue默认还是**最大堆**
- 表示，**字典序大**的优先级高？**是的!!**

```cpp
struct fruit
{
	string name;
	int price;
	//结构体增加一个，友元函数
	friend bool operator < (fruit f1,fruit f2)
	{
		return f1.name<f2.name;
	}
};
```

代码测试

```cpp
#include<bits/stdc++.h>
using namespace std;
struct fruit
{
	string name;
	int price;
	//结构体增加一个，友元函数
	friend bool operator < (fruit f1,fruit f2)
	{
		return f1.name<f2.name;
	}
};

int main()
{
	priority_queue<fruit> q;
	fruit t;
	t.name="aaa";
	t.price=3;
	
	q.push(t);
	
	t.name="aa";
	t.price=3;
	
	q.push(t);
	
	t.name="aaaaa";
	t.price=3;
	
	q.push(t);
	
	while(!q.empty())
	{
		cout<<q.top().name<<endl;
		q.pop();
	}
	return 0;
}
```

输出为

```txt
aaaaa
aaa
aa
```

##### 222、方法二（比较类）

有没有办法和sort中的cmp函数那样卸载结构体外面呢？
有的，写一个比较类

```cpp
struct cmp
{
	//注意，类中的重载的是()
	bool operator () (fruit f1,fruit f2)
	{
		return f1.price > f2.price; 
	}
}; 
```

使用如下

```cpp
priority_queue<fruit, vector<fruit>, cmp> q;
```







## 二、sort

### 尝试统一sort和 priority_queue  

//从大到小排序  
//怎么说呢，这个和priority_queue中的设定看起来有些相反  

- 1.我尝试合并一下想法，假设，priority_queue的底层也是vector承载
  那么，最大堆，也就是<默认重载是一样的，那么建立堆之后，我们的最大值也就在堆顶。
- 2.这个时候，我们把STL中的**make_heap**扯进来，它在vector上面建堆，就是这样子的，最大的在最后。
- 3.所以，底层的话，这个比较是统一的，
- 4.我们都是重载<，但是priority_queue取数字是**从后面往前面**取。
  我们**sort**后是喜欢**从前面往后面**遍历，自然会出现反常的感觉。


### 方法（建比较函数）

```cpp
bool cmp(int a,int b)
{
	return a>b;	
}
```



2、结构体数据类型





## 三、Question：STL中可以放仿函数的地方也可以放普通函数？

### （0）仿函数和普通函数都能在这个地方使用

Tips：struct和class修饰都OK啦，在这个方面（仿函数的话）

[sort的官方文档](http://www.cplusplus.com/reference/algorithm/sort/?kw=sort) 

```cpp
template <class RandomAccessIterator, class Compare>
void sort (RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

[accumulate的官方文档](http://www.cplusplus.com/reference/numeric/accumulate/?kw=accumulate) 

```cpp
template <class InputIterator, class T, class BinaryOperation>
   T accumulate (InputIterator first, InputIterator last, T init,
                 BinaryOperation binary_op);
```

其实统一是：（强调仿函数**Pred pr**）

```cpp
template <class RandomAccessIterator, class Compare>
void sort (RandomAccessIterator first, RandomAccessIterator last, Pred pr);
```

和

```cpp
template <class InputIterator, class T, class BinaryOperation>
   T accumulate (InputIterator first, InputIterator last, T init,
                 Pred pr);
```

### （1）sort官方文档这么使用

```cpp
// sort algorithm example
#include <iostream>     // std::cout
#include <algorithm>    // std::sort
#include <vector>       // std::vector

//普通自定义函数
bool myfunction (int i,int j) { return (i<j); }

//重载类的()运算符，弄出仿函数
struct myclass {
  bool operator() (int i,int j) { return (i<j);}
} myobject;

int main () {
  int myints[] = {32,71,12,45,26,80,53,33};
  std::vector<int> myvector (myints, myints+8);               // 32 71 12 45 26 80 53 33

  // using default comparison (operator <):
  std::sort (myvector.begin(), myvector.begin()+4);           //(12 32 45 71)26 80 53 33

  // using function as comp，用普通函数作为比较操作
  std::sort (myvector.begin()+4, myvector.end(), myfunction); // 12 32 45 71(26 33 53 80)

  // using object as comp，用“类生产的对象”来作为比较操作
  std::sort (myvector.begin(), myvector.end(), myobject);     //(12 26 32 33 45 53 71 80)

  // print out content:
  std::cout << "myvector contains:";
  for (std::vector<int>::iterator it=myvector.begin(); it!=myvector.end(); ++it)
    std::cout << ' ' << *it;
  std::cout << '\n';

  return 0;
}
```



### （2）accumulate的两种使用方式

```cpp
// accumulate example
#include <iostream>     // std::cout
#include <functional>   // std::minus
#include <numeric>      // std::accumulate

//函数
int myfunction (int x, int y) {return x+2*y;}
//仿函数
struct myclass {
	int operator()(int x, int y) {return x+3*y;}
} myobject;

int main () {
  int init = 100;
  int numbers[] = {10,20,30};

  std::cout << "using default accumulate: ";
  std::cout << std::accumulate(numbers,numbers+3,init);
  std::cout << '\n';

  std::cout << "using functional's minus: ";
  std::cout << std::accumulate (numbers, numbers+3, init, std::minus<int>());
  std::cout << '\n';

    //使用用户自定义函数
  std::cout << "using custom function: ";
  std::cout << std::accumulate (numbers, numbers+3, init, myfunction);
  std::cout << '\n';

//使用对象
  std::cout << "using custom object: ";
  std::cout << std::accumulate (numbers, numbers+3, init, myobject);
  std::cout << '\n';

  return 0;
}
```











