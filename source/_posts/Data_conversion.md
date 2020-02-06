layout: post
title: 数据清洗之数据转换
author: kavin
categories: Python
tags:
  - Pandas
top: false
cover: false
date: 2020-02-05
---

##  日期格式数据处理  ##

1. Pandas中使用to_datetime()方法将文本格式转换为日期格式  
2. dataframe数据类型如果为datatime64，可以使用dt方法取出年月日等  
3. 对于时间差数据，可以使用timedelta函数将其转换为指定时间单位的数值  
4. 时间差数据，可以使用dt方法访问其常用属性  

当日期类型为int64时(errors代表没有就报错)  
df[列名] = pd.to_datetime(df[所在列名], format = '%Y%m%d', errors='coerce')  

提取年  
df[列名].dt.year  

提取月  
df[列名].dt.month  

提取日  
df[列名].dt.day  

当前时间：  
pd.datetime.now()  

算时间差  
df[列名] = pd.datetime.now() - df[日期所在列名]  

结果为多少天多少小时等等  
转换为天为单位(D换为H就是小时为单位)  
df[列名] = df[列名]/pd.Timedelta('1 D') 科学计数转换为小数计数  
df[列名].round(decimals=3)  

另一种方法转换为天数，但结果是整数(其他单位同理上面那种方法)  
df[列名].astype('timedelta64[D]')  

只有当属性为datetime64或timedelta64时才可以使用dt提取  

##  高阶函数处理  ##

1. 在dataframe中使用apply方法，调用自定义函数对数据进行处理
2. 函数apply，axis=0表示对行进行操作，axis=1表示对列进行操作
3. 可以使用astype函数对数据进行转换
4. 可以使用map函数进行数据转换

###  代码：  ###
假如有一列数据为性别，列名为gender，男为1，女为0，未知为2  
def(f):  
&nbsp;&nbsp;&nbsp;&nbsp;if '0' in str(x):  
&nbsp;&nbsp;&nbsp;&nbsp;return '女性'  
&nbsp;&nbsp;&nbsp;&nbsp;elif '1' in str(x):  
&nbsp;&nbsp;&nbsp;&nbsp;return '男性'  
&nbsp;&nbsp;&nbsp;&nbsp;else:  
&nbsp;&nbsp;&nbsp;&nbsp;return '未知'  
df2['性别'] = df2['gender'].apply(f)  
0、1、2就转换为了我们规定的，因为是文本型数据，所以加引号  

使用map进行转换  
df2['性别'] = df2['gender'].map({'0':'女性', '1':'男性', '2':'未知'})  
或者：  
df2['性别'] = df2['gender'].map(f)  

假如有一列数据为电话号码，列名为number，我们要把后四位变成*打印  
str(x)是为了保证数据是字符类型  
def2['number'].apply(lambda x: str(x).replace(x[7:10], '**'))  

假如要打印后四位  
df2['number'].apply(lambda x: str(x)[7:10])  

##  字符串数据处理  ##

假如有一列数据是价格，类型是文本型，其中有美元符号，列名为price  
1、把价格转换为整数型,因为其中有字符串如美元符号等，所以先处理  
去除特定符号($)  
df1['价格'] = df1['price'].str.strip('$')  

将"，"转换为空  
df1['价格'] = df1['价格'].str.replace(',', '')  

转换为整数型 df1['价格'] = df1['价格'].astype(int)  

2、假如有一列为地址，比如中国，北部，黑龙江，列名为location  
提取指定某一块，比如中间的    

split是切片，得出由三种元素组成的列表，x代表提取第几个元素，写1就代表提取第二个元素，不写就会打印列表  
df1['location'].str.split(',').str[x]  

![](https://i.imgur.com/YnveXfO.png)