---
layout: post
title: "Algorithm Diary (3)"
date: 2022-12-09 17:28:00 -0000
categories: CATEGORY-1 CATEGORY-2
---
## 203.Remove linkedlist elements
**Question:给定一个链表的头节点`head`和整数`val`,删除链表中所有满足`node.val == val`的节点，返回新的节点头。**

### Gneral Thinking:
根据链表的特性，删除元素意味着将它前一个元素指向它的指针断开，并让它指向下下个元素。因此，需要指定一个目前节点`cur` 以及前一个节点`pre`。一方面题目要求返回头节点，另一方面为了使头节点不需要单独处理，所以也需要设置一个虚拟节点`dummyNode`指向原本的头节点。
### Solution: 
```
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(-1); 
        dummy.next = head; 
        ListNode cur = head, pre = dummy; 
        while(cur != null){
            if(cur.val == val){
                cur = cur.next;
                pre.next = cur; 
            }else{
                pre = cur; 
                cur = cur.next;
            }
        }
        return dummy.next;
    }
```

## 707.Design linkedlist
**Question:设计链表的实现。**

### Gneral Thinking:
链表的本质是由多个链表节点组成。每个节点存储节点本身的值`val`和指向下一个节点的指针`next`。所以需要先定义一个节点的类，后续再LinkedList中完成其他方法
- `get(index)`：获取第index个节点的值，遍历链表到第index个节点，返回该节点的值
- `addAtHead(val)`: 在链表头添加一个值为val的节点。
- `addAtTail(val)`: 
### Solution: 
```
   class ListNode {
    int val;
    ListNode next;
    ListNode(){}
    ListNode(int val) {
        this.val=val;
    	}
	}
class MyLinkedList {
    //size存储链表元素的个数
    int size;
    //虚拟头结点
    ListNode head;

    //初始化链表
    public MyLinkedList() {
        size = 0;
        head = new ListNode(0);
    }

    //获取第index个节点的数值，注意index是从0开始的，第0个节点就是头结点
    public int get(int index) {
        //如果index非法，返回-1
        if (index < 0 || index >= size) {
            return -1;
        }
        ListNode currentNode = head;
        //包含一个虚拟头节点，所以查找第 index+1 个节点
        for (int i = 0; i <= index; i++) {
            currentNode = currentNode.next;
        }
        return currentNode.val;
    }

    //在链表最前面插入一个节点，等价于在第0个元素前添加
    public void addAtHead(int val) {
        addAtIndex(0, val);
    }

    //在链表的最后插入一个节点，等价于在(末尾+1)个元素前添加
    public void addAtTail(int val) {
        addAtIndex(size, val);
    }

    // 在第 index 个节点之前插入一个新节点，例如index为0，那么新插入的节点为链表的新头节点。
    // 如果 index 等于链表的长度，则说明是新插入的节点为链表的尾结点
    // 如果 index 大于链表的长度，则返回空
    public void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }
        if (index < 0) {
            index = 0;
        }
        size++;
        //找到要插入节点的前驱
        ListNode pred = head;
        for (int i = 0; i < index; i++) {
            pred = pred.next;
        }
        ListNode toAdd = new ListNode(val);
        toAdd.next = pred.next;
        pred.next = toAdd;
    }

    //删除第index个节点
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        size--;
        if (index == 0) {
            head = head.next;
	    return;
        }
        ListNode pred = head;
        for (int i = 0; i < index ; i++) {
            pred = pred.next;
        }
        pred.next = pred.next.next;
    }
}
```

## 206. Reverse linkedlist
**Question:反转一个给定链表。**

### Gneral Thinking:
遍历链表，将每个元素的`next`指针断开并重新指向它前一个元素。
### Solution: 
```
public ListNode reverseList(ListNode head) {
        //ListNode dummy = new ListNode();
        //dummy.next = head; 
        //ListNode pre = dummy, cur = head;
        ListNode pre = null; 
        ListNode cur = head; 
        while(cur != null){
            ListNode next = cur.next; 
            cur.next = pre; 
            pre = cur; 
            cur = next; 
        }
        return pre;
```
