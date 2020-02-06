layout: post
title: 面向对象
author: kavin
categories: java
tags:
  - java设计模式
top: false
cover: false
date: 2019-04-16
---
## 主函数 ##
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/9 8:47
	 * public static void main(String[] args)
	 * 主函数：是一个特殊的函数，作为程序的入口，可以被jvm调用
	 * 主函数的定义：
	 * public：代表该函数访问权限最大
	 * static：代表主函数随着类的加载就已经存在了
	 * void：主函数没有具体的返回值
	 * main：不是关键字，但是是一个特殊的单词，可以被jvm识别
	 * （String[] arr）：函数的参数，参数类型是一个数组，该数组中的元素是字符串，字符串类型的数组
	 * 主函数是固定格式的：jvm识别
	 * jvm在调用主函数时，传入的是new String[0]
	 */
	public class MainDemo {
		public static void main(String[] args) {
			System.out.println(args.length);
		}
	
		public void main(int x){
			//这个是可以存在的，方法的重载
		}
	}
```
## 设计模式 ##
Java中有23种设计模式  
#### 单例设计模式 ####
##### 第一种体现方式 #####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/15 21:03
	 * 设计模式：Java中23种设计模式
	 * 解决某一类问题最有效的方法
	 * 单例设计模式：解决一个类在内存只存在一个对象
	 * 想要保证对象唯一
	 * 1. 为了避免其他程序过多建立该类对象，先禁止其他程序建立该类对象
	 * 2. 还为了让其他程序可以访问到该类对象，只好在本类中，自定义一个对象
	 * 3. 为了方便其他程序对自定义对象的访问，可以对外提供一些访问方式
	 * 这三步怎么用代码体现
	 * 1. 将构造函数私有化
	 * 2. 在类中创建一个本类对象
	 * 3. 提供一个方法可以获取到该对象
	 * 对于事物该怎么描述还怎么描述，当需要该事物的对象在内存中唯一时，就将以上三步加上即可
	 * 第一种体现方式
	 * 这个是先初始化对象
	 * 称为：饿汉式
	 * Single类一进内存，就已经创建好了对象
	 * 定义单例建议使用饿汉式
	 */
	public class SingleDemo {
		public static void main(String[] args) {
			Single s1 = Single.getInstance();
			Single s2 = Single.getInstance();
			s1.setNum(23);
			System.out.println(s2.getNum());
		}
	}
	
	class Single {
		private int num;
		//第一步
		private Single(){}
	
		public void setNum(int num) {
			this.num = num;
		}
		public int getNum() {
			return num;
		}
		//第二步
		private static Single s = new Single();
		//第三步
		public static Single getInstance() {
			return s;
		}
		//这三步就保持了对象的唯一性
	}
```
##### 第二种体现方式 #####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/15 22:11
	 * 第二种体现方式
	 * 对象是方法被调用时，才初始化，也叫做对象的延时加载
	 * 称为：懒汉式（什么时候需要什么时候再创建（做））
	 * Single1类进内存，对象还没有存在，只有调用了getInstance方法时，才建立对象
	 */
	public class SingleDemo02 {
		public static void main(String[] args) {
			Single1 s = Single1.getInstance();
			s.setAge(21);
			System.out.println(s.getAge());
		}
	}
	class Single1 {
		private int age;
		private static Single1 s = null;
		private Single1() {}
		public void setAge(int age){
			this.age = age;
		}
		public int getAge(){
			return age;
		}
		public static Single1 getInstance() {
			if (s == null) {
				s = new Single1();
			}
			return s;
		}
	}
```