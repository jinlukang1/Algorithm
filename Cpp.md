# 算法刷题中C++常见语法及数据结构

由于自己平常用C++较少，需要记录一些刷题中常见的C++语法和数据结构。

## 常见数据结构

map

主要用法，相同的还有unordered_map，包含在对应头文件中，映射内容不排序，查找速度相对快一些。map的映射是会自动排序的。

```C++
#include <map>
//容器初始化
map<int, string> mapStudent;
//对于任意的新string，其初始化int值均为0；
map<string, int> counts;
//容器目前大小
mapStudent.size();
//插入方式1
maoStudent[666] = 'Example';
//插入方式2
mapStudent.insert(map<int, string>::value_type (1, "student_one"));
//取值方式1，无对应值不会报错
mapStudent[666];
//会进行关键字检查，无对应值会报错
mapStudent.at(666)
//删除元素
mapStudent.erase(666)
//它返回的一个迭代器，当数据出现时，它返回数据所在位置的迭代器，如果map中没有要查找的数据，它返回的迭代器等于end函数返回的迭代器!!!
iter = mapStudent.find(1);
if(iter != mapStudent.end()) Cout<<"Find, the value is "<<iter->second<<endl;
//如果存在返回1，不存在返回0
mapStudent.count(666);
//迭代器遍历
for(iter=maps.begin();iter!=maps.end();iter++){
    cout << iter->first;//前面的结构体
    cout << iter->second;//后面的结构体
    }//遍历方法
```

---

vector

主要用法

```C++
#include<vector>
//创建vector对象1
vector<int> vec;
//创建vector对象1，此方法创建7个缺省值（0）
vector<int> ilist4(7);
//创建7个3
vector<int> ilist5(7,3);
//初始化
vector<int> ilist{1,2,3.0,4,5,6,7};
//尾部插入值
vec.push_back(a);
//使用下标访问元素
cout<<vec[0]<<endl;
//使用迭代器遍历元素
vector<int>::iterator it;
for(it=vec.begin();it!=vec.end();it++)
    cout<<*it<<endl;
//在第i+1个元素前面插入a
vec.insert(vec.begin()+i,a);
//删除第3个元素
vec.erase(vec.begin()+2);
//删除区间[i,j-1];区间从0开始
vec.erase(vec.begin()+i,vec.end()+j);
//大小
vec.size();
//清空
vec.clear();
//将元素翻转，即逆序排列！
#include<algorithm>
reverse(vec.begin(),vec.end());
//(默认是按升序排列,即从小到大).
sort(vec.begin(),vec.end());
//可以通过重写排序比较函数按照降序比较，如下：
//定义排序比较函数：
bool Comp(const int &a,const int &b){
    return a>b;
}
//这样就降序排序。
sort(vec.begin(),vec.end(),Comp);
//r行c列向量初始化
vector<vector<int> > newOne(r, vector<int>(c, 0));
//vec查找，需要algorirhm库，等于end()说明没找到
find(vec.begin(), vec.end(), 6) = vec.end();
```

---

string

主要用法

```C++
string s10="qweqweqweq";
string s11(s10,3,4);//s4是s3从下标3开始4个字符的拷贝，超过s3.size出现未定义
string s="abcdefg";
//s.substr(pos1,n)返回字符串位置为pos1后面的n个字符组成的串
string s2=s.substr(1,5);//bcdef
//s.substr(pos)//得到一个pos到结尾的串
string s3=s.substr(4);//efg
//s.insert(pos,str)//在s的pos位置插入str
str.insert(6,str2);
//直接指定删除的字符串位置第十个后面的8个字符
str.erase (10,8);
//直接追加一个str2的字符串
str.append(str2);
//追加字符串形参的前5个字符
str.append("dots are cool",5);
//添加10个'.'
str.append(10u,'.');
//字符串追加也可以用重载运算符实现
str+="lalala";
//在str当中查找第一个出现的needle，找到则返回出现的位置，否则返回结尾
found = str.find(str2);//待测试
```

---

set

主要用法

```C++
begin()//返回set容器的第一个元素
end()//返回set容器的最后一个元素
clear()//删除set容器中的所有的元素
empty()//判断set容器是否为空
max_size()//返回set容器可能包含的元素最大个数
size()//返回当前set容器中的元素个数
rbegin//返回的值和end()相同
rend()//返回的值和rbegin()相同
```

---

stack

主要用法

```C++
stack<char> st;//初始化
stark.push();//入栈
stark.pop();//出栈
```

---

C++输入

```C++
//多种输入方式
//一般情况cin即可
//一行一行的输入，可以接受空格，换行结束。
getline(cin, temp_value);
//接受单个字符
cin.get();
//接受单个字符串，送到数组中，不可以是vector
cin.gets();
//接受任意字符
getchar();
getchar()=='\n';//可以用来判断是否输入回车，用来跳出输入循环，并且记得放在cin后面，否则会丢失一个字符。
```

python输入

主要是通过先读入，再进行切割处理。

```py
#单行输入 每一行均是如此
a = input()
# 多行输入
import sys
lines=sys.stdin.readlines()
```
