---
layout: post
title: "demo"
date: 2022-12-01 17:28:00 -0000
categories: CATEGORY-1 CATEGORY-2
---
## 203.Remove linkedlist elements
**Question:给定一个链表的头节点`head`和整数`val`,删除链表中所有满足`node.val == val`的节点，返回新的节点头。**

### Gneral Thinking:
根据链表的特性，删除元素意味着将它前一个元素指向它的指针断开，并让它指向下下个元素。因此，需要指定一个目前节点`cur` 以及前一个节点`pre`。题目要求返回头节点，所以也需要设置一个dummyNode指向原本的头节点。
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
