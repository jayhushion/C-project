# **软件工程过程作业**


------
## 项目地址：[project](https://github.com/jayhushion/C-project)

## 项目详细
### 需求分析
当今属于大数据时代，人人需要操作大量文件信息，而这款软件系统为学校所设计的学生信息管理系统，学校需要一套学生学籍管理系统来对学生学籍等情况进行管理。建立该系统有利于教务处、学生工作处、师资科、院长办公室、各系辅导员对各自所需的及管理的学生信息进行查阅和管理，可以完成以下几个信息数据操作功能：
> * 1.输入数据
> * 2.排序数据
> * 3.查找数据
> * 4.统计数据
> * 5.显示数据
> * 6.退出系统

还要在用户界面实现：界面自然、清晰、友好，包含所需全部功能，且界面间切换自然。
能够让使用者清楚了解学生信息内容和简洁操作数据信息。
可以较为方便的管理学生信息，进行输入、显示、查询、统计数据等操作。
### 系统设计
#### 系统中的数据定义

此系统定义了两个类：
1.日期类 里面定义了整数型年、月、日
2学生类 里面定义了字符串型学生姓名、布尔型性别、里面继承日期类、
静态变量整数型学生个数。


### 系统的功能设计
![初始界面](https://github.com/jayhushion/C-project/blob/master/2.png)
### 系统的详细设计
#### 输入模块
![输入模块](https://github.com/jayhushion/C-project/blob/master/3.png)
#### 排序模块：
通过两个对象对比出生日期进行排序，找到当前未元素中年龄最小的对象的下标并交换两个对象的数据
#### 查询模块：
先输入要查询对象的名字，通过循环匹配相应的对象数据
，若循环超出当前人数则查无此人，若匹配成功则显示相应匹配对象的信息

#### 统计模块：
先提取学生的学生数信息，通过访问对象数组的性别来统计男女生各多少人。
#### 显示模块：
         通过调取类函数循环显示所有学生的全部信息。
### 系统实现及运行结果
#### （一）系统开发工具
     CODEBLOCK::   ADOBE PHOTOSHOP	CC2018  WPSWORD
#### （二）系统运行界面及结果
#####开始界面：
![开始界面](https://github.com/jayhushion/C-project/blob/master/1.png)
#####输入界面：
![输入界面](https://github.com/jayhushion/C-project/blob/master/4.png)
![输入界面](https://github.com/jayhushion/C-project/blob/master/5.png)
#####排序界面：
![排序界面](https://github.com/jayhushion/C-project/blob/master/6.png)
#####查询界面：
![查询界面](https://github.com/jayhushion/C-project/blob/master/7.png)
#####统计界面：
![统计界面](https://github.com/jayhushion/C-project/blob/master/8.png)
#####显示界面：
![显示界面](https://github.com/jayhushion/C-project/blob/master/9.png)
## 总结
整体程序运行良好，没有发现重大BUG，可以实现应有功能。
 在编写程序调试程序的过程中我学会了很多，比如友元函数的使用以及重载运算符的使用，强化了类的继承和派生的用法和类函数的调用吗，利用友元函数直接调用学生类有关于日期的检查合法性函数。加强了C++语言的编写能力。在编写时发现了无法辨别年月日的区分，利用了重载运算符的方式，分开了年月日及检查日期的合法性。
通过这次的项目实践，对于我来说编写C++程序变得更容易、更熟练了，也为以后JAVA语言的学习打下了基础，因为JAVA语言也是面向对象的语言，也更好的巩固了C语言的使用。以后我会更加对C++语言深入学习的。
## 源代码
```c++
#include <iostream>
#include <string.h>
#include<windows.h>
using namespace std;
#define MAX 100

class CDate  // 定义日期类
{
private:
    unsigned short int year;   // 年
    unsigned short int month;  // 月
    unsigned short int day;    // 日
public:
    CDate(int y=0,int m=0,int d=0);
    bool operator < (CDate d);
    friend istream & operator >> (istream &in,CDate &d);
    friend ostream & operator<<(ostream &out,CDate &d);
    friend bool CheckValid(CDate d);
    friend bool LeapYear(int year);
    void SetDate(int y,int m,int d);
};
CDate::CDate(int y,int m,int d):year(y),month(m),day(d) {}
// 设置日期
void CDate::SetDate(int y,int m,int d)
{
    year=y;
    month=m;
    day=d;
}
// 重载输入运算符>>
istream &operator>>(istream &in,CDate &d)
{
    char ch1,ch2;
    cout<<"请输入日期(输入格式：YYYY-MM-DD)：";
    while(1)
    {
        cin>>d.year>>ch1>>d.month>>ch2>>d.day;
        if (ch1=='-' && ch2=='-')
            if (CheckValid(d)) break;
        cerr<<"时间格式或取值不正确! 请重新输入\n";
    }
    return cin;
}
// 重载输出运算符<<
ostream &operator<<(ostream &out,CDate &d)
{
    out<<d.year<<"年"<<d.month<<"月"<<d.day<<"日";
    return out;
}
// 判断日期d1<d2
bool CDate::operator < (CDate d)
{
    if (year<d.year) return true;
    if (year>d.year) return false;
    if (month<d.month) return true;
    if (month>d.month) return false;
    if (day<d.day) return true;
    return false;
}

// 检查是否为闰年
bool LeapYear(int year)
{
    if (year%4==0 && year%100 || year%400==0)
        return true;
    return false;
}

// 检查日期合法性
bool CheckValid(CDate d)
{
    int n;
    if (d.month<1 || d.month>12) return false;
    if (d.day<1) return false;
    n=31;
    switch(d.month)
    {
    case 2:
        if (LeapYear(d.year))
            n=29;
        else
            n=28;
        break;
    case 4:
    case 6:
    case 9:
    case 11:
        n=30;
        break;
    }
    if (d.day>n) return false;
    return true;
}

class CStudent :public CDate
{
private:
    char *name;              // 姓名
    bool sex;                // 性别
    CDate date;              // 出生日期，类对象作数据成员
public:
    static int num;          // 学生人数
    CStudent();
    void InputData();
    friend void Sort();      // 排序
    friend void FindName();  // 按姓名查询
    friend void Statistic(); // 按性别统计
    friend void Display();   // 显示全部信息
} stu[MAX];
int CStudent::num=0;
CStudent::CStudent() {}
// 输入信息
void CStudent::InputData()
{
    int p;
    char s[41];
    cout<<"请输入学生信息（NO."<<num<<"）：\n";
    cout<<"姓名：";
    cin>>s;
    name=new char[strlen(s)+1];
    strcpy(name,s);
    cout<<"性别(1-男，0-女)：";
    cin>>p;
    if (p)  sex=true;
    else sex=false;
    cin>>date;
    cout<<endl;
}
// 排序
void Sort()
{
    int i,j,p,num;
    char *tn;
    bool ts;
    CDate td;
    num=CStudent::num;
    for(i=1; i<num; i++)
    {
        p=i;
        for(j=i+1; j<=num; j++)
            if (stu[j].date<stu[p].date) p=j;//找到当前未排序元素中年龄最小的对象的下标
        if (p==i) continue;
        //下面交换stu[i]和stu[p]
        tn=stu[i].name;
        stu[i].name=stu[p].name;
        stu[p].name=tn;
        ts=stu[i].sex;
        stu[i].sex=stu[p].sex;
        stu[p].sex=ts;
        td=stu[i].date;
        stu[i].date=stu[p].date;
        stu[p].date=td;
    }
}
// 按姓名查询
void FindName()
{
    char name[41];
    int i,num;
    cout<<"请输入姓名：";
    cin>>name;
    num=CStudent::num;
    for(i=1; i<=num; i++)
        if (strcmp(stu[i].name,name)==0) break;
    if (i>num)
    {
        cout<<"查无此人!"<<endl<<endl;
        return;
    }
    //如果查到了，显示学生信息
    cout<<"姓名："<<stu[i].name<<endl;
    cout<<"性别：";
    if (stu[i].sex)
        cout<<"男"<<endl;
    else
    cout<<"女"<<endl;
    cout<<"生日："<<stu[i].date<<endl;
    cout<<endl;
}
// 按性别统计
void Statistic()
{
    int i,num,s1,s0;
    num=CStudent::num;
    s1=0;
    s0=0;
    for(i=1; i<=num; i++)
        if (stu[i].sex==1)
            s1++;
        else
            s0++;
    cout<<"男生人数："<<s1<<endl;
    cout<<"女生人数："<<s0<<endl;
    cout<<endl;
}

// 显示全部信息
void Display()
{
    int i,num;
    num=CStudent::num;
    for(i=1; i<=num; i++)
    {
        cout<<stu[i].name<<"\t";
        if (stu[i].sex)
            cout<<"男";
        else
            cout<<"女";
        cout<<"\t"<<stu[i].date<<endl;
    }
    cout<<endl;
}

int ui(void)
{
    cout<<"\t\t\t*******************************";
    cout<<"**********\n";
    cout<<"\t\t\t*\t\t学生信息管理系统\t*\n";
    cout<<"\t\t\t*Student Information Management System\t*\n";
    cout<<"\t\t\t*\t\tBETA TEST VERSION1.0\t*\n";
    cout<<"\t\t\t*\t\t键入1~5以运行程序\t*\n";
    cout<<"\t\t\t*\t\t(1) 输入数据\t\t*\n";
    cout<<"\t\t\t*\t\t(2) 排序数据\t\t*\n";
    cout<<"\t\t\t*\t\t(3) 查找数据\t\t*\n";
    cout<<"\t\t\t*\t\t(4) 统计数据\t\t*\n";
    cout<<"\t\t\t*\t\t(5) 显示数据\t\t*\n";
    cout<<"\t\t\t*\t\t(6) 退出程序\t\t*\n";
    cout<<"\t\t\t*\tWRITTEN BY 软件17-2班刘博\t*\n";
    cout<<"\t\t\t*******************************";
    cout<<"**********\n";
}

int main()
{

    int i,p;
    bool end;
    end=false;
    while(!end)
    {
        ui();
        cin>>p;system("cls");
        switch(p)
        {
        case 1:                          // 输入信息
            CStudent::num++;
            stu[CStudent::num].InputData();
            system("pause");
            system("cls");
            break;
        case 2:                          // 排序
            Sort();
            system("pause");
            system("cls");
            break;
        case 3:                          // 按姓名查询
            FindName();
            system("pause");
            system("cls");
            break;
        case 4:                          // 按性别统计人数
            Statistic();
            system("pause");
            system("cls");
            break;
        case 5:                          // 显示全部信息
            Display();
            system("pause");
            system("cls");
            break;
        case 6:                          // 退出
            end=true;
            break;
        }
    }
    return 0;
}

```
