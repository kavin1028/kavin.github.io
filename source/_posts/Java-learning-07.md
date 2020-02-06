layout: post
title: 面向对象
author: kavin
categories: java
tags:
  - java对象
top: false
cover: false
date: 2019-04-07
---
## 封装 ##
封装：是指隐藏对象的属性和实现细节，仅对外提供公公访问方式  
#### 好处： ####
1. 将变化隔离  
2. 便于使用  
3. 提高重用性  
4. 提高安全性 
 
#### 封装原则： ####
将不需要对外提供的内容都隐藏起来  
把属性都隐藏，提供公共方法对其访问  
每个属性都有两个方法：  
set：设置值  
get：获取值  
## 注意：私有(private)仅仅是封装的一种表现形式 ##
## 构造函数 ##
#### 特点： ####
1.	函数名与类名相同  
2.	不用定义返回值类型  
3.	不可以写return语句  

作用：给对象进行初始化  
#### 注意： ####
1. 多个构造函数是以重载的形式存在的  
2. 构造函数和一般函数在写法上有不同，在运行上也有不同  
3. 构造函数是在对象一建立就运行，给对象初始化；而一般方法是对象调用才执行，给对象添加对象具备的功能  
4. 一个对象建立，构造函数只运行一次，而一般方法可以被该对象调用多次  

什么时候定义构造事物：  
当分析事物时，该事物存在具备一些特性或者行为，那么将这些内容定义在构造函数中；  
#### 构造函数代码示例 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/5 9:34
	 * 构造函数
	 *对象一建立就会调用与之对应的构造函数
	 * 构造函数的小细节：
	 * 当一个类中没有定义构造函数时，那么系统会默认给该类加入一个空参数的构造函数
	 * 当在类中自定义了构造函数后，默认的构造函数就没有了
	 */
	public class Constructor {
		Constructor(){
			System.out.println("Constructor run");
		}
		/**
		 * 空函数
		 * Constructor（）{}
		 */
	}
	
	class Constructor2{
		public static void main(String[] args) {
			Constructor c = new Constructor();
			new Constructor();
			//new一次就会执行一次
		}
	}
```
#### 面试小知识-构造代码块 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/5 9:58
	 *
	 */
	public class Constructor01 {
		private String name;
		private int age;
	
		/**
		 * 构造代码块
		 * 作用：给对象进行初始化
		 * 对象已建立就运行，而且优先于构造函数执行
		 * 区别：
		 * 构造代码块是给所有对象进行初始化
		 * 构造函数是给对应的对象初始化
		 * 代码块中定义的时不同对象共性的初始化内容
		 * 一般用于面试
		 */
		{
			//孩子一出生就哭
			//有了这个就不用每一次都调用
			cry();
		}
	
		Constructor01(){
			//构造代码块
			System.out.println("A:name="+name+",age="+age);
			//如果没有这个构造器就执行不了Constructor01 c1 = new Constructor01();
			//原因：
			//我在描述时就规定要么有姓名要么姓名年龄都有
			//不可能没姓名没年龄
		}
	
		Constructor01(String n){
			name = n;
			System.out.println("B:name="+name+",age="+age);
			//cry();
		}
	
		Constructor01(String n,int a){
			name = n;
			age = a;
			System.out.println("C:name="+name+",age="+age);
			//cry();
		}
	
		public void cry(){
			//规定小孩一出生就会哭
			System.out.println("cry...");
		}
	}
	
	class Constructor02{
		public static void main(String[] args) {
			//创建对象
			Constructor01 c1 = new Constructor01();
			//一般方法哭
			c1.cry();
			Constructor01 c2 = new Constructor01("李四");
			Constructor01 c3 = new Constructor01("张三",20);
		}
	}
```
#### this关键字 ###
this：看上去，是用于区分局部变量和成员变量同名情况  
this：就代表他所在函数所属对象的引用  
this代表他所在函数所属对象的应用，简单来说，那个对象在调用this所在函数，this就代表那个对象  
#### this关键字示例 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/7 10:30
	 * this关键字的应用
	 * 需求：判断是否是同龄人
	 * this的应用：当定义类中功能时，该函数内部要用到调用该函数的对象时，这时用this来表示这个对象
	 * 但凡本类功能内部使用了本类对象，都用this表示
	 */
	
	public class Person {
		private int age;
		Person(int age) {
			this.age = age;
		}
	
		public boolean compare(Person p) {
			return this.age == p.age;
		}
	}
	
	class Person01 {
		public static void main(String[] args) {
			Person p1 = new Person(20);
			Person p2 = new Person(25);
			boolean b = p1.compare(p2);
			System.out.println(b);
		}
	}
```
#### this语句应用示例： ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/7 10:57
	 * this语句（this（））的使用
	 * this语句：用于构造函数之间进行互相调用，仅限于构造函数之间
	 * 使用时传相对应的参数
	 * this语句只能定义在构造函数的第一行
	 * 原因：初始化动作要先执行，如果初始化中还有初始化，先执行更细节初始化再执行自己初始化
	 */
	public class Person {
		private String name;
		private int age;
	
		Person(String name){
			this.name = name;
		}
		Person(String name,int age){
			//this.name = name;
			//这个动作有函数封装完了
			//普通函数调用：Person(name);
			//构造函数间用this语句调用
			this(name);
			//this代表对象
			this.age = age;
		}
	}
	
	class Person02{
		public static void main(String[] args) {
			Person p = new Person("lisi",20);
			Person p1 = new Person("zhangsan",20);
		}
	}
```
