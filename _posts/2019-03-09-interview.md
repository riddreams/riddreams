---
layout: post
title: '面试笔记'
subtitle: '不断积累&不断更新'
date: 2017-03-09
categories: 学习
tags: 学习
---

## 一、 数据结构与算法
### 1. 单链表反转
```java
public ListNode reverseList(ListNode head) {
    ListNode pre = null;
    ListNode next = null;
    while (head != null) {
        next = head.next;
        head.next = pre;
        pre = head;
        head = next;
    }
    return pre;
}
```
### 2. 二进制中1的个数
```java
public int count(int n){
	int num = 0;
    while(n != 0){
        n = n & (n-1);
        num++;
    }
    return num;
}
```
## 二、 多线程
### 1. ReentrantLock原理
ReentrantLock的实现基于AQS，可以概括为：先通过CAS尝试获取锁，如果此时已经有线程占据了锁，那就加入CLH（带头结点的双向非循环链表）队列并且被挂起。当锁被释放之后，排在CLH队列队首的线程会被唤醒，然后CAS再次尝试获取锁。

CAS（Compare and Swap，比较和交换）：CAS有3个操作数：内存值V、预期值A、要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做。该操作是一个原子操作，被广泛的应用在Java的底层实现中。在Java中，CAS主要是由sun.misc.Unsafe这个类通过JNI调用CPU底层指令实现。
AQS（AbstractQueuedSynchronizer，队列同步器）：构建锁或其他同步组件的基础框架，内部通过一个int类型的成员变量state来控制同步状态，当state=0时，说明没有任何线程占有共享资源的锁，当state=1时，则说明有线程目前正在使用共享变量，其他线程必须加入同步队列进行等待，AQS内部通过内部类Node构成FIFO的同步队列来完成线程获取锁的排队工作。
