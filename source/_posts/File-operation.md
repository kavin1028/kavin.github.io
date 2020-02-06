layout: post
title: 数据清洗之文件操作
author: kavin
categories: Python
tags:
  - Pandas
  - csv
  - excel
  - mysql
top: false
cover: false
date: 2020-02-03
---

##  csv文件读取  ##
1. 使用read_csv方法读取，结果为dataframe格式  
2. 在读取csv文件时，文件名称尽量是英文  
3. 参数较多，可以自行控制，但很多时候用默认参数  
4. 读取csv时，注意编码，常用编码为utf-8、gbk、gbk2312和gb18030等  
5. 使用to_csv方法快速保存  

###  代码：  ###

import numpy as np  
import pandas as pd  
//专门用来更改文件路径的库  
import os  

//显示路径
os.getcwd()

//设置路径,建议使用双斜线，或者使用r防止转义  
os.chdir('F:\\csdn\\123')  

编码可不写  
data = pd.read_csv('文件名', encoding = 'utf-8')  

//读取csv时默认使用第一行当成列标签  
//打印,5表示只读取5行  
data.head(5)  

//查看数据信息，字段、类型  
data.info()  

//如果要将编码型读成字符串，在括号里加上dtype={'字段名':str}即可  

//如果只要前100行，在括号内加上nrows=100即可  

//设置显示最多的行数和列数  
//最多20列  
pd.set_options('display.max_columns', 20)  
//最多100行  
pd.set_options('display.max_rows', 100)  

//编码可写可不写，默认utf-8，保存在设置的路径下  
//默认保存索引，所以设置为false  
data.to_csv('123.csv',index=False)  

##  excel文件读写  ##

1. 使用read_excel方法读取，结果为dataframe格式  
2. 读取excel文件和csv文件参数大多一样，但要考虑工作表sheet页  
3. 使用to_excel快速保存为xlsx格式  
4. 使用sheet_name控制工作页，或者使用sheet_name=0（表示第一个工作页）  

df1 = pd.read_excel('文件名', sheet_name ='sheet名' )  
df1.to_excel('文件名', index=False, sheet_name='sheet名')  

##  数据库文件读写  ##

1. 使用sqlalchemy建立连接
2. 需要知道数据库的相关参数，如数据库IP地址、用户名和密码等
3. 通过pandas中read_sql函数读入，读取完以后时dataframe格式
4. 通过dataframe的to_sql方法保存  

###  代码：###

import pandas as pd  
import pymysql  
from sqlalchemy import creat-engine  

//建立连接
conn = create_engine('mysql+pymysql://user:passward@IP:3306/test01')  
- user： 用户名  
- passward： 密码  
- IP： 服务器IP，本地用localhost  
- 3306： 端口号  
- test01： 数据库名称  

//sql语句  
sql = 'select * from 表明'  

#读取数据库中的表
df1 = pd.read_sql(sql, con = conn)

//函数形式  
def query(table): host = 'localhost'  
	user = 'root'  
	passward = '密码'  
	database = 'test01'  
	port = '3306'  

	//使用字符串占位符的方法  
	conn = creat_engine('mysql+pymysql://{}:{}@{}:{}/{}'.format  (user,passward,host,port,database))  
	sql = 'select * from ' + table  
	result = pd.read_sql(sql, con = conn)  
	return result  

df2 = query('表名')

####  数据的保存  ####

//例如把test.csv的数据保存到数据库中  
df = pd.read_csv('test.csv')  
try:  
	df.to_sql('表名', con = conn, index = False, if_exists='replace')  
except:  
	print('error')  

df.to_sql(name, con=engine, if_exists='replace/append/fail', index = false)  

//name是表名  
//con是连接  
//if_exists：如果存在此表该如何处理。三个选项append代表追加，replace代表删除原表，建立新表，fail代表什么都不干  
index=False不插入索引
