---
title:  "Introduction of CAS"
header:
  teaser: 
categories: 
  - Multithread
tags:
  - Multithread
  - CAS
---

{% include toc title="CAS Introduction" %}


## 1. What is CAS
Full name of CAS is Compare and swap, which is a techniques used when designing concurrent algorithms. Actually, there are three important value in this mechanism, the value in memory(V), expected value(A), new value(B). CPU will compare V and A, if they are equal it will use B to replace V, otherwise do nothing. Finally, CPU will return the old value.

## 2. Example Code
Let's read a piece of Java Code first:
```java
class sampleClass {
	private int value = 0;
	public int updateValue(int x){
	  if(value == x){
		value += x;
	  }else{
		value = 0;
	  }
	  return value;  
	}
}
```
This code works well in single thread program, however, it has many errors if it is used in multithreaded application. Think about this situation, there is an instance of sampleClass and its value is 0, if a thread A call updateValue method by **XXX.updateValue(0)** checking the value and seeing that it is true, a thread B may also do the same thing at the same time, finally they all update value by value += x. However, it is not the proper result what we want.
In fact, this is "check then act" pattern that must be atomic. In another words, any thread that starts to run the block will finish executing without any interference from other threads. Now maybe you know how to solve the problem, just add **synchronized** keyword on the function mark will be all right. That's true, but I will introduce another way to deal with this situation.
```java
public static class sampleClass{
	private AtomicInteger value = new AtomicInteger(0);
	public int updateValue(int x){
	   value.compareAndSet(x,value+x);
	   return value;
	}
} 
```
Here I use java.util.concurrent.atomic package, set value to be AtomicInteger which has a function compareAndSet() that compares the value of AtomicInteger instance to an expected value, if they are equal, swaps the value with the new value.

## 3. More Infomation

If you can read Chinese, here is introduction of java.util.concurrent.atomic package. [Java中的Atomic包使用指南](http://ifeve.com/java-atomic/)