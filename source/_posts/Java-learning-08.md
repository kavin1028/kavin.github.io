layout: post
title: 面向对象
author: kavin
categories: java
tags:
  - java基础
top: false
cover: false
date: 2019-04-11
---
## 关键字 ##
static：静态关键字  
用法：是一个修饰符，用于修饰成员（成员变量，成员函数）  
当成员被静态修饰后，就多了一个调用方式，除了可以被对象调用外，还可以直接被类名调用，写法格式：类名.静态成员  
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/8 20:24
	 * 静态：static
	 * 用法：是一个修饰符，用于修饰成员（成员变量，成员函数）
	 * 当成员被静态修饰后，就多了一个调用方式，除了可以被对象调用外
	 * 还可以直接被类名调用，写法格式：类名.静态成员
	 * 特有数据随着对象存储
	 * 共享数据存储在方法区（共享区，数据区）
	 */
	public class StaticDemo01 {
		public static void main(String[] args) {
			/**
			 * Person04 p = new Person04();
			 * p.name = "zhangsan";
			 * p.show();
			 * System.out.println(name+":"+country);
			 */
	
			System.out.println(Person04.country);
		}
	}
	class Person04{
		String name;
		//成员变量，实例变量
		static String country = "CN";
		//静态的成员变量，类变量
		public void show(){
			System.out.println(name+":"+country);
		}
	}
```
#### 什么时候使用静态 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/9 9:16
	 * 什么时候使用静态
	 * 要从两方面下手
	 * 因为静态修饰的内容有成员变量和函数
	 * 什么时候定义静态变量（类变量）
	 * 当对象中出现共享数据时，该数据被静态所修饰
	 * 对象中的特有数据要定义成非静态存在于堆内存中
	 * 什么时候定义静态函数
	 * 当功能内部没有访问到非静态数据（对象的特有数据）那么该功能可以定义成静态的
	 */
	public class StaticDemo02 {
		public static void main(String[] args) {
			Person03 p = new Person03();
			p.show();
			//这个时候不能写静态
			//有了对象后这个功能才有意义
		}
	
	}
	
	class Person03 {
		String name;
		public void show(){
	
			System.out.println("haha");
		}
	}
```
#### static特点： ####
1.	随着类的加载而加载（也就是说，静态会随着类的消失而消失，说明他的生命周期长）
2.	优先于对象存在（静态是现存在，对象是后存在的）
3.	被所有对象所共享
4.	可以直接被类名所调用  

静态的使用：是不是被多个对象共享，是就用静态，不是千万别静态  
#### 实例变量和类变量的区别： ####
1.	存放位置：  
类变量随着类的加载而存在与方法区中  
实例变量随着对象的建立而存在于堆内存中  
2.	生命周期:  
类变量生命周期最长，随着类的消失而消失  
实例变量生命周期随着对象的消失而消失  

静态使用注意事项：  
1.	静态方法只能访问静态成员（包括方法和变量），非静态方法既可以访问静态也可以访问非静态  
2.	静态方法中不可以定义this，super关键字（因为静态优先于对象存在，所以静态方法中不可以出现this）  
3.	主函数是静态的

#### 静态有利有弊 ####
利：对对象的共享数据进行单独空间的存储，节省空间，没有必要每个对象中都存储一份；可以被类名调用  
弊端：生命周期过长，访问出现局限性（静态虽好，只能访问静态）  
#### 静态的应用以及说明文档的制作 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/10 21:37
	 * 静态的应用以及说明文档的制作
	 * 每一个应用程序中都有共性的功能
	 * 可以将这些功能进行抽取，独立封装，以便复用
	 * 虽然可以通过建立ArrayTool的对象使用这些工具方法，对数组进行操作
	 * 问题：
	 * 1.对象是用于封装数据的，可是ArrayTool对象濒危封装特有数据
	 * 2.操作数组的的每一个方法都没有用到ArrayTool对象中的特有数据
	 * 这时就考虑让程序更严谨，是不需要对象的
	 * 可以将ArrayTool中的方法都定义成static的，直接通过类名调用即可
	 * 将方法都静态后，可以方便于使用，但是该类还是可以被其他程序建立对象的
	 * 为了更严谨，强制让该类不能建立对象
	 * 可以通过将构造函数私有化完成
	 * 接下来，将ArrayTool.class文件发送给其他人
	 * 其他人只要将文件设置到classpath路径下，就可以使用该工具类
	 * 但是，很遗憾，该类中到底定义了多少个方法对方并不清楚
	 * 因为该类并没有使用说明文档
	 * 开始制作程序的说明文档（帮助文档，api），Java的说明文档通过文档注释来完成
	 * 如何提取：javadoc -d 目录位置 -author -version ArrayTool.java
	 * 如果要生成文档，这个类必须要有public修饰
	 *
	 * 一个类中默认会有一个空参数的构造函数
	 * 这个默认的构造函数的权限和所属类一致
	 * 如果类被public修饰，那么默认的构造函数也带public修饰符
	 * 如果类没有被public修饰，那么默认的构造函数也没有public修饰
	 * 默认构造函数的权限是随着类的变化而变化的
	 */
	
	/**
	 * 这是一个可以对数组进行操作的工具类，该类中提供了获取最值，排序等功能
	 * @author 张三
	 * @version V1.1
	 */
	public class ArrayTool {
		/**
		 * 空参数构造函数
		 */
		private ArrayTool(){}
		//空构造函数不可以提供出去，对方是可以建立对象的
		/**
		 * 获取一个整形数组中的最大值
		 * @param arr  接收一个int类型的数组
		 * @return 会返回一个该数组中最大值
		 */
		public static int getMax(int[] arr){
			int max = 0;
			for (int x = 1 ; x < arr.length ; x++){
				if (arr[x] > arr[max]){
					max = x;
				}
			}
			return arr[max];
		}
		/**
		 * 获取一个整形数组中的最小值
		 * @param arr  接收一个int类型的数组
		 * @return 会返回一个该数组中最小值
		 */
		public static int getMin(int[] arr){
			int min = 0;
			for (int x = arr.length-1 ; x >= 0 ; x--){
				if (arr[x] < arr[min]){
					min = x;
				}
			}
			return arr[min];
		}
	
		/**
		 * 给int数组进行排序
		 * @param arr 接收一个int类型的数组
		 */
		public static void selectSort(int[] arr){
			for (int x = 0 ; x < arr.length-1 ; x++){
				for (int y = x + 1 ; y < arr.length ; y++){
					if (arr[x] > arr[y]){
						swap(arr,x,y);
					}
				}
			}
		}
		/**
		 * 给int数组进行冒泡排序
		 * @param arr 接收一个int类型的数组
		 */
		public static void bubblleSort(int[] arr){
			for (int x = 0 ; x < arr.length-1 ; x++){
				for (int y = x ; y < arr.length-x-1 ; y++){
					if (arr[y] > arr[y+1]){
						swap(arr,y,y+1);
					}
				}
			}
		}
	
		/**
		 * 给数组中元素进行位置的置换
		 * @param arr 接收一个int类型的数组
		 * @param a 要置换的位置
		 * @param b 要置换的位置
		 */
		private static void swap(int[] arr,int a,int b){
			int temp = arr[a];
			arr[a] = arr[b];
			arr[b] = temp;
		}
	
		/**
		 * 用于打印数组中的元素，打印形式是：[element1,element2,...]
		 * @param arr 接收一个int类型的数组
		 */
		public static void printArray(int[] arr){
			System.out.print("[");
			for (int x = 0 ; x < arr.length ; x++){
				if (x != arr.length-1){
					System.out.print(arr[x]+",");
				}else{
					System.out.println(arr[x]+"]");
				}
			}
		}
	}

```
#### 使用工具 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/10 22:01
	 */
	public class ArrayToolDemo {
		public static void main(String[] args) {
			int[] arr = {1,3,6,2,9,4};
			int max = ArrayTool.getMax(arr);
			System.out.println("Max="+max);
	
			/**
			ArrayTool tool = new ArrayTool();
	
			int max = tool.getMax(arr);
			System.out.println("Max="+max);
	
			int min = tool.getMin(arr);
			System.out.println("Min="+min);
	
			tool.printArray(arr);
			tool.selectSort(arr);
			tool.printArray(arr);
			 */
		}
	}
```

##### 可以把代码拷到本地自己试着运行一下javadoc命令，看看生成的说明文档 #####

#### 静态代码块 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/11 13:19
	 * 静态代码块
	 * 格式：
	 * static{
	 *     静态代码块中的执行语句。
	 * }
	 * 特点：随着类的加载而执行，只执行一次，并优先于主函数
	 * 用于给类进行初始化的
	 */
	public class StaticDemo03 {
		static {
			System.out.println("b");
		}
		public static void main(String[] args) {
			new StaticCode();
			new StaticCode();
			System.out.println("over");
		}
		static {
			System.out.println("c");
		}
	}
	class StaticCode{
		static {
			System.out.println("a");
		}
	}
	//输出顺序：b c a over

```
#### 静态代码块考试知识点 ####
```java
	/**
	 * @Author: kavin
	 * @Data: 2019/4/11 13:34
	 * 考试知识
	 */
	public class StaticDemo04 {
		public static void main(String[] args) {
			new StaticCode1(4);
		}
	}
	class StaticCode1 {
		int num = 9;
		StaticCode1(){
			System.out.println("b");
			//不会打印，没有创建与之对应的对象
		}
	
		/**
		 *静态代码块，给类初始化
		 */
		static {
			System.out.println("a");
			//num属于非静态，不能访问
		}
	
		/**
		 *构造代码块，给对象初始化
		 */
		{
			System.out.println("c"+this.num);
		}
	
		/**
		 *构造函数，给对应对象初始化
		 * @param x
		 */
		StaticCode1(int x) {
			System.out.println("d");
		}
		public static void show() {
			System.out.println("show run");
		}
	}
	//运行结果：a c9 d
	//要理清执行顺序
```
