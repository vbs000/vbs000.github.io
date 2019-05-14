---
layout:     post                    # 使用的布局（不需要改）
title:      Test Palindrome               # 标题 
subtitle:   Test Linked List #副标题
date:       2019-05-14              # 时间
author:     NXY                      # 作者
header-img: img/post-bg-debug.png    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Coding
---
# [Test Palindrome Linked List][title]

## 描述

测试编写单链表类。

**疑问:**

单链表头节点设置为空，并且不保存数据，是否浪费?


## 思路


找到链表中点，在中点往两侧遍历，看两侧走过的路径是否完全一致。

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
    public Node head = new Node(null);
    /**
     * 定义链表大小
     */
    public int size;

    /**
     * 添加一个元素
     * @param data 数据
     */
    public void add(T data){
        Node temp = head;
        while(temp.next != null){//遍历至链表末尾
            temp = temp.next;
        }
        temp.next = new Node(data);//将链表末尾指向新建节点
        size++;
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
            Node pointerNode = head;
            int count = -1;
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

    /**
     * 删除指定坐标的节点
     * @param idx 坐标
     */
    public void delete(int idx){
        if(idx<0 || idx>size){//如果超出范围
            throw new ArrayIndexOutOfBoundsException("删除的位置超出范围!(实际范围0~"+size+"，输入位置:"+idx+")");
        }else{
            Node pointerNode = head;
            int count = -1;
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
        if(idx<0 || idx>size){//如果超出范围
            throw new ArrayIndexOutOfBoundsException("获取的位置超出范围!(实际范围0~"+size+"，输入位置:"+idx+")");
        }else{
            Node pointerNode = head;
            int count = -1;
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
            if(pointerNode != head){//不是头结点
                System.out.println(("Index["+count+"]")+":"+(T) pointerNode.data);
                count++;
            }
            pointerNode = pointerNode.next;
        }
    }

    public LinkedList(){
    }


    public boolean isPalindrome(Node head) {
        if (head == null || head.next == null) {
            return true;
        }

        Node prev = null;
        Node slow = head;
        Node fast = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            Node next = slow.next;
            slow.next = prev;
            prev = slow;
            slow = next;
        }

        if (fast != null) {
            slow = slow.next;
        }

        while (slow != null) {
            if (slow.data != prev.data) {
                return false;
            }
            slow = slow.next;
            prev = prev.next;
        }

        return true;
    }
}

```

[title]: https://leetcode.com/problems/palindrome-linked-list