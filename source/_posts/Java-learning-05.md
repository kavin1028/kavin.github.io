layout: post
title: Java 基础
author: kavin
categories: java
tags:
  - java基础
top: false
cover: false
date: 2019-03-29
---
## 数组 ##
概念：同一种类型数据的结合，其实数组就是一个容器。  
好处：可以自动给数组中的元素从0开始编号，方便操作这些元素。  
格式1：  
元素类型【】 数组名 = new 元素类型【元素个数或数组长度】；  
示例：int【】 arr = new int 【5】；  
格式2：  
元素类型【】 数组名 = new 元素类型【】{元素，元素，……}；  
Int【】 arr = new int【】{3，5，1，7}；  
Int【】 arr = {3，5，1，7}；  
#### 二维数组 ####
数组默认初始化值：null  
定义一个名称为arr的二维数组，二维数组中有三个一维数组  
每一个一位数组中有四个元素  
int[] [] arr = new int[3] [4];  

## 内存结构 ##
#### 栈内存： ####
用于存储局部变量，当数据使用完，所占空间会自动释放；  
#### 堆内存： ####
数组和对象，通过new建立的实例都存放在堆内存中；  
每一个实体都有内存地址值；  
实体中的变量都有默认初始值；  
实体不在被使用，会在不确定的时间被垃圾回收机制回收；  
方法区、本地区、寄存区  
无论什么排序，都可以把代码提取出来，单独封装成一个函数  
Arrays.sort(arr);  
Java中已经定义好的一种排序方式，开发中，对数组排序，要使用该句代码  
### 折半查找 ###
折半查找可以提高效率，但必须保证该数组是有序的数组  
```java

	package study;
	
	/**
	 * @Author: kavin
	 * @Data: 2019/3/25 14:15
	 * 折半查找
	 * 数组必须是有序的
	 * key是指找那个值
	 */

	public class Bisearch01 {
	    public static int halfSearch(int[] arr,int key){
	        int min,max,mid;
	        min = 0;
	        max = arr.length-1;
	        mid = (min + max) / 2;
	
	        while(arr[mid] != key){
	            if(key > arr[mid]){
	                min = mid + 1;
	            }
	            else if(key < arr[mid]) {
	                max = mid - 1;
	            }
	
	            if(min > max){
	                return -1;
	            }
	
	            mid = (max + min) / 2;
	
	        }
	        return mid;
	    }
	
	    /**
	     * 第二种做法
	     */
	
	    public static int halfSearch_2(int[] arr,int key){
	        int min,max,mid;
	        min = 0;
	        max = arr.length-1;
	
	        while(min<=max){
	            mid = (max+min)>>1;
	            if (key>arr[mid]){
	                min = mid + 1;
	            }
	            else if (key < arr[mid]){
	                max = mid - 1;
	            }
	            else {
	                return mid;
	            }
	        }
	        return -1;
	    }
	
		//主方法
	    public static void main(String[] args) {
	        int[] arr = {1,2,3,4,5,6,7,8,9};
	        int index = halfSearch_2(arr,3);
	        System.out.println("index="+index);
	    }
	}

```  

StringBuffer 存数据  
StringBuffer arr = new StringBuffer（）；  
arr.append（）；  
arr.reserve 结果反转  
