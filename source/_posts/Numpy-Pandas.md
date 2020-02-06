layout: post
title: 数据清洗之常用工具
author: kavin
categories: Python
tags:
  - Numpy
  - Pandas
top: false
cover: false
date: 2020-02-03
---

##  Numpy  ##

####  1、Numpy中常用得数据结构是ndarry格式  ####
####  2、使用array函数创建，语法格式为array(列表或元组)  ####
####  3、可以使用其他函数例如arange、linspace、zeros等创建  ####

###  代码：###
//导入Numpy包  
import numpy as np  

//建立一维数组  
arr1 = np.array([-9, 7, 4, 3])  

//查看数组类型  
type(arr1)  

//可以规定元素类型,dtype可以是int、float、str  
arr2 = np.arry([-9, 7, 4, 3], Dtype = 'str')  

//二维数组  
arr3 = np.arry([1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12])  

//使用迭代器创建(左闭右开）  
np.arange(起始值， 终止值，步长)  

//等差数组（endpoint：是否包含终止值）   
np.linspace(初始值, 终止值, 元素个数, endpoint=True)  

//得到的数组使用“0”填充，只写一个参数就会生成一维数组
np.zeros(行数，列数)  

//使用“1”填充
np.ones([行数，列数)  

//每个元素加1.5
arr3 + 1.5

//判断数组维度  
arr3.ndim

//判断数组形状  
arr3.shape

//判断数组有多少个元素  
arr3.size  

//判断数组内元素类型  
arr3.dtype

//数组访问  
data1 = ((8.5, 6, 4, 1.2, 0.7), (1, 4, 2.3, 6, 3.1), (11, 0.4, 21, 5.2, 16), (3, 4.3, 13, 4.6, 6))  
arr4 = np.arry(data1)  

//打印第一行到第三行，下标从“0”开始，不限制列数  
arr4[0:3]  

等效于  
arr4[0][3]  

//打印指定哪一个位置得元素  
arr4[行，列]  

//打印第几列,不限制行数  
arr4[:, 0:3]

//排序  
s = np.arry([1, 3, 5, 6, 7, 5, 23, 2, 43, 4, 6, 4, 9])  

//sort函数：从小到大进行排序  
np.sort(s)  

//argsort函数：返回的是数据中，从小到大的索引值(下标)  
np.argsort(s)  

//将数组内的元素排序并改变,上面两种写法只是打印视图，并没有改变  
s = np.sort(s)  

//降序的排序  
//结果是列表结构  
sorted(s, reverse=True)  

//结果是数组结构  
np.array(sorted(s, reverse=True))  

//如果是二维数组，会涉及一个轴向得选择  
arr5 = ([3,0,1], [2,4,9], [4,3,6], [3,-1,5])  

//axls为“0”代表以行的方向排序，为“1”则以列的方向排序  
np.sort(arr5,axls = 0)  

//搜索  
np.where(条件)  
例：（大于3返回1，否则返回-1）  
    np.where(s>3, 1, -1)
//如果要返回数组本身把“1”换为数组名即可  

//筛选  
//将满足条件的元素拿出来  
np.extract(s>3, s)  


##  Pandas  ##

###  常用数据结构之Series  ###

####  通过pandas.Series来创建Series数据结构（序列  ####
####  pandas.Series(data, index, dtype, name)  ####
####  上述参数中，data可以为列表、array或dict，index表示索引，必须与数据同长度，name代表对象的名称  ####

###  代码：  ###

//导入包
import pandas as pd  
import numpy as np  

//第一种方法  
series1 = pd.Series([2,8,3,4,6,2,4,54,12,34,19])  
使用type查看数据结构  
type(series1)  

//第二种方法  
series2 = pd.Series([2,8,3,4,6,2,4,54,12,34,19]   index=["a","b","c","d","e"],name='这是一个序列')  

//第三种方法  
series3 = pd.Series({'北京':2.8, '上海':1.3, '广东':4.2, '江苏':3.1})  

//切片或索引方式  

//位置访问，左开右闭  
series3[0:3]  
series3['北京':]  

//标签访问 series3['北京':'江苏']  

//输出值(数组结构)  
series3.values  

//输出行索引  
series3.index  

//元素数据类型  
series3.dtypes 

###  常用数据结构之DataFrame  ###

#### 通过pandas.DataFrame来创建DataFrame数据结构  ####
#### panDas.DataFrame(data, index, dtype, columns)  ####
#### data可以为列表、array或者dict  ####
#### index表示行索引，columns代表列名或列标签  ####

###  代码：  ###

//第一种创建方法，使用嵌套列表  
list1 = [['张三',23,'男'],['李四',27,'女'],['王二',14,'女']]  
df1 = pd.DataFrame(list1, colums=['姓名','年龄','性别'])  
df1.head(5)  

//第二种创建方法，使用字典  
df2 = pd.DataFrame({'姓名':['张三','李四','王二'], '年龄':['23','27','14'], '性别':['男','女','女']})  
df2

//第三种创建方法，使用数组  
array1 = np.array([['张三',23,'男'],['李四',27,'女'],['王二',14,'女']])  
df3 = pd.DataFrame(array1, columns=['姓名','年龄','性别'], index=['a','b','c'])  

//打印数据框结构的值，数组结构  
df3.values  

//打印行索引标签  
df3.index  

//打印列标签,tolist将输出结果转换为列表  
df3.columns.tolist()  

//打印数组维度  
df3.ndim  

//shape、size、dtype都可以使用   