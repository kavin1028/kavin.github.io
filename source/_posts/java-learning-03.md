layout: post
title: Java 基础
author: kavin
categories: java
tags:
  - java基础
top: false
cover: false
date: 2019-03-14
---

## 判断结构： ## 
### 三种格式 ###  
#### 第一种： #### 

	If(条件表达式)
	{ 
	执行语句; 
	}  

#### 第二种： ####  
//if else结构简写格式： 变量 = （条件表达式）？表达式1：表达式2）；  
//三元运算符：可以简化if else 代码，但因为是一个运算符，所以运算完必须要有一个结果； 

	If(条件表达式)  
	{  
	执行语句；  
	}  
	else  
	{  
	执行语句;    
	} 

#### 第三种： #### 
```
 
	If(条件表达式)  
	{  
	执行语句；  
	}  
	else if(条件表达式）  
	{  
	执行语句;  
	}  
	………  
	else  
	{  
	执行语句;  
	}  
```

#### if和switch语句很像 ####  
##### 具体什么场景下，应用那个语句？ ####  
如果判断得具体数值不多，而是符合byte short int char这四种类型。  
虽然两个语句都可以使用，建议使用switch语句，因为效率稍高。  
其他情况：对区间判断，对结果为boolean类型判断，使用if，if的使用范围更广。  
## 选择结构： ##  
#### 格式 ####  
case之间与default没有顺序，先执行第一个case，没有匹配的case执行default  

	 switch(表达式)  //表达式只接受四种类型：byte int short char  
	 {  
	 case 取值1：  
	 执行语句；  
	 break;  
	 case 取值2:  
	 执行语句;  
	 break;  
	 .....  
	 default:  
	 执行语句;  
	 break;  
	 }  
## 循环结构： ##  
#### 代表语句：while，do while，for ####  
#### while语句格式： ####
  
	while（条件表达式）  
	{  
	循环体（执行语句）；  
	}  

	do while语句格式：  
	do  
	{  
	执行语句；  
	}while（条件表达式）； 
 
#### while：先判断条件，只有条件满足才执行循环体； ####  
#### do while：先执行循环体，再判断条件，条件满足，再继续执行循环体； ####  
#### do while特点是条件无论是否满足，循环体至少被执行一次。 ####  
## for语句格式： ##  
	for（初始化表达式；循环条件表达式；循环后的操作表达式）  
	{  
	执行语句；  
	}  

##### 总结：什么时候用循环结构？ #####  
当对某些语句执行很多次时，就用循环结构。  
##### 循环语句其他特点： #####  
![运行结果](https://kavin1028.github.io/images/fortest.png)  
无限循环最简单表达形式：  
For（；；）{}  

While（true）{}  
计数器思想：通过一个变量记录住数据的状态变化，也需要通过循环完成。   
![运行结果](https://kavin1028.github.io/images/fortest1.png)  
累加思想：通过变量记录住每次变化的结果，通过循环的形式，进行累加工作。   
![运行结果](https://kavin1028.github.io/images/fortest2.png)  
语句嵌套形式：  
![运行结果](https://kavin1028.github.io/images/fortest3.png) 
## 实践 ##  
利用for循环实现输出九九乘法表  
![运行结果](https://kavin1028.github.io/images/ninetest.png) 
### 其他流程控制语句 ###
break（跳出）语句：  
应用范围：选择结构和循环结构  
Continue（继续）语句：  
只能应用于循环结构。继续循环，特点：结束本次循环，继续下一次循环
这两个语句离开应用范围，存在时没有意义的  
break和continue语句作用的范围  
break和continue单独存在时，下面可以有任何语句，因为都执行不到  
![运行结果](https://kavin1028.github.io/images/other.png)
loop：循环  
打印等腰三角形  
![运行结果](https://kavin1028.github.io/images/test.png)
