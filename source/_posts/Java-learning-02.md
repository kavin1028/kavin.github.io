layout: post
title: Java 基础
author: kavin
categories: java
tags:
  - java基础
top: false
cover: false
date: 2019-03-07
---

## 标识符 ##
包名：多单词组成时所有字母小写  
类名接口名：多单词组成时，所有单词首字母大写  
变量名和函数名：多单词组成时，第一个单词首字母小写，第二单词开始首字母大写  
常量名：所有字母大写，多单词时，每个单词用下划线将连接  
## 常量与变量 ##
整数常量：所有整数  
小数常量：所有小数  
布尔型常量：较为特有，只有两个数值：true、false  
字符常量：将一个数字字母或者符号用单引号（‘’）标识  
字符串常量：将一个或多个字符用双引号标识  
Null常量：只有一个数值：null  
变量的概念：就是将不确定数据进行存储，也就是需要在内存中开辟一个空间。  
如何开辟内存空间：就是通过明确数据类型、变量名称、数据来完成 

```java

	public class Demo01 {
		public static void main(String[] args) {
			//定义变量格式；
			//数据类型 变量名 = 初始化值；
			//定义一个int类型变量，取值为4；
			int x = 4;
			System.out.println(x);
		
			x = 10;
			System.out.println(x);
		
			//演示其他数据类型
			byte b = 2;	//范围：-128~127
		
			short s = 3000;
		
			long l = 4l;	//long型数据后加l
		
			float f = 2.3f;	//float类型数据后加f
		
			double d = 34.56;
		
			char ch = '4';
			char ch1 = 'a';
			char ch2 = ' ';
		
			boolean bo = true;
			/*
			 当数据不确定时，需要对数据进行存储时，
			 就定义一个变量来完成存储动作 。
			 */
		}

	}

```
## 运算符 ##
“&”和“&“的区别：  
单&时，左边无论真假，右边都进行运算  
双&时，如果左边为真，右边参与运算，如果左边为假，那么右边不参与运算  
”|“和”||“得区别同理，双或时，左边为真，右边不参与运算  
异或(^)与或（|）得不同之处是：当左右都为true时，结果为false。  
```java

	public class OperateDemo {

		public static void main(String[] args) {
			int a = 3, b;
			b = a++;	//先进行赋值运算再进行自增
			System.out.println(b);
			System.out.println(a);
			
			b = ++a;	//先进行自增再进行赋值运算
			System.out.println(b);
		}

	}

``` 

![运行结果](https://kavin1028.github.io/images/operate.png)

### 转义字符： ###
通过\ 来转变后面字母或者符号得含义  
\n：换行；  
\b：退格；相当于backspace；  
\r：按下回车键‘；window系统，回车符是由两个字符来表示\r \n；  
\t：制表符，相当于tab键；    
```java

	public class Escapechar {
		public static void main(String[] args) {
			System.out.println("hello \n word");	//换行
			System.out.println("hello \b word");	//退格
			System.out.println("hello \r word");	//回车
			System.out.println("hello \t word");	//制表符
			System.out.println(" \\ hello  word \" ");//反斜杠后是什么就转义什么
		}

	}

``` 

![运行结果](https://kavin1028.github.io/images/escape.png)

