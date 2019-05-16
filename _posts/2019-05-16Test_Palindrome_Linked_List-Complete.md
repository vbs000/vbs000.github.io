---
layout:     post                    # 使用的布局（不需要改）
title:      Palindrome [LinkedList]               # 标题 
subtitle:   Test Palindrome Linked List (Complete) #副标题
date:       2019-05-16              # 时间
author:     NXY                      # 作者
header-img: img/post-bg-debug.png    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Coding
---
# [Test Palindrome Linked List][title]

## 描述

将单链表的头结点也利用起来。

**疑问:**

* 单链表每次访问都要从头结点遍历一遍是否效率太低?有没有改善的办法？
* 判断是否回文的方法是否太暴力？在破坏了原来的链表后，怎么恢复连接？


## 思路


快慢指针和回溯指针的配合需要技巧。

## [完整代码][src]

```java
package org.vbs000.utils;

/**
 * 单链表实现
 * @param <T> 数据类型
 */
public class LinkedList<T> {
    /**
     * 节点-定义为内部类
     * @param <T> 数据类型
     */
    private class Node<T>{
        Node next;
        T data;
        Node(T data){
            this.data = data;
        }
    }

    /**
     * 定义头结点
     */
    public Node head = null;
    /**
     * 定义链表大小
     */
    public int size;

    /**
     * 添加一个元素
     * @param data 数据
     */
    public void add(T data){
        if(head == null){
            head = new Node(data);
            size++;
        }else{
            Node temp = head;
            while(temp.next != null){//遍历至链表末尾
                temp = temp.next;
            }
            temp.next = new Node(data);//将链表末尾指向新建节点
            size++;
        }

    }

    /**
     * 在指定位置插入数据
     * @param idx 坐标
     * @param data 数据
     */
    public void insert(int idx,T data){
        if(idx<0 || idx>size){//如果超出范围
            throw new ArrayIndexOutOfBoundsException("插入的位置超出范围!(实际范围0~"+size+"，输入位置:"+idx+")");
        }else{
            if(head == null){
                head = new Node(data);
                size++;
            }else{
                Node pointerNode = head;
                int count = 0;
                while(pointerNode != null){
                    if((idx-1) == count){
                        Node insertNode = new Node(data);
                        Node nextNode = pointerNode.next;
                        pointerNode.next = insertNode;//将前面的节点指向插入的节点
                        insertNode.next = nextNode;//将新插入的节点的下一个指向原来节点的后一个节点
                        size++;//整体长度+1
                    }
                    pointerNode = pointerNode.next;//往后遍历
                    count++;
                }
            }

        }
    }

    /**
     * 删除指定坐标的节点
     * @param idx 坐标
     */
    public void delete(int idx){
        if(idx<0 || idx>size){//如果超出范围
            throw new ArrayIndexOutOfBoundsException("删除的位置超出范围!(实际范围0~"+size+"，输入位置:"+idx+")");
        }else{
            Node pointerNode = head;
            int count = 0;
            while(pointerNode != null){
                if((idx-1) == count){
                    pointerNode.next = pointerNode.next.next;//将前面的节点指向后面的后面的节点
                    size--;
                }
                count++;
                pointerNode = pointerNode.next;
            }
        }
    }

    /**
     * 获得相应坐标下的数据
     * @param idx 坐标
     * @return
     */
    public T get(int idx){
        if(idx<0 || idx>size-1){//如果超出范围
            throw new ArrayIndexOutOfBoundsException("获取的位置超出范围!(实际范围0~"+size+"，输入位置:"+idx+")");
        }else{
            Node pointerNode = head;
            int count = 0;
            while(pointerNode != null){
                if(count == idx){
                    return (T) pointerNode.data;
                }
                pointerNode = pointerNode.next;
                count++;
            }
            return null;
        }
    }
    public void printAll(){
        Node pointerNode = head;
        int count = 0;
        while(pointerNode != null){
            //if(pointerNode != head){//不是头结点
                System.out.println(("Index["+count+"]")+":"+(T) pointerNode.data);
                count++;
           //}
            pointerNode = pointerNode.next;
        }
    }

    public LinkedList(){
    }


    public boolean isPalindrome(Node head) {
        if (head == null || head.next == null) {//如果头节点为空，或者仅仅只有头结点的话
            return true;//则判断为回文
        }

        Node prev = null;//回溯指针
        Node slow = head;//慢指针
        Node fast = head;//快指针

        while (fast != null && fast.next != null) {//直到快指针走到尽头
            fast = fast.next.next;//快指针走2步
            Node next = slow.next;//慢指针走1步
            slow.next = prev;//回溯指针设为慢指针的下1个，打断原来的下一结点连接
            prev = slow;//回溯指针本身变成原来的慢指针
            slow = next;//慢指针走1步
        }

        if (fast != null) {//如果快指针本身不为空
            slow = slow.next;//慢指针需要纠正1位
        }

        while (slow != null) {
            if (slow.data != prev.data) {//直到查询到不想等的值
                return false;//跳出，判断为不是回文
            }
            slow = slow.next;//慢指针继续往前
            prev = prev.next;//回溯指针往回走
        }

        return true;
    }
}



```


## [测试代码][src]

```java
package org.vbs000.practice.p0;

import org.vbs000.utils.LinkedList;

public class LinkedList_Palindrome {

    public static void main(String[] args) {
	// write your code here
        System.out.println("Hello Algorithm!");
        LinkedList<String> lkList = new LinkedList<>();
        lkList.add("A");
        lkList.add("B");
        lkList.add("C");
        lkList.add("C");
        lkList.add("B");
        lkList.add("A");
		
        lkList.insert(4,"X");
        lkList.delete(4);

        System.out.println("lkList size:"+lkList.size);
        lkList.printAll();

        System.out.println(lkList.isPalindrome(lkList.head));

    }

}
```

## [测试结果][src]

```
Hello Algorithm!
lkList size:6
Index[0]:A
Index[1]:B
Index[2]:C
Index[3]:C
Index[4]:B
Index[5]:A
true
```