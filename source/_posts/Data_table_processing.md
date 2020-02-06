layout: post
title: 数据清洗之数据表处理
author: kavin
categories: Python
tags:
  - Pandas
  - Numpy
  - xlrd
top: false
cover: false
date: 2020-02-04
---

##  数据筛选  ##

####  常用方法：  ####
1、在数据中,选择需要的行或者列  
2、基础索引方式,就是直接引用  
3、ioc[行索引名称或者条件,列索引名称或者条件]  
4、iloc[行索引位置,列索引位置]  
5、注意,区分loc和iloc  


###  代码：  ###
import pandas as pd  
import os  
import numpy sas np  

//更改数据存储位置  
os.chdir(r'目录')  
df = pd.read_csv('文件名')  

//如果只取第一列  
df['列名']
  
//取两列或更多,使用嵌套方式（两层[]）  
df[['列名', '列名']]
  
//取两列的第多少行  
df[['列名', '列名']][1:5]
  
//使用loc,定位的是标签,loc第一个参数对应的是行,第二个是列  
//取出索引标签为3和4的(行的方式）  
df.loc[3:4]
  
//取出指定列标签的数据(列方式),head表示前十行  
df.loc[:, ['列名', '列名']].head(10)
  
//指定行和列,行标签1到三  
df.loc[1:3, ['列名', '列名']]  

//单个条件  
df.loc[df.列名 == '值', ['列名', '列名']]  

//多个标签用“&”或“|”连接  
df.loc[(df.列名 == '值') | (df.列名 > 3), ['列名', '列名']]  

//使用iloc  
//第二行到第三行
df.iloc[1:3]  

//第二列到第三列  
df.iloc[:, 1:3]  

//只要第一列和第三列  
df.iloc[:, [0,2]]  

//第一行和第十行以及第一列和第三列  
df.iloc[[0:9], [0,2]]  


##  数据增加和删除  ##

###  常用方法  ###
1、在数据中,直接添加列  
2、使用df.insert方法在数据中添加一列  
3、掌握drop(labels, axis, inplace=True)的用法  
4、labels表示删除的数据,axis表示作用轴,inplace=True表示是否对原数据生效  
5、axis=0按行操作,axis=1按列操作  
6、使用del函数直接删除其中一列  

查找某一列的数据并判断增加到另一列  
大于3则高反之则低  
df['购买量'] = np.where(df['列名'] > 3, 高, 低)  

将第二列放到第一列  
变量名 = df['第一列']  
del df['第一列']  
df.insert(0, '新列名', 变量名)  


删除第一列,不加inplace=True不会对原数据进行操作  
df.drop(labels=['列名'], axis=1)  

删除两列  
df.drop(labels=['列名', '列名'], axis=1)  

删除行标签为3和4的行,label指的是行标签  
df.drop(labels=[3,4], axis=0)  

使用迭代器  
df.drop(labels=range(6,11), axis=0)  

##  数据修改和查找  ##

###  常用方法：  ###
1、在数据中,可以使用rename修改列名或行标签名称  
2、使用loc方法修改数据  
3、使用loc方法查找符合条件的数据  
4、条件与条件之间用&或|连接,分别代表‘且’和‘或’  
5、使用between和isin选择满足条件的行  

###  代码：  ###
df1 = pd.read_csv('文件', encoding = 'utf-8', dtype = str)  
加入一个表有一列为性别,列名为sex,男为1,女为0,未知为2  
df1.loc[df1['sex'] == '0', 'sex'] == '女性'  
df1.loc[df1['sex'] == '1', 'sex'] == '男性'  
df1.loc[df1['sex'] == '2', 'sex'] == '未知'  

修改列标签  
df1.rename(columns={'列名':'新列命', '列名':'新列名'}, inplace=True)  

修改行标签  
df1.rename(index={2:23, 1:31}, inplace=True)  

重置索引(drop = True表示把原数据扔掉)  
df1.reset_index(drop = True, inplace = True)  

如果只运行下面代码会返回布尔值  
df[列名] > 10  

如果需要返回数据则把他放到dataframe里就好  
df[df[列名] > 10]  

取相反条件  
df[~(df[列名] > 10)]  

使用多条件时,一个条件必须用括号括起来用&或|连接  

between函数(只能针对整数型或浮点型)  
4到10,inclusive=true包含4和10,否则不包含,同样需要返回数据需要放到dataframe中  
df[列名].between(4, 10, inclusive = True)  

找出某一列里变量为28和38的,同样需要返回数据需要放到dataframe中,字符型需要加引号  
df[列名].isin([28, 38])  


##  数据整理  ##

常见的合并方法有堆叠和按主键进行合并,堆叠又分为横向堆叠和纵向堆叠,按主键合并类似于sql里面的关联操作  
1、横向堆叠将两张表或多张表在X轴方向,即横向拼接在一起  
2、纵向堆叠将两张表或多张表在Y轴方向,即纵向拼接在一起  
3、注意使用concat时,axis=1用于横向,0代表纵向  
4、注意join取inner或outer时,分别代表交集和并集  

###  代码：  ###
impord xlrd  

workbook = xlrd.open_workbook(文件)  
//获取工作表的名称  
sheet_name = workbook.sheet_name()  
//打开  
order1 = pd.read_excel(文件, sheet_name=名称)  
order2 = pd.read_excel(文件, sheet_name=名称)  
order3 = pd.read_excel(文件, sheet_name=名称)  
//纵向合并(在下方增加),ignore_index=True表示忽略原来的索引并重置索引  
order = pd.concat([order, order2,order3], axis=0, ignore_index=True)  

建议  
basic = pd.DataFrame()  
for i in sheet_name:  
    basic_1 = pd.read_excel(文件,sheet_name = i)  
    basic = pd.concat([basic, basic_i, axis=0, ignore_index=True)  

关联：  
df1 = pd.read_csv(文件1)  
df2 = pd.read_csv(文件2)  

inner表示关联字段两张表都有的就关联在一起,没有就丢弃  
df2 = pd.merge(left = df1, right = df2, how='inner', left_on = '列名', right_on = '列名')  


##  层次化索引  ##

在一个轴上有两个或者两个以上的索引  
1、使用loc语句进行访问  
2、loc里面接收tuple,如loc[(a, b),:]  

###  代码：###
第四列和第一列当作行索引标签  
df = pd.read_csv(文件, index_col[3,0])  

a代表第一层索引的值,b代表第二层索引的值
df.loc[(a,b), [标签名, 标签名]]  

都代表第一层索引  
df.loc[([a,b])]