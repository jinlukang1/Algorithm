# 算法刷题中C++常见语法及数据结构

由于自己平常用C++较少，需要记录一些刷题中常见的C++语法和数据结构。

## 常见数据结构

map

主要用法

```C++
#include <map>
map<int, string> mapStudent;//容器初始化

mapStudent.size();//容器目前大小

maoStudent[666] = 'Example'//插入方式1

mapStudent.insert(map<int, string>::value_type (1, "student_one"));//插入方式2

mapStudent[666]//取值方式1，无对应值不会报错

mapStudent.at(666)//会进行关键字检查，无对应值会报错

mapStudent.erase(666)//删除元素

iter = mapStudent.find(1);
if(iter != mapStudent.end()) Cout<<"Find, the value is "<<iter->second<<endl;//它返回的一个迭代器，当数据出现时，它返回数据所在位置的迭代器，如果map中没有要查找的数据，它返回的迭代器等于end函数返回的迭代器

mapStudent.find(666);//如果存在返回1，不存在返回0

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
vector<int> vec;//创建vector对象1

vector<int> ilist4(7);//创建vector对象1，此方法创建7个缺省值（0）

vector<int> ilist5(7,3);//创建7个3

vec.push_back(a);//尾部插入值

cout<<vec[0]<<endl;//使用下标访问元素

vector<int>::iterator it;
for(it=vec.begin();it!=vec.end();it++)
    cout<<*it<<endl;//使用迭代器遍历元素

vec.insert(vec.begin()+i,a);//在第i+1个元素前面插入a

vec.erase(vec.begin()+2);//删除第3个元素

vec.erase(vec.begin()+i,vec.end()+j);//删除区间[i,j-1];区间从0开始

vec.size();//大小

vec.clear();//清空

#include<algorithm>
reverse(vec.begin(),vec.end());//将元素翻转，即逆序排列！

sort(vec.begin(),vec.end());//(默认是按升序排列,即从小到大).
//可以通过重写排序比较函数按照降序比较，如下：
//定义排序比较函数：
bool Comp(const int &a,const int &b){
    return a>b;
}
sort(vec.begin(),vec.end(),Comp);//这样就降序排序。
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
